# CASO 1 — Agente de terminal

Ejercicio de **Inteligencia de Negocios**: construir un dashboard interactivo con OpenCode + MCP.

## Contexto

Eres consultor de inteligencia de negocios. Un cliente te entrega datos crudos de una campaña de marketing digital multicanal. Tu trabajo es usar **OpenCode**, conectado a un **modelo de IA** y a servidores **MCP**, para limpiar los datos, calcular KPIs, investigar un benchmark externo, y construir un **dashboard interactivo** que el cliente pueda consultar en su navegador.

## Estructura del repositorio

```
bi-ejercicio-opencode/
├── README.md                        # este archivo
├── data/
│   ├── ventas_campana.csv           # datos crudos con errores intencionales
│   └── diccionario_datos.md         # descripción de las columnas y problemas conocidos
├── config/
│   └── opencode.json.example        # config de ejemplo lista para usar
└── entregable/                      # aquí va tu resultado final (ver Paso 5)
```

## Requisitos previos

- Cuenta de GitHub (gratuita)
- OpenCode instalado (visto en clase)
- Acceso a un modelo de IA configurado en OpenCode

---

## Guía de trabajo

### Paso 1 — Clonar este repositorio

```bash
git clone https://github.com/daververa/CASO-1-AGENTE-DE-TERMINAL.git
cd CASO-1-AGENTE-DE-TERMINAL
```

### Paso 2 — Configurar OpenCode

Copia `config/opencode.json.example` a `opencode.json` en la raíz del proyecto y ajusta el modelo según tu configuración (visto en clase). Este archivo ya trae declarados los dos servidores MCP que vas a necesitar en el siguiente paso.

### Paso 3 — Conectar mínimo 2 servidores MCP

Puedes pedirle a OpenCode (la IA) que instale y configure los MCP por ti, copiando y pegando esto en el chat:

> *"Instala y configura los siguientes MCP servers en opencode.json:*
> 1. *`filesystem` tipo local, con el comando `npx -y @modelcontextprotocol/server-filesystem ./data`, para leer los archivos de este proyecto.*
> 2. *`web-fetch` tipo remote en la URL `https://fetch.mcp.a-sh.work`, para buscar datos en internet."*
>
> *Luego verifica que ambos MCP estén conectados y funcionando.*

Los nombres de los servidores MCP que vas a necesitar son:

1. **`filesystem`** — `@modelcontextprotocol/server-filesystem`
   MCP de **filesystem**, para que el modelo pueda leer directamente `data/ventas_campana.csv` sin que tú se lo pegues manualmente en el chat.
2. **`web-fetch`** — servidor **fetch/MCP de acceso a web**, para investigar un dato externo real: busca cuál es el CTR promedio de la industria en redes sociales o Google Ads para un sector similar al de la campaña (puedes elegir el sector, ej. retail, moda, restaurantes).

> Si algo falla, revisa el archivo `config/opencode.json.example` de este repositorio, que ya viene con ambos servidores declarados.

### Paso 4 — Limpiar los datos y calcular KPIs (usando OpenCode)

Usando OpenCode (con el modelo y los MCP ya conectados), pide que:

1. Lea el CSV crudo desde el MCP de filesystem.
2. Detecte y corrija los problemas descritos en `data/diccionario_datos.md` (fechas inconsistentes, valores nulos, columna duplicada, outlier).
3. Calcule los KPIs por fila y agregados por canal y campaña: **CTR, CPA, tasa de conversión, CPC**.
4. Genere un archivo `entregable/data/kpis.json` con los datos ya limpios y los KPIs calculados, listo para ser consumido por JavaScript.

> **Documenta en tu reporte** qué decisiones tomaste sobre los datos faltantes y el outlier (por qué los trataste así), y qué problemas encontraste en los datos crudos.

### Paso 5 — Construir el dashboard interactivo (HTML + CSS + JS)

Dentro de `entregable/`, construye un sitio estático (para publicar en **GitHub Pages**) que muestre el análisis. Puedes pedirle ayuda a OpenCode para generarlo, pero debes entender y poder explicar el código.

**Obligatorio:**

- Cargar `kpis.json` con `fetch()`
- Tarjetas con los KPIs principales (CTR, CPA, tasa de conversión, CPC)
- Al menos **1 gráfico interactivo** (puedes usar una librería vía CDN, por ejemplo Chart.js)
- Un filtro interactivo (por canal o por campaña) que actualice el gráfico

**A elección (suma puntos extra):**

- Comparación visual contra el benchmark externo que investigaste con el MCP web
- Modo oscuro / claro
- Tabla con los datos, ordenable o con buscador
- Selector para cambiar entre métricas (CTR vs CPA vs conversión)
- Cualquier otra interactividad que consideres útil para el cliente

**Estructura esperada dentro de `entregable/`:**

```
entregable/
├── index.html
├── style.css
├── script.js
├── data/
│   └── kpis.json
└── reporte.md          # ver Paso 6
```

### Paso 6 — Reporte de conclusiones (`entregable/reporte.md`)

Debe incluir:

- Qué problemas encontraste en los datos y cómo los corregiste
- Los KPIs principales y qué canal/campaña tuvo mejor desempeño
- Comparación con el benchmark externo investigado
- 3 recomendaciones accionables para el cliente

### Paso 7 — Publicar y entregar

1. Sube todo (código, datos limpios, reporte) a un **repositorio público propio** en tu cuenta de GitHub.
2. Activa **GitHub Pages** apuntando a la carpeta `entregable/` (o a la rama que uses).
3. Envíame:
   - El link del repositorio
   - El link del sitio publicado en GitHub Pages

---

## Rúbrica de evaluación

| Criterio | Peso |
|---|---|
| Configuración correcta de OpenCode y el modelo | 10% |
| Uso de mínimo 2 MCP distintos (filesystem + web) | 20% |
| Limpieza de datos y cálculo correcto de KPIs | 20% |
| Dashboard funcional y publicado en GitHub Pages (obligatorios cumplidos) | 25% |
| Interactividad extra / creatividad | 15% |
| Recomendaciones fundamentadas con benchmark externo | 10% |

**Importante:** el objetivo no es solo que el dashboard se vea bien, sino que se note que usaron OpenCode con modelo y MCP como parte real del flujo de trabajo, no que hicieron todo manualmente y solo instalaron la herramienta sin usarla.