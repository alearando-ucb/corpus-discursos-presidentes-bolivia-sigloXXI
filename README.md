# Corpus de discursos de asunción presidencial de Bolivia (siglo XXI)

Corpus con los discursos de asunción al cargo de distintos presidentes de Bolivia
del siglo XXI, en texto completo, pensado para análisis de discurso y procesamiento
de lenguaje natural (PLN).

## Contenido

| Presidente | Año | Tipo de asunción | Archivo |
|---|---|---|---|
| Carlos Mesa | 2003 | Sucesión constitucional | `textos/2003_mesa.txt` |
| Eduardo Rodríguez Veltzé | 2005 | Sucesión constitucional | `textos/2005_rodriguez_veltze.txt` |
| Evo Morales | 2006 | Elección directa | `textos/2006_morales.txt` |
| Luis Arce | 2020 | Elección directa | `textos/2020_arce.txt` |
| Rodrigo Paz | 2025 | Elección directa | `textos/2025_paz.txt` |

La fuente de cada discurso, están en [`catalog.json`](./catalog.json).

No se incluyen los discursos de asunción de Jorge Quiroga(2001), Gonzalo Sánchez de Lozada (2002), ni las reelecciones de Evo Morales(2010 y 2015), porque no se logró encontrar el discurso intégro en fuentes en línea.
Lamentablemente Bolivia no cuenta con un archivo oficial centralizado en línea de discursos presidenciales, es posible que existan registros físicos de los discursos en archivos como el de la Asamblea Legislativa Plurinacional, pero al no estar el archivo en línea su consulta fue imposible.

## Estructura del repositorio

```
.
├── README.md
├── LICENSE
├── catalog.json      # metadatos: presidente, año, tipo de asunción, archivo, fuente
└── textos/            # texto completo de cada discurso, uno por archivo .txt
```

## Cómo usar el corpus en Python / Google Colab

```python
import json, requests
import pandas as pd

BASE = "https://raw.githubusercontent.com/alearando-ucb/corpus-discursos-presidentes-bolivia-sigloXXI/main"

catalog = requests.get(f"{BASE}/catalog.json").json()

for doc in catalog:
    doc["texto"] = requests.get(f"{BASE}/textos/{doc['archivo']}").text

df = pd.DataFrame(catalog)

```
Esto permite armar un dataframe con cada discurso cargado a texto completo por fila.

