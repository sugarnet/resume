# CV de Diego David Scifo — instrucciones para el agente

## Fuente de verdad

`resume.json` es la ÚNICA fuente de verdad, en formato [JSON Resume v1.0.0](https://jsonresume.org/schema/).
`index.html` es un renderer estático que lee `resume.json` en el cliente: **no hay build step**.
Actualizar el CV = editar `resume.json`. No tocar `index.html` salvo que se pida un cambio visual.

## Sitio bilingüe (ES/EN)

El sitio detecta el idioma del navegador (`navigator.language`) y muestra ES o EN automáticamente; hay un botón para cambiarlo a mano, que se recuerda en `localStorage`. No hay geolocalización por IP ni llamadas a terceros.

Cualquier campo de texto que **cambie de contenido entre idiomas** (highlights, summary, label, position, nombres de categorías de skills, etc.) debe ser un objeto `{ "es": "...", "en": "..." }` en vez de un string plano. Campos que son iguales en ambos idiomas (nombres de empresas, tecnologías como "Java" o "Angular", nombres de certificaciones, URLs, fechas) se dejan como string plano — el renderer (`index.html`) soporta ambas formas indistintamente vía el helper `L()`.

## Cómo agregar contenido

- **Logro dentro de un trabajo existente** → agregar un objeto `{ "es": "...", "en": "..." }` a `work[].highlights` del trabajo correspondiente. Redactar en español primero, empezando con sustantivo o verbo de acción, incluyendo tecnologías y año si aplica; después traducir al inglés.
- **Trabajo nuevo** → nuevo objeto al INICIO del array `work` (orden cronológico inverso). Fechas en formato `YYYY-MM` o `YYYY`. Omitir `endDate` si sigue vigente. `position` bilingüe solo si el título cambia de idioma (ej. "Desarrollador Web" → "Web Developer"); si ya está en inglés o es igual en ambos ("Java Developer"), dejarlo como string plano.
- **Proyecto personal / trading / side project** → array `projects` (mismo criterio de orden y de bilingüismo que `work`).
- **Curso o certificación** → array `certificates`, ordenado por fecha descendente. El `name` del curso NO se traduce (queda como aparece en el certificado).
- **Tecnología nueva** → agregarla a `skills[].keywords` de la categoría que corresponda (string plano, salvo que la palabra cambie de idioma); crear categoría nueva solo si ninguna encaja.

## Reglas

1. Español, registro profesional pero directo. Nada de frases infladas tipo "apasionado por la excelencia".
2. **Nunca publicar datos sensibles**: DNI, domicilio, fecha de nacimiento. Ubicación solo a nivel ciudad/provincia. Este archivo se publica en una web pública.
3. Validar que el JSON quede bien formado antes de commitear (`python -m json.tool resume.json` o similar).
4. Mensajes de commit en español, formato `cv: <qué se agregó/cambió>`. Ej: `cv: agrega proyecto EA NY Kill Zone`.
5. No inventar ni "mejorar" logros: escribir solo lo que Diego indique, se puede pulir la redacción pero no el contenido.
6. Si Diego pasa un logro ambiguo (sin fecha, sin proyecto asociado), preguntar antes de ubicarlo.

## Verificación local

```bash
python -m http.server 8000
# abrir http://localhost:8000
```

(`fetch` de `resume.json` no funciona abriendo `index.html` con `file://`.)

## Export a PDF

Abrir la web y Ctrl+P → guardar como PDF. La hoja de estilos `@media print` ya está preparada.
