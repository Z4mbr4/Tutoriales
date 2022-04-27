---
author: 'Luis Alberto Zambrana'
slug: 'Gestion_de_Documentos_con_OpenKm_sobre_docker'
title: 'Gestion de Documentos con OpenKm sobre docker'
---

# Gestion de Documentos con OpenKm sobre docker

En el siguiente docker-compose se encuentra detallado la instalación de OpenKm un gestor libre de documentos el cual trabaja con etiquetado, categorias, roles de usuarios entre otros.



```yaml
version: '3.2'

services:
  openkm:
    image: openkm/openkm-ce:6.3.9
    ports:
      - 8080:8080   
    volumes:
      - ${PWD}/server.xml:/opt/tomcat/conf/server.xml
      - ${PWD}/OpenKM.cfg:/opt/tomcat/OpenKM.cfg
      - ${PWD}/repository:/opt/tomcat/repository
    links:
      - mysql:mysql

  mysql:
    image: mysql:8.0.13
    command: --default-authentication-plugin=mysql_native_password --character-set-server=utf8 --collation-server=utf8_bin
    environment:
      - MYSQL_DATABASE=okmdb
      - MYSQL_USER=openkm
      - MYSQL_PASSWORD=openkm
      - MYSQL_ROOT_PASSWORD=openkm
    security_opt:
      - seccomp:unconfined
    volumes:
      - ${PWD}/mysql:/var/lib/mysql

```

a su vez necesitaran de dos archivos:

OpenKM.cfg

```
hibernate.dialect=org.hibernate.dialect.MySQL5InnoDBDialect
hibernate.hbm2ddl=none
logback.config=logback.xml

```

server.xml

```
<?xml version='1.0' encoding='utf-8'?>
<Server port="8005" shutdown="SHUTDOWN">
  <Listener className="org.apache.catalina.startup.VersionLoggerListener" />
  <!--APR library loader. Documentation at /docs/apr.html -->
  <Listener className="org.apache.catalina.core.AprLifecycleListener" SSLEngine="on" />
  <!-- Prevent memory leaks due to use of particular java/javax APIs-->
  <Listener className="org.apache.catalina.core.JreMemoryLeakPreventionListener" />
  <Listener className="org.apache.catalina.mbeans.GlobalResourcesLifecycleListener" />
  <Listener className="org.apache.catalina.core.ThreadLocalLeakPreventionListener" />

  <!-- Global JNDI resources -->
  <GlobalNamingResources>
    <!-- Editable user database that can also be used by
         UserDatabaseRealm to authenticate users
    -->
    <Resource name="UserDatabase" auth="Container"
              type="org.apache.catalina.UserDatabase"
              description="User database that can be updated and saved"
              factory="org.apache.catalina.users.MemoryUserDatabaseFactory"
              pathname="conf/tomcat-users.xml" />

    <Resource name="jdbc/OpenKMDS" auth="Container" type="javax.sql.DataSource"
            maxTotal="100" maxIdle="30" maxWaitMillis="10000" validationQuery="select 1"
            username="openkm" password="openkm" driverClassName="com.mysql.cj.jdbc.Driver"
            url="jdbc:mysql://mysql:3306/okmdb?useSSL=false&amp;autoReconnect=true&amp;useUnicode=true&amp;characterEncoding=UTF8&amp;useJDBCCompliantTimezoneShift=true&amp;useLegacyDatetimeCode=false&amp;serverTimezone=UTC"/>

    <Resource name="mail/OpenKM" auth="Container" type="javax.mail.Session"
              mail.smtp.host="localhost" mail.from="noreply@openkm.com"/>

  </GlobalNamingResources>

  <!-- A "Service" is a collection of one or more "Connectors" that share
       a single "Container" Note:  A "Service" is not itself a "Container",
       so you may not define subcomponents such as "Valves" at this level.
       Documentation at /docs/config/service.html
   -->
  <Service name="Catalina">
    <Connector port="8080" address="0.0.0.0" protocol="HTTP/1.1" connectionTimeout="20000" redirectPort="8443" />

    <!-- Define an AJP 1.3 Connector on port 8009 -->
    <Connector port="8009" address="127.0.0.1" protocol="AJP/1.3" redirectPort="8443" />

    <Engine name="Catalina" defaultHost="localhost">
      <!-- Use the LockOutRealm to prevent attempts to guess user passwords via a brute-force attack -->
      <Realm className="org.apache.catalina.realm.LockOutRealm">
        <!-- This Realm uses the UserDatabase configured in the global JNDI
             resources under the key "UserDatabase".  Any edits
             that are performed against this UserDatabase are immediately
             available for use by the Realm.  -->
        <Realm className="org.apache.catalina.realm.UserDatabaseRealm"
               resourceName="UserDatabase"/>
      </Realm>

      <Host name="localhost"  appBase="webapps" unpackWARs="true" autoDeploy="true">
        <Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs"
               prefix="localhost_access_log" suffix=".txt"
               pattern="%h %l %u %t &quot;%r&quot; %s %b" />

        <!-- External resources -->
        <!-- <Context docBase="${catalina.home}/custom" path="/OpenKM/custom" reloadable="true"/> -->
      </Host>
    </Engine>
  </Service>
</Server>
```

Luego de esto deben ejecutar docker-compose up -d y OpenKm se encontrarán funcionando.

**Valores por defecto:**

**Link:** localhost:8080

**Usuario:** okmAdmin

**Contraseña:** admin