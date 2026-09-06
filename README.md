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

El manual para la dueña del negocio y el código del puente viven aparte, en
`Escritorio/MUNDO-MAGICO/`.
