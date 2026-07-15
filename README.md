# CV — Diego David Scifo

CV centralizado como código. `resume.json` (esquema [JSON Resume](https://jsonresume.org/)) es la fuente de verdad; `index.html` lo renderiza como web estática, sin build step.

## Estructura

```
resume.json   ← fuente de verdad (editar SOLO esto para actualizar el CV)
index.html    ← renderer estático (GitHub Pages lo sirve directo)
CLAUDE.md     ← instrucciones para agentes de Claude que mantienen el repo
```

## Publicar en GitHub Pages

1. Crear el repo en GitHub (ej: `cv`) y pushear:
   ```bash
   git remote add origin git@github.com:TU_USUARIO/cv.git
   git add . && git commit -m "cv: versión inicial"
   git push -u origin main
   ```
2. En GitHub: **Settings → Pages → Source: Deploy from a branch → main / (root)**.
3. Queda publicado en `https://TU_USUARIO.github.io/cv/`.

## Ver localmente

```bash
python -m http.server 8000
# http://localhost:8000
```

## Exportar a PDF

Abrir la web → Ctrl+P → guardar como PDF (tiene estilos de impresión).
