---
author: 'Luis Alberto Zambrana'
slug: 'Escribir_en_Markdown'
title: 'Escribir en Markdown'
---

# Escribir en Markdown

En principio les cuento que **Markdown** es un lenguaje de marcado ligero creado por John Gruber que trata  de conseguir la máxima legibilidad y facilidad de publicación tanto en  su forma de entrada como de salida, inspirándose en muchas convenciones  existentes para marcar mensajes de correo electrónico usando texto plano.

> Creo que desde las escuelas se podría enseñar a usar este tipo de herramientas y que en la universidad debería usarse si o si para la entrega de proyectos y/o trabajos

Es importante saber que hay editores de textos que soportan markdown con lo cual aprenderte todas las convenciones no es necesario ya que con un par de clics estarás escribiendo

## 1. Negrita e itálica

**Esto es negrita**

```
    **Esto es negrita**
```

*Esto es itálica*

```
    *Esto es itálica*
```

***Esto es negrita e itálica, conjuntamente\***

```
    ***Esto es negrita e itálica, conjuntamente***
```

## 2. Títulos

Usá uno o más numerales para establecer el nivel de título, en orden ascendente.

# Este es un título de primer nivel

```
    #Este es un título de primer nivel
```

Te recomendamos un H3 o H4 para un primer subtítulo.

```
    ###Este es un título de tercer nivel

    ####Este es un título de cuarto nivel

    #####Este es un título de quinto nivel
```

Ejemplo:

### Este es un subtítulo de tercer nivel

## 3. Enlaces (links)

Los enlaces se pueden construir de dos maneras: 1) abandonando la página en la que se está navegando para ir directamente al sitio al que deriva el enlace; 2) abriendo el sitio del enlace en otra pestaña, manteniendo la navegación en nuestro portal.

**Ejemplo caso 1:**

Este es un link hacia [la página web de General Roca](https://www.generalroca.gov.ar/).

```
    Este es un link hacia [la página web de General Roca](https://www.generalroca.gov.ar/).
```



**Ejemplo caso 2**:

Este es un link hacia [la página web de General Roca](https://www.generalroca.gov.ar/) que abre el enlace en otra pestaña nueva y permite mantener la navegación en nuestro portal.

```
    Este es un link hacia [la página web de General Roca](blank:#https://www.generalroca.gov.ar/) que abre el enlace en otra pestaña nueva y permite mantener la navegación en nuestro portal.
```

Lo que hemos hecho en este caso es anteponer dentro del paréntesis que contiene la URL y sin espacios el siguiente texto: **blank:#**

**Nota**: Si el enlace dirige hacia una página externa, es necesario poner la **URL completa** (incluyendo "http://" o "https://").

**Importante**:

- La etiqueta **blank:#** funciona en cualquier campo Markdown, excepto cuando se arman los atajos desde **grupos de atajos.**
- Si el enlace se refiere a alguna normativa (Ley, Decreto, Resolución, etc.), consultá las recomendaciones específicas en [Vincular normativa](https://www.argentina.gob.ar/contenidosdigitales/disenio/normativa).

##### Cómo vincular correos electrónicos:

Este es un link al correo electrónico [uncorreo@ejemplo.com.ar](mailto:uncorreo@ejemplo.com.ar)

```
    Este es un link a [uncorreo@ejemplo.com.ar](mailto:uncorreo@ejemplo.com.ar)
```

Lo que hemos hecho fue anteponer dentro del paréntesis que contiene la URL y sin espacios el siguiente texto: **mailto:**

**Nota:** Al cliquear en el enlace se abre el correo electrónico en tu dispositivo con ese destinatario.

Otra opción es colocar entre los caracteres "<" y ">" la dirección del correo, por ejemplo:

```
    Este es un link a <uncorreo@ejemplo.com.ar>
```

##### Cómo vincular números de teléfonos

Este es un link al teléfono [(54–298) 4387807](tel:+542984387807)

```
    Este es un link al teléfono [(54–298) 4387807](tel:+542984387807)
```

Lo que hemos hecho fue anteponer dentro del paréntesis que contiene la URL y sin espacios el siguiente texto: **tel:**

**Nota:** Al cliquear en el enlace se habilita la llamada telefónica.

##### Cómo vincular un número de celular para enviar un mensaje por WhatsApp

Este es un link al teléfono [(54–298) 4387807](https://api.whatsapp.com/send?phone=+542984387807).

```
    Este es un link al teléfono [(54–298) 2984387807](blank:#https://api.whatsapp.com/send?phone=+542984387807)
```

Lo que hemos hecho fue anteponer dentro del paréntesis que contiene la URL y sin espacios el siguiente texto: **blank:#https://api.whatsapp.com/send?phone=+542984387807

En **"número-de-teléfono"** hay que escribir el número completo, sin guiones ni símbolos,  característica país, número 9 que identifica que es celular,  característica de localidad y número de teléfono.

###### Mensaje preseteado

Se puede agregar un mensaje preseteado para que, al ingresar a WhatsApp, aparezca en el  campo de texto listo para enviar. En tal caso, sería **blank:#https://api.whatsapp.com/send?phone=5491127716463&text=mensaje**

Donde dice **mensaje** se escribe el texto de la siguiente manera: Hay que reemplazar los espacios entre palabras por el símbolo %20

Si quiero dejar preseteado el mensaje "¡Hola, cómo estás!", hay que  escribirlo ¡Hola,%20Cómo%20estás!. De esta manera, la forma correcta  quedaría **[(54–11) 2771-6463](https://api.whatsapp.com/send?phone=5491127716463&text=¡Hola, Cómo estás!)**

```
    Este es un link al teléfono [(54–11) 2771-6463](blank:#https://api.whatsapp.com/send?phone=5491127716463&text=¡Hola,%20Cómo%20estás!)
```

**Nota:** funciona con números que no estén agendados en el celular.

## 4. Listas

Markdown te permite listar con viñetas o con números.

**Lista con viñetas**

Listá cada ítem usando asterisco, signo de suma o guion corto (*, + o -) como si se tratara de viñetas. Recordá dejar un salto de línea antes de  comenzar a enlistar.

- Ítem 1.

- Ítem 2.

  ```
  -    Lista de ítems sin numeración.
  -    Lista de ítems sin numeración.
  ```

Para indentar u obtener una sangría para indicar jerarquía en el listado, agregá un espacio adelante del guion.

- Lista de ítems sin numeración.
  - 
  - 
- Lista de ítems sin numeración.

**Listado con numeración**

Para una lista con números, usalos seguidos de un punto como viñetas.

1. Ítem 1

2. Ítem 2

   ```
   1.  Lista de ítems numerada.
   2.  Lista de ítems numerada.
   ```



## 5. Imágenes inline

1. Subí la imagen en el apartado **Insertar imagen** que aparece dentro del tipo página, página de libro o noticia en la que estás trabajando.
2. Completá los campos **Texto alternativo** (sirve para los lectores de pantalla, normalmente describe la tipografía) y **Título**.
3. Posicioná el cursor en el campo de texto donde quieras que vaya la imagen y hacé clic en el botón **Insert**.

Ejemplo de cómo subir una imagen al servidor.

**Así se ve el enlace de la imagen inline:**

<img src="https://github.com/Z4mbr4/Tutoriales/blob/main/culturalibre.png" alt="CulturaLibre" style="zoom:25%;" />



```
`<img src="Aca tenes que poner donde esta ubicada la imagen" alt="CulturaLibre" style="zoom:25%;" />`
```

Fijate que con style podes agregar un zoom personalizado (la imagen que yo elegí era muy grande)
