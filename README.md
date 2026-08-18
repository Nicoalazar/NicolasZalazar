# Landing de portafolio personal | Nicolás Joel Zalazar

![HTML5](https://img.shields.io/badge/HTML5-sem%C3%A1ntico-E34F26?style=flat-square&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-variables%20%7C%20Grid%20%7C%20Flexbox-1572B6?style=flat-square&logo=css3&logoColor=white)
![Google Fonts](https://img.shields.io/badge/Google%20Fonts-Fraunces%20%2B%20Public%20Sans-4285F4?style=flat-square&logo=googlefonts&logoColor=white)
![Vercel](https://img.shields.io/badge/Deploy-Vercel-000000?style=flat-square&logo=vercel&logoColor=white)

Landing page personal desarrollada con **HTML y CSS puros**, sin frameworks, librerías ni JavaScript.
Es la entrega **PFO1** de la materia Desarrollo de Sistemas Web, Front End (IFTS N°29, 2do cuatrimestre 2026).

---

## Índice

1. [Demo](#demo)
2. [Qué es esta PFO1](#qué-es-esta-pfo1)
3. [Tecnologías](#tecnologías)
4. [Estructura del proyecto](#estructura-del-proyecto)
5. [Decisiones de diseño y de lógica](#decisiones-de-diseño-y-de-lógica)
6. [Accesibilidad](#accesibilidad)
7. [Cómo ejecutarlo localmente](#cómo-ejecutarlo-localmente)
8. [Declaración de uso de IA](#declaración-de-uso-de-ia)
9. [Autor](#autor)

---

## Demo

**URL publicada en Vercel:** _(pendiente de despliegue)_

**Repositorio:** https://github.com/nicoalazar

_(La captura del sitio se agrega junto con la URL de Vercel.)_

---

## Qué es esta PFO1

La consigna pedía una landing individual que presentara mi nombre y apellido, una presentación, mis
habilidades, una forma de contacto y una sección personal a elección, con el perfil de GitHub
enlazado de manera visible y el proyecto publicado en Vercel.

La sección personal que elegí es **Proyectos destacados**: es la que mejor responde a lo que alguien
busca cuando entra al portafolio de un desarrollador junior, porque muestra código y producto real
en lugar de declaraciones sobre mí mismo.

Todo el contenido del sitio es real: el puesto en el Hospital de Clínicas José de San Martín, la
Tecnicatura en curso, el stack que uso y los cuatro proyectos enlazados.

---

## Tecnologías

| Tecnología | Uso en el proyecto |
|---|---|
| HTML5 semántico | `header`, `nav`, `main`, `footer`, `section`, `article`, `figure`, `form` |
| CSS3 | Variables en `:root`, Flexbox, Grid, `clamp()`, `@keyframes`, media queries |
| Google Fonts | Fraunces (variable) para títulos y Public Sans para texto |
| SVG inline | Iconos de GitHub, LinkedIn, correo, ubicación y flechas |
| Vercel | Publicación del sitio estático |
| Git y GitHub | Control de versiones con un commit por etapa del proceso |

Sin JavaScript, sin frameworks y sin dependencias: el sitio es exactamente lo que se ve en el repositorio.

---

## Estructura del proyecto

```
.
├── index.html              Documento único con las cuatro secciones
├── css/
│   └── style.css           Hoja de estilos organizada en 7 bloques comentados
├── assets/
│   └── img/
│       ├── nicolas-zalazar.jpg   Foto propia, recortada y optimizada
│       └── tuconsulta.jpg        Captura del proyecto en producción
├── .gitignore
└── README.md
```

El CSS está dividido en bloques numerados y comentados: tokens de diseño, reset, tipografía,
componentes, maquetación, media queries e interactividad.

---

## Decisiones de diseño y de lógica

### Paleta clara y colorida

Elegí un fondo cálido (`#fffaf3`) en lugar de blanco puro y un violeta saturado (`#5b2cd9`) como
color de marca, con coral y verde azulado como acentos puntuales. La idea fue que el color marque
jerarquía (antetítulos, estados, enlaces) y no que decore por decorar. Todos los colores viven en
variables CSS dentro de `:root`, así que la paleta se cambia en un solo lugar.

### Tipografía: Fraunces + Public Sans

Descarté a propósito las familias que aparecen en casi todos los portafolios (Inter, Poppins,
Roboto, Montserrat). Fraunces es una serif **variable** con ejes propios, y los uso con intención:

- El `h1` va con `opsz 144`, `SOFT 40` y `WONK 1`, que activan las variantes más expresivas de la fuente.
- Los `h2` y `h3` bajan el tamaño óptico y apagan `WONK`, para que se lean como títulos de servicio y
  no compitan con el nombre.

Public Sans se ocupa del texto corrido y de los antetítulos en mayúsculas, con `letter-spacing`
abierto. La escala tipográfica es fluida: cada paso usa `clamp()` entre el valor de 320px y el de 1280px.

### Flexbox y Grid: por qué cada uno

Uso las dos tecnologías, cada una donde rinde:

- **Flexbox** para distribuir en un solo eje contenido de ancho impredecible: la barra de
  navegación, los grupos de botones, las filas de chips de tecnologías y el pie. Ahí lo que importa
  es cómo se reparte el espacio sobrante y cuándo un elemento baja de línea (`flex-wrap`), no
  alinearlo con lo de arriba o lo de abajo.
- **Grid** para las estructuras bidimensionales: la grilla de habilidades, la de proyectos, el hero y
  las fichas de contacto. Con `repeat(auto-fit, minmax(min(100%, 15rem), 1fr))` la cantidad de
  columnas la calcula el navegador según el ancho disponible, y todas las tarjetas de una fila
  comparten altura sin trucos.

La maquetación es mobile first y en unidades relativas (`rem`, `%`, `ch`, `fr`, `clamp`). Solo hay
tres media queries, y agregan columnas o reordenan el encabezado cuando el ancho ya alcanza.

### Animaciones

Hay tres capas de movimiento, todas con la misma curva y las mismas duraciones (también en variables):

1. **Entrada del hero**: el keyframe `surgir` se aplica a cada hijo con retardos crecientes, lo que
   arma una cascada de lectura. La foto entra con `brotar` (escala y una rotación mínima) y la
   insignia de "2023" flota con `flotar` en bucle alternado.
2. **Transiciones de estado**: subrayado que crece desde la izquierda en el menú, elevación de
   tarjetas y botones, chips que se rellenan, flecha que se desplaza y captura que se acerca apenas
   dentro de su tarjeta.
3. **Revelado al hacer scroll**: las tarjetas aparecen al entrar en pantalla usando
   `animation-timeline: view()`, es decir, animaciones ligadas al scroll resueltas solo con CSS, sin
   JavaScript. Va dentro de un `@supports`, así que en los navegadores que todavía no lo implementan
   el contenido se muestra normalmente.

Todo el bloque queda desactivado bajo `@media (prefers-reduced-motion: reduce)`.

### Formulario estático

La PFO1 es de HTML y CSS, sin back-end. En vez de simular un envío que no existe, el formulario está
maquetado con sus `label` asociados a cada campo y avisa en el propio sitio que todavía no envía
nada, ofreciendo el correo como vía real de contacto. Me pareció preferible ser honesto en la
interfaz antes que aparentar una funcionalidad ausente.

### Qué datos de contacto publico

Publico correo, LinkedIn, GitHub y ciudad; no publico mi teléfono. El repositorio es público y
permanente, y un número de teléfono indexado no se puede "despublicar".

### Proyectos enlazados

- **tuConsulta.com.ar** enlaza al sitio en producción, no a un repositorio, porque su código es privado.
- **seprice-turnos**, **seprice-api**, **club-deportivo-mobile** y **club-deportivo-dotnet** enlazan a
  sus repositorios públicos. Este último es un proyecto colaborativo (sistema de escritorio en C# y
  .NET con WinForms para la gestión de un club deportivo), y la tarjeta lo aclara explícitamente para
  no dar a entender que es un trabajo individual.
- Solo hay dos imágenes reales en el sitio: mi foto y la captura de tuConsulta. Los otros cuatro
  proyectos usan portadas construidas con CSS (gradiente e iniciales), para no descargar imágenes de
  terceros ni inventar capturas de pantalla que no existen.

---

## Accesibilidad

- Enlace de salto al contenido principal como primer elemento enfocable del documento.
- Las dos imágenes tienen `alt` descriptivo; los iconos SVG decorativos van con `aria-hidden="true"`
  y `focusable="false"`.
- Cada `section` se asocia a su encabezado con `aria-labelledby`; el `nav` lleva `aria-label` y el
  enlace activo, `aria-current="page"`.
- Jerarquía de encabezados sin saltos: un `h1`, un `h2` por sección y `h3` en las tarjetas.
- Los tres campos del formulario tienen su `label for` correspondiente.
- Estados `:focus-visible` con contorno visible en todo elemento interactivo.
- Contraste verificado sobre la paleta final: todos los textos superan la relación 4.5:1 exigida por
  WCAG AA (el valor más bajo del sitio es 4.5:1 y la mayoría está por encima de 7:1).
- `prefers-reduced-motion` desactiva animaciones, scroll suave y desplazamientos de hover.

---

## Cómo ejecutarlo localmente

Al ser un sitio estático sin dependencias, alcanza con abrir el archivo:

```bash
git clone https://github.com/nicoalazar/landing-portafolio-personal.git
```

Después se puede abrir `index.html` directamente en el navegador, o levantar un servidor local para
que las rutas relativas se comporten igual que en producción:

```bash
python -m http.server 4321
```

Y entrar a `http://localhost:4321`.

---

## Declaración de uso de IA

**Herramienta utilizada:** Claude Code (Anthropic), modelo Claude Opus, ejecutado desde la terminal
sobre la carpeta del proyecto.

**Plan:** pago, Claude Pro (USD 20 por mes).

**Experiencia previa:** la uso hace meses, prácticamente a diario, en mis proyectos personales; entre
ellos tuConsulta.com.ar y el sistema de turnos que enlazo en la sección de proyectos. No fue mi
primer contacto con la herramienta.

**Para qué la usé en esta PFO1:**

- Leer la consigna y la rúbrica y convertirlas en un checklist de reglas obligatorias antes de
  escribir código.
- Redactar el HTML semántico, la hoja de estilos y este README.
- Recortar y optimizar mi foto y tomar la captura de tuConsulta.com.ar.
- Verificar el resultado en el navegador: responsive, contraste de color, estructura de encabezados,
  `label` asociados y enlaces externos.

**Qué revisé y adapté con mi propio criterio:**

- **Contenido y datos reales.** Definí yo qué proyectos mostrar (tuConsulta.com.ar, seprice-turnos,
  seprice-api, club-deportivo-mobile y club-deportivo-dotnet), qué tecnologías listar según lo que
  realmente uso, y qué datos de contacto se publican y cuáles no: descarté publicar mi teléfono en un
  repositorio público.
  Ningún dato del sitio es genérico ni inventado; todo sale de mi CV y de mis repositorios.
- **Revisión del código generado.** Leí el HTML y el CSS antes de aceptarlos, probé el sitio en el
  navegador y pedí ajustes cuando algo no me cerraba, por ejemplo el comportamiento del encabezado
  fijo en pantallas chicas. También fijé restricciones propias sobre el resultado: estilo claro y
  colorido, tipografía que no fuera la genérica de todos los portafolios, y nada de emojis en el
  sitio, el README ni los mensajes de commit.

**Imágenes:** la foto del hero es una foto propia. Se recortó a formato cuadrado, se optimizó para
web y se le corrigió el balance de blancos, porque la original tenía luz mixta: la pared cálida y mi
cara con un dominante azulado. La corrección es un ajuste clásico de ganancia por canal aplicado con
un script de Pillow, no un retoque con IA generativa. **No hay imágenes generadas ni recreadas con
IA en este proyecto.** La captura de tuConsulta.com.ar es del sitio real que desarrollé.

---

## Autor

**Nicolás Joel Zalazar** — Desarrollador Full Stack Junior, Buenos Aires, Argentina.

- GitHub: https://github.com/nicoalazar
- LinkedIn: https://linkedin.com/in/nicolasjoelzalazar
- Correo: nicozalazar67@gmail.com

Estudiante de la Tecnicatura en Desarrollo de Software (IFTS N°29) y programador junior en el
Hospital de Clínicas José de San Martín.
