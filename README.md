# Módulo [nombre del curso] — Material en Quarto

Material didáctico por tema, escrito en Quarto (`.qmd`) con código en **R y
Python**, estructurado como: Motivación → Revisión teórica → Ejercicios
resueltos → Ejercicios propuestos.

## Estructura del repositorio

```
modulo-curso/
├── _quarto.yml                      # configuración global (tema, TOC, formato)
├── styles.css                       # estilos de las cajas de color
├── _plantilla_tema.qmd              # plantilla en blanco: copiar para cada tema nuevo
├── 01_ejemplo-medidas-tendencia-central.qmd   # ejemplo ya desarrollado
├── 02_tema-...qmd
├── 03_tema-...qmd
└── .gitignore
```

**Convención de nombres:** `NN_nombre-corto-del-tema.qmd` (dos dígitos +
guion bajo), así el orden de los temas queda claro en el explorador de
archivos y en GitHub.

## 1. Requisitos previos (una sola vez)

En Positron necesitas ambos lenguajes activos en el mismo proyecto:

1. **R**: instala el paquete `reticulate`, que es el puente que permite usar
   chunks `{r}` y `{python}` en un mismo documento.
   ```r
   install.packages("reticulate")
   ```
2. **Python**: ten un entorno (venv o conda) con las librerías que uses
   (`pandas`, `matplotlib`, `numpy`, etc.). En Positron, selecciona ese
   intérprete de Python desde el selector de intérpretes (arriba a la
   derecha).
3. Si `reticulate` no detecta automáticamente tu entorno, fija la ruta en el
   chunk `setup` de cada `.qmd`:
   ```r
   library(reticulate)
   use_virtualenv("ruta/o/nombre/del/entorno", required = TRUE)
   ```
4. Instala **Quarto CLI** (si no viene ya con Positron):
   https://quarto.org/docs/get-started/

## 2. Flujo para crear un tema nuevo

1. Copia `_plantilla_tema.qmd` y renómbralo, p. ej. `02_probabilidad.qmd`.
2. Completa cada sección; usa las pestañas `## R` / `## Python` dentro de
   `::: {.panel-tabset}` para el mismo ejercicio en ambos lenguajes.
3. Renderiza para revisar en Positron:
   - Botón **Render** (▶) en la barra superior del editor, o
   - desde la terminal integrada:
     ```bash
     quarto render 02_probabilidad.qmd
     ```
4. El resultado es un único `.html` autocontenido (`embed-resources: true`
   en `_quarto.yml`), lo que significa que **no genera carpetas `_files`
   adicionales** y es el archivo que subes a Moodle.

## 3. Versionamiento con GitHub

```bash
git init
git add .
git commit -m "Estructura inicial del módulo"
git branch -M main
git remote add origin https://github.com/<usuario>/<repo>.git
git push -u origin main
```

Flujo por tema (recomendado):
```bash
git checkout -b tema-02-probabilidad
# ... trabajas y renderizas ...
git add 02_probabilidad.qmd
git commit -m "Agrega tema 2: probabilidad"
git push -u origin tema-02-probabilidad
# luego Pull Request -> main
```

El `.gitignore` ya excluye los `.html` generados y las carpetas de caché
(`.quarto/`, `_freeze/`, `*_files/`), para no versionar archivos pesados o
regenerables. Si prefieres versionar también los `.html` finales (por
ejemplo, para tener respaldo exacto de lo subido a Moodle), quita esa línea
del `.gitignore`.

## 4. Subir a Moodle

- Cada `.qmd` renderizado produce **un `.html` autocontenido** (incluye CSS,
  JS, imágenes y gráficos embebidos en base64): no depende de archivos
  externos.
- En Moodle: **Agregar actividad o recurso → Archivo**, sube el `.html`, y
  en la configuración marca *"Mostrar → Incrustar"* (o *"Abrir"*) para que
  se visualice dentro del curso en lugar de forzar la descarga.
- Alternativa: si quieres que Moodle liste automáticamente todos los temas
  en una sola página de navegación, se puede convertir el proyecto en un
  **Quarto Book** (`project: type: book` en `_quarto.yml`) y subir el sitio
  completo comprimido como recurso de tipo **Carpeta**, apuntando a
  `index.html`. Puedo preparar esa variante si te interesa.

## 5. Próximos pasos

Cuéntame los temas concretos del módulo (nombres y, si los tienes, el
orden/silabo) y te genero cada `.qmd` ya desarrollado siguiendo esta misma
plantilla, con la motivación, la teoría, y los ejercicios resueltos/
propuestos ya redactados en R y Python.
