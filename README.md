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
| `logo.jpg` | El logo, también usado como vista previa al compartir el enlace |
| `404.html` | Para que una dirección mal escrita no muestre la página de GitHub |

## Lo que la página no puede saber

El puente consulta los arriendos de los **próximos seis meses**. Más allá de eso no sabe
nada, así que la página se topa ahí sola en vez de pintar como «libre» un día que nadie ha
mirado. El puente manda ese límite en el campo `hasta` del JSON.

Si el puente se cae, la página conserva lo último que supo y lo dice. Si nunca alcanzó a
saber nada, apaga el calendario y manda a escribir por WhatsApp: no muestra días libres
que no puede garantizar.

## Lo que vive fuera de este repo

En `Escritorio/MUNDO-MAGICO/` (el computador de Diego):

| | |
|---|---|
| `MANUAL_MUNDO_MAGICO.html` | El manual de la dueña. Se le entrega a ella; no habla de tokens ni de código |
| `ENCENDERLO.md` | La ficha técnica de Diego: cómo publicar, qué revisar, qué queda pendiente |
| `apps-script/` | El puente. `clasp push` **no** publica: hay que correr `desplegar_mundo_magico.ps1` |
| `pruebas/` | `node pruebas/probar_puente.js` antes de publicar el puente |
