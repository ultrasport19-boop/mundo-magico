# Mundo Mágico Pencahue

Arriendo de juegos inflables para cumpleaños, en Pencahue, Región del Maule.

**La página:** https://ultrasport19-boop.github.io/mundo-magico/

## Cómo funciona

La página no tiene los juegos escritos dentro. Los pide a un puente en Google Apps Script,
que a su vez lee dos bases de Notion:

- **🎈 Juegos** — el catálogo. La columna `Disponibilidad` es el stock.
- **📅 Arriendos** — las reservas. Solo las `Confirmado` bloquean fechas.

Así, para agregar un juego o bloquear un día no hay que tocar este repositorio: se escribe
en Notion y la página se actualiza sola en menos de diez minutos.

La página **solo lee**. Los pedidos llegan por WhatsApp y se anotan a mano. Por eso la
llave que conecta con Notion es de solo lectura.

## Archivos

| Archivo | Qué es |
|---|---|
| `index.html` | Toda la página: estilos, contenido y lógica en un solo archivo |
| `gracias/` | Número de reserva, resumen y pasos. Se abre con el enlace «Ver qué pasa ahora» que aparece después de tocar «Reservar» (nada navega solo). Lleva `noindex`. Los datos van después del `#` (número, fecha, juegos y montos; nunca nombre ni dirección) |
| `fotos/` | Copias livianas de las fotos **propias** de los juegos, sin metadatos. Se usan cuando la URL de Notion venció. Fotos de catálogo de terceros no se copian aquí |
| `logo.jpg` | El logo, también usado como vista previa al compartir el enlace |
| `404.html` | Para que una dirección mal escrita no muestre la página de GitHub |
| `manual/` | El manual de la dueña, en `/mundo-magico/manual/`. Lleva `noindex`: es para ella, no para los clientes |

El número de WhatsApp está en dos lugares: la constante `WSP` de `index.html` y la de
`gracias/index.html`. Si cambia, se cambia en los dos.

«Reservar por WhatsApp» abre WhatsApp en la misma pestaña (sin `target="_blank"`), como
funcionó siempre: abrir otra pestaña no está probado en el navegador interno de Facebook.

## Condiciones que la página trae escritas

Los juegos, sus precios y los días tomados salen de Notion. Lo demás está escrito en
`index.html` y solo se cambia aquí, cuando la dueña cambia una condición:

| Qué | Dónde |
|---|---|
| Traslado ($5.000 o $10.000, y qué sectores tienen valor conocido), generador y días de anticipación | Objeto `COND` |
| Precio por llevar dos juegos juntos (por id de Notion) | Lista `JUNTOS` |
| Horario, abono, lluvia, viento y demás respuestas | Sección «Lo que hay que saber», preguntas frecuentes y `gracias/` |

## Pruebas

La página publicada no tiene modo de prueba ni otro número que `WSP`. Para probar sin
escribirle a nadie se usa un servidor local, fuera de este repositorio, que cambia el número
al servir la página. La dirección nunca puede traer un número: eso permitiría desviar pedidos.

## Lo que la página entiende del puente

| Campo | Para qué | Obligatorio |
|---|---|---|
| `juegos`, `diasLlenos`, `ocupados`, `hasta`, `maxPorDia`, `actualizado` | Catálogo y calendario | Sí (como hasta ahora) |
| `usados` | Juegos ya comprometidos por fecha. Sin él, la página los cuenta desde `ocupados` | No |
| `juegos[].fotos` | Todas las fotos del juego; la tarjeta las desliza | No |
| `juegos[].ocupaCupo` | `false` = ese juego no cuenta para el tope por día | No |
| `resenas` | `[{texto, nombre}]`, solo reseñas reales con permiso. Sin él, la sección no aparece | No |

## Lo que la página no puede saber

El puente consulta los arriendos de los **próximos seis meses**. Más allá de eso no sabe
nada, así que la página se topa ahí sola en vez de pintar como «libre» un día que nadie ha
mirado. El puente manda ese límite en el campo `hasta` del JSON.

Si el puente se cae, la página conserva lo último que supo y lo dice. Si nunca alcanzó a
saber nada, o lo que guardó el navegador tiene más de un día, apaga el calendario y manda a
escribir por WhatsApp: no muestra días libres que no puede garantizar.

## Lo que vive fuera de este repo

En la carpeta del proyecto, en el computador de quien lo mantiene:

| | |
|---|---|
| `MANUAL_MUNDO_MAGICO.html` | El manual de la dueña. Se le entrega a ella; no habla de tokens ni de código |
| `ENCENDERLO.md` | La ficha técnica: cómo publicar, qué revisar, qué queda pendiente |
| `apps-script/` | El puente. `clasp push` **no** publica: hay que correr `desplegar_mundo_magico.ps1` |
| `pruebas/` | `node pruebas/probar_puente.js` antes de publicar el puente |
