# Steam Showcase Builder

Herramienta gratuita para crear **escaparates animados para tu perfil de Steam** (GIFs divididos que calzan perfecto entre sí), directamente en el navegador. Sin cuentas, sin tokens, sin marcas de agua y sin subir tus archivos a ningún servidor.

## ¿Para qué sirve?

En Steam, los escaparates de ilustraciones y de Workshop muestran **varias imágenes separadas una al lado de la otra**. Si quieres que se vean como una sola imagen continua, cada pieza tiene que tener el ancho exacto y hay que descartar el espacio que Steam deja entre ellas. Si no, la parte chica queda "corrida" y no calza con la grande.

Esta herramienta arma todo en un solo lienzo, le agregas capas (fondo, personaje, textos, marco, efectos) y al exportar lo corta automáticamente en los GIFs que Steam necesita, ya alineados.

## Tipos de escaparate

| Pestaña      | Archivos que genera           | Medidas                                   |
|--------------|-------------------------------|-------------------------------------------|
| Destacado    | 1 GIF                         | 630 px de ancho                           |
| Ilustración  | 2 GIFs (grande + tira)        | 506 px + 100 px (con 9 px ocultos entre medio) |
| Taller       | 5 GIFs (Workshop)             | 5 × 122 px (con 4 px ocultos entre cada uno)   |
| Adaptable    | 1 GIF                         | 630 px, el alto se ajusta al fondo        |
| Avatar       | 1 imagen                      | 512 × 512 px                              |

El alto lo eliges tú (por defecto 824 px).

## Funciones

- **Fondo:** imagen, GIF animado, WebP o video (MP4/WEBM). Ajustes de cubrir/ajustar, y **"Alinear con perfil"**: escala un fondo de perfil de 1920 px y lo recorta en la posición exacta del escaparate para que se funda con tu fondo de Steam. Brillo, contraste, saturación, tono y desenfoque.
- **Personajes (varios):** quitar fondo de tres formas — rápido (color de las esquinas), clave de color (chroma key, también para GIF y video) o **IA que corre en tu propio PC** ([@imgly/background-removal](https://github.com/imgly/background-removal-js)). Escala, rotación, voltear, 10 animaciones (respiración, ola, flotar, balanceo, latido, temblor, giro 3D, zoom, glitch…), efectos de luz, resplandor, pegatina, eco y sombra, "integrar en el fondo" y corrección de color.
- **Textos (varios):** 38 fuentes, orientación horizontal / apilada / de lado, degradado, borde, sombra y 26 animaciones (Glow, Tube Charge, Holo Foil, Chrome Neon, Embers, Molten Gold, Glitch, máquina de escribir, ola de letras…).
- **Marcos:** 18 estilos (clásico, neón, HUD, película, arcoíris, glitch, espinas…), animados o estáticos. Cada pieza del escaparate lleva su propio marco.
- **Efectos:** 40 efectos en bucle perfecto (Matrix, Sakura, Lightning, Pentagram, Hyperspace, nieve, lluvia, chispas, VHS…) más un Glitch general.
- **Exportar:** duración del bucle, FPS y colores. Si un GIF pasa del límite (5 MB por defecto) se **optimiza solo**. Incluye el truco hex, descarga en ZIP y PNG estático.
- **Optimizador de GIF:** baja el peso de cualquier GIF (colores, escala, saltar cuadros) o en modo automático hasta el límite.
- **Hex patcher:** cambia el último byte de tus GIFs de `0x3B` a `0x21`.
- **Mockup de perfil**, **guardar/abrir proyecto** (.json) y una **guía paso a paso** para subirlo a Steam con los comandos de consola.

## Cómo usarlo

1. Abre `index.html` en Chrome, Brave o Edge (doble clic). Necesita internet solo para cargar fuentes y librerías.
2. Elige el tipo de escaparate arriba (por ejemplo **Ilustración**).
3. Agrega fondo, personaje, textos, marco y efectos desde el panel izquierdo. Arrastra en la vista previa para mover la capa seleccionada y usa la rueda del mouse para escalarla.
4. Pulsa **Descargar GIFs**.
5. Sigue la pestaña **Cómo subirlo**.

## Subirlo a Steam (resumen)

1. Ve a <https://steamcommunity.com/sharedfiles/edititem/767/3/> (subir material gráfico).
2. Elige el archivo y pega en el título el carácter invisible `⠀` (U+2800) para que no aparezca texto debajo.
3. Abre la consola (F12 → Console), pega el comando y presiona Enter:
   - Ilustración / Destacado:
     ```js
     $J('#image_width').val(1000).attr('id',''),$J('#image_height').val(1).attr('id','');
     ```
   - Capturas:
     ```js
     $J('#image_width').val(1000).attr('id',''),$J('#image_height').val(1).attr('id','');$J('[name=file_type]').val(5);
     ```
   - Workshop (sube las 5 partes en orden):
     ```js
     $J('[name=consumer_app_id]').val(480);$J('[name=file_type]').val(0);$J('[name=visibility]').val(0);
     ```
4. Marca la casilla de autoría, guarda y repite con cada parte.
5. **Modificar perfil → Escaparates** y elige las obras en cada espacio.

> Los escaparates se desbloquean desde el nivel 10 de Steam (uno más cada 10 niveles). Los comandos de consola y el truco hex son trucos de la comunidad, no funciones oficiales de Steam, así que podrían dejar de funcionar si Steam cambia algo.

## Tecnología

Un solo archivo HTML con JavaScript puro. Usa [gifenc](https://github.com/mattdesl/gifenc) para crear los GIFs, [fflate](https://github.com/101arrowz/fflate) para el ZIP, `ImageDecoder` del navegador para leer GIFs animados y Google Fonts para las fuentes.

---

No está afiliado a Valve ni a Steam.
