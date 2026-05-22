# Fase 1 — Arquitectura física del rack de producción

Documentación técnica del subsistema físico: rack, contenedores, flujo
productivo, post-cosecha con deshidratadora y preparación de sustrato
(esterilización + inoculación).

**Revisión actual:** `0.2-relleno-parcial`.

---

## Estructura del directorio

```
fase1-arquitectura-fisica/
├── main.tex                       # documento maestro LaTeX
├── params.tex                     # parámetros editables (H, W, D, T_amb, ...)
├── referencias.bib                # bibliografía
├── secciones/
│   ├── 01-rack.tex
│   ├── 02-contenedores.tex
│   ├── 03-asignacion-especies.tex
│   ├── 04-bom.tex
│   ├── 05-flujo-productivo.tex
│   ├── 06-postcosecha.tex
│   └── 07-preparacion-sustrato.tex   ← nuevo (esterilización + inoculación)
├── diagramas/
│   ├── flujo-productivo.mmd       # mermaid (incluye §1.7 aguas arriba)
│   └── flujo-postcosecha.mmd      # mermaid con bifurcación fresco/seco
├── plantilla-secado.csv           # caracterización experimental vacía
├── cotizaciones_pendientes.md     # BOM físico con placeholders
├── pendientes-postcurso.md        # decisiones diferidas al curso
└── README.md
```

---

## Cómo compilar el LaTeX

Requiere TeX Live (o MiKTeX) con `latexmk`, `biber`, y paquetes
`tikz`, `siunitx`, `biblatex`, `babel-spanish`.

```bash
cd docs/fase1-arquitectura-fisica
latexmk -pdf main.tex
```

Limpieza:

```bash
latexmk -C
```

## Cómo renderizar los diagramas mermaid

```bash
npm install -g @mermaid-js/mermaid-cli
mmdc -i diagramas/flujo-productivo.mmd   -o diagramas/flujo-productivo.png
mmdc -i diagramas/flujo-postcosecha.mmd  -o diagramas/flujo-postcosecha.png
```

GitHub renderiza los `.mmd` cuando se embeben en markdown.

---

## Parámetros editables (`params.tex`)

| Macro                       | Default | Significado                            |
|-----------------------------|---------|----------------------------------------|
| `\paramHmax`                | 180 cm  | Altura máxima disponible               |
| `\paramWmax`                | 90 cm   | Ancho máximo disponible                |
| `\paramDmax`                | 45 cm   | Fondo máximo disponible                |
| `\paramTambMin`             | 16 °C   | T ambiente mínima esperada             |
| `\paramTambMax`             | 26 °C   | T ambiente máxima esperada             |
| `\paramHRamb`               | 45 %    | HR ambiente típica                     |
| `\paramNiveles`             | 4       | Número de niveles del rack             |
| `\paramNcontenedores`       | 3       | Cámaras de fructificación              |
| `\paramVolTote`             | 55 L    | Volumen nominal de cada tote           |
| `\paramCargaUtilNivel`      | 50 kg   | Carga útil por nivel mínima            |
| `\paramVolOllaPresion`      | 23 L    | Capacidad olla de presión              |
| `\paramPresionEster`        | 15 psi  | Presión de esterilización              |
| `\paramTiempoEsterSustrato` | 90 min  | Tiempo esterilización sustrato         |
| `\paramTiempoEsterGrano`    | 60 min  | Tiempo esterilización grano            |

---

## Estado de cada sección

| Sección | Estado | Notas |
|---|---|---|
| §1.1 Rack | ✅ relleno | Carga calculada, geometría paramétrica, comparativa de materiales |
| §1.2 Contenedores | ✅ relleno | Patrón de perforación por especie, pasamuros tabulados |
| §1.3 Asignación especies | ⚠ tentativa | Tabla con literatura. Validar tras curso |
| §1.4 BOM | ⚠ placeholders | Sin precios inventados. Ver `cotizaciones_pendientes.md` |
| §1.5 Flujo productivo | ✅ relleno | Incluye etapas aguas arriba (§1.7) |
| §1.6 Post-cosecha | ⚠ parcial | Refs bibliográficas listas. Specs deshidratadora pendientes |
| §1.7 Preparación sustrato | ✅ relleno | **Nuevo:** olla presión, SAB, spawn, ensacado |

## Próximos pasos del operador

1. Revisar `pendientes-postcurso.md` y empezar a marcar lo que se resuelva tras el curso.
2. Empezar a cotizar lo de `cotizaciones_pendientes.md` (estructura del rack y olla de presión son los más urgentes).
3. Compilar `main.tex` localmente y validar que renderiza limpio.
4. Cuando estés listo: arrancamos Fase 2 (firmware ESP32) sin esperar a que esté todo cotizado/llegado.
