# Diccionario de datos — `ventas_campana.csv`

Este archivo contiene datos crudos (sin procesar) de una campaña de marketing digital multicanal durante noviembre de 2024. **El archivo tiene errores intencionales** que deben identificar y corregir como parte del ejercicio.

| Columna | Descripción | Tipo esperado |
|---|---|---|
| `fecha` | Fecha en la que se registraron las métricas | Fecha (⚠️ el formato varía entre filas, hay que estandarizarlo) |
| `canal` | Plataforma donde corrió el anuncio (Facebook, Instagram, Google Ads, TikTok) | Texto |
| `campana` | Nombre de la campaña asociada | Texto |
| `impresiones` | Número de veces que el anuncio fue mostrado | Numérico |
| `clics` | Número de clics recibidos | Numérico |
| `clicks` | ⚠️ Columna duplicada de `clics` (mismo dato, nombre en inglés). Deben decidir cuál conservar y eliminar la redundante. | Numérico |
| `conversiones` | Número de conversiones (ventas o leads) generadas | Numérico |
| `costo` | Costo total invertido en esa fila, en pesos colombianos (COP) | Numérico |

## Problemas conocidos que deben resolver

1. **Formatos de fecha inconsistentes**: algunas filas usan `YYYY-MM-DD` y otras `DD/MM/YYYY` o `DD-MM-YYYY`. Deben estandarizar a un solo formato.
2. **Valores nulos/vacíos**: hay celdas vacías en `impresiones`, `clics`, y `conversiones`. Deben decidir cómo tratarlos (¿eliminar la fila?, ¿interpolar?, ¿marcar como dato faltante?) y **documentar su decisión** en el reporte.
3. **Columna duplicada**: `clics` y `clicks` contienen la misma información. Deben quedarse con una sola.
4. **Outlier / dato atípico**: hay al menos una fila con un valor de clics anormalmente alto respecto a sus impresiones (un CTR imposible, ej: por encima del 40-50%). Deben detectarlo, señalarlo en el reporte, y decidir si lo corrigen o lo excluyen del análisis (con justificación).

## KPIs que deben calcular a partir de los datos ya limpios

- **CTR** (Click Through Rate) = clics / impresiones
- **CPA** (Costo por Adquisición) = costo / conversiones
- **Tasa de conversión** = conversiones / clics
- **CPC** (Costo por Clic) = costo / clics
- Desempeño agregado **por canal** y **por campaña**
