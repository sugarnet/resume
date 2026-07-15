# CV de Diego David Scifo — instrucciones para el agente

## Fuente de verdad

`resume.json` es la ÚNICA fuente de verdad, en formato [JSON Resume v1.0.0](https://jsonresume.org/schema/).
`index.html` es un renderer estático que lee `resume.json` en el cliente: **no hay build step**.
Actualizar el CV = editar `resume.json`. No tocar `index.html` salvo que se pida un cambio visual.

## Cómo agregar contenido

- **Logro dentro de un trabajo existente** → agregar un string a `work[].highlights` del trabajo correspondiente. Redactar en español, empezando con sustantivo o verbo de acción, incluyendo tecnologías y año si aplica.
- **Trabajo nuevo** → nuevo objeto al INICIO del array `work` (orden cronológico inverso). Fechas en formato `YYYY-MM` o `YYYY`. Omitir `endDate` si sigue vigente.
- **Proyecto personal / trading / side project** → array `projects` (mismo criterio de orden).
- **Curso o certificación** → array `certificates`, ordenado por fecha descendente.
- **Tecnología nueva** → agregarla a `skills[].keywords` de la categoría que corresponda; crear categoría nueva solo si ninguna encaja.

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
