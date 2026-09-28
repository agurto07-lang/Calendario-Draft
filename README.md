Calendario Linaje Fénix — calendario-linaje-fenix.html

Calendario mensual interactivo para la comunidad Linaje Fénix, en un único archivo HTML autocontenido (incluye todo el CSS, JS e imágenes en base64 — no depende de ningún archivo externo). Edición actual: Halloween — Octubre 2026.

Para usarlo, solo abre el archivo .html en cualquier navegador (doble clic) o compártelo tal cual por WhatsApp/correo/Drive.

1. Cómo editar el contenido

Todo el contenido dinámico está al inicio de la etiqueta <script>, cerca del final del archivo. Ábrelo con cualquier editor de texto (VS Code, Notepad++, etc.) y busca estas secciones:

Mes y año
js
const YEAR = 2026;
const MONTH = 10; // octubre (1-12)

Cambia estos dos valores para pasar a otro mes. El calendario recalcula automáticamente qué día de la semana cae el día 1, cuántos días tiene el mes, y qué días quedan "en el pasado" según la fecha real del dispositivo que lo abre.

Actividades / eventos
js
const events = {
  2:  [{ icon:"📺🍿", title:"Cine en Casa", place:"Surco", time:"7:30 pm" }],
  10: [
        { icon:"🏄", title:"Paddle", place:"Playa los Yuyos - Barranco", time:"4:45 - 7:00 pm" },
        { icon:"🌙🚶", title:"Ruta Nocturna", place:"Magdalena del Mar", time:"12:00 am (medianoche)" }
      ],
  ...
};
La clave es el número de día del mes.
Cada día admite uno o varios eventos (por eso el valor es una lista [ ... ]).
Campos por evento: icon (emoji, se muestra en la celda), title, place, time.
Si no hay lugar/hora definidos aún, usa "Por confirmar". Para fechas especiales sin lugar/hora aplicable (feriados, etc.) se usa "—".
Al hacer clic en un día con eventos se abre un popup con el detalle completo (lugar + hora) de todos los eventos de ese día.
Cumpleaños
js
const birthdays = [
  { day:5,  name:"Max Valeriano Arias" },
  { day:7,  name:"Valentín Ramirez" },
  ...
];
Se muestran en la barra lateral "🎂 CUMPLEAÑOS", ordenados por columnas (izquierda a derecha, de arriba hacia abajo) en pantallas medianas/móviles.
Privacidad automática: en toda la interfaz (sidebar, celda del día, popup) el nombre se muestra como Primer nombre + inicial del segundo apellido/nombre (ej. "Max Valeriano Arias" → "Max V."). Esto lo hace la función privacyName(), no hace falta abreviar los nombres manualmente en el array.
El día del cumpleaños, ese cumpleañero aparece resaltado en dorado en la barra lateral y dispara un banner animado arriba del calendario ("¡Feliz cumpleaños...!") si coincide con la fecha real del día en que se abre el archivo.
Días feriados / fechas especiales
js
const holidays = [4, 8];

Lista simple de números de día. Cada uno se pinta con rayas doradas, borde dorado y una etiqueta "FERIADO" en la celda, independientemente de si tiene o no actividades asociadas. Solo agrega o quita números para el mes correspondiente.

2. Iconos de los días de la semana

En el HTML (buscar dow-row), cada columna del encabezado tiene un ícono editable:

html
<div class="dow mon"><span class="dow-icon">🎃</span><span class="dow-full">LUNES</span><span class="dow-short">LUN</span></div>

Edición actual (tema Halloween): 🎃 Lunes · 🦇 Martes · 🕷️ Miércoles · 👻 Jueves · 🧪 Viernes · 💀 Sábado · 🧙 Domingo.

Los colores de cada columna se controlan en el CSS con .dow.mon, .dow.tue, etc., usando las variables de :root (--fire-red, --ember, --gold, --leaf, --sky, --lav, --magenta).

3. Imágenes del header y del fondo

El logo Fénix, el header (imagen superior) y el fondo del calendario están embebidos como base64 directamente en el CSS/HTML (por eso el archivo pesa ~2 MB). Hay versión distinta para escritorio y para móvil (se cambia automáticamente con un @media (max-width:640px)):

.header { background: url(data:image/jpeg;base64,...) } → imagen del header, PC.
Dentro del media query móvil, otra regla .header{ background:url(...) } → imagen del header, móvil.
.sheet { background: ... url(data:image/jpeg;base64,...) } → fondo detrás de todo el calendario, PC.
Dentro del media query móvil, otra regla .sheet{ background:... } → fondo, móvil.

Para reemplazar cualquiera de estas imágenes en el futuro (ej. cambiar de tema en diciembre), hay que volver a convertir la nueva imagen a base64 y pegar el texto resultante en el lugar correspondiente. Si prefieres, puedes pedir que se haga este cambio y se entrega el archivo ya actualizado.

4. Estructura general (por si necesitas tocar el diseño)
Header: imagen de fondo + logo Fénix (<img> embebido) + texto "OCTUBRE / 2026" en HTML/CSS encima.
Sidebar (#bdayList): lista de cumpleaños, en 2 columnas cuando el ancho de pantalla es ≤900px.
Calendario (#daysGrid): grilla de 7 columnas. En móvil tiene scroll horizontal (con flechas ‹ › táctiles) porque las columnas mantienen un ancho mínimo legible en vez de comprimirse.
Popup de evento (#eventModal): se abre al hacer clic en cualquier día con actividades y/o cumpleaños.
Footer: franja inferior con las frases de la comunidad.
5. Notas
El archivo es 100% autocontenido: se puede reenviar, subir a Drive o abrir sin internet.
Todo el texto y lógica está en español; los nombres de clases/variables están en inglés (estándar en desarrollo web) pero no afectan el uso.
Cualquier cambio de contenido (eventos, cumpleaños, mes) se puede seguir pidiendo directamente en el chat — no es necesario editar el código a mano salvo que prefieras hacerlo tú mismo.
