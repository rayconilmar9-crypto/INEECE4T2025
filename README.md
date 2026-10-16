# Informe interactivo – Encuesta Continua de Empleo (ECE) 4T2025, Bolivia

Análisis estadístico de la ECE del cuarto trimestre de 2025 (INE Bolivia). El proyecto convierte los microdatos del Excel en un CSV limpio y lo presenta en un informe HTML interactivo que funciona en el navegador, sin Python ni servidor.

## Contenido

| Archivo | Descripción |
|---|---|
| `ECE_4T2025.xlsx` | Microdatos originales del INE (52.650 personas, 121 variables). |
| `generar_csv.py` | Script de Python que lee el Excel, decodifica las categorías y genera el CSV. |
| `df_ece.csv` | Datos limpios: población en edad de trabajar (14 años o más), 38.596 filas y 15 columnas. |
| `informe_ece.html` | Informe interactivo: arrastrar y soltar el CSV, gráficos, pruebas estadísticas e interpretación. |
| `papaparse.min.js`, `plotly.min.js` | (Opcional) Copias locales de las librerías para usar el informe sin internet. |

## Cómo usar el informe (no requiere Python)

1. Coloca `informe_ece.html` y `df_ece.csv` en la misma carpeta.
2. Abre `informe_ece.html` con doble clic (Chrome o Edge recomendados).
3. Arrastra `df_ece.csv` al recuadro de la página, o haz clic en él para elegir el archivo.
4. El informe se genera en pantalla.

El HTML carga PapaParse (lectura del CSV) y Plotly.js (gráficos). Si no hay internet, descarga `papaparse.min.js` y `plotly.min.js` y guárdalos junto al HTML.

## Cómo regenerar el CSV (requiere Python)

1. Instala Python 3 y las librerías: `pip install pandas openpyxl`
2. Coloca `generar_csv.py` y `ECE_4T2025.xlsx` en la misma carpeta.
3. Ejecuta: `python generar_csv.py ECE_4T2025.xlsx`
4. Se crea `df_ece.csv` (tarda 1–2 minutos por el tamaño del Excel).

## Qué incluye el informe

- **Descriptivos:** estadística cuantitativa (media, desviación, cuartiles) y tablas de frecuencia de las variables categóricas.
- **Distribuciones:** barras (área, sexo, departamento, nivel educativo, grupo ocupacional, actividad, subocupación, tipo de hogar) e histogramas (edad, años de estudio, horas de trabajo, ingresos).
- **Ingreso por grupos:** diagramas de caja y gráficos de media y mediana por área, departamento, nivel educativo, sexo y tramo de edad; sexo por área apilado.
- **Relaciones:** mapas de densidad 2D (ingreso vs. años de estudio, edad y horas) y matriz de correlaciones.
- **Pruebas de hipótesis (α = 0,05):** t de Student (Welch), chi-cuadrado, ANOVA y correlación de Pearson, cada una con su interpretación y tamaño del efecto.

## Columnas del CSV

| Columna | Variable original (INE) | Significado |
|---|---|---|
| `departamento` | depto | Departamento de residencia |
| `area` | area | Urbana / Rural |
| `sexo` | s1_02 | Hombre / Mujer |
| `edad` | s1_03a | Edad en años |
| `anios_estudio` | aestudio | Años de estudio aprobados |
| `nivel_educativo` | niv_ed | Mayor nivel educativo cursado |
| `condicion_actividad` | condact | Ocupado / Desocupado / Inactivo |
| `grupo_ocupacional` | cob_op | Grupo de ocupación del empleo principal |
| `actividad` | caeb_op | Rama de actividad económica (CAEB, secciones A–U) |
| `subocupacion` | psubocup | Subocupado / No subocupado |
| `tipo_hogar` | tipohogar | Tipología del hogar (códigos 1–7) |
| `horas_trabajo_total` | tothrs | Horas semanales trabajadas |
| `ingreso_laboral` | ylab | Ingreso laboral mensual (Bs) |
| `ingreso_oc_principal` | yprilab | Ingreso mensual de la ocupación principal (Bs) |
| `factor_expansion` | fact_trim_act | Ponderador del INE (no usado en el informe) |

## Limitaciones

- Los resultados son **sin ponderar**: describen la muestra, no se extrapolan a toda Bolivia. Para eso habría que usar `factor_expansion`.
- `ingreso_laboral` e `ingreso_oc_principal` son prácticamente idénticos en esta base.
- Las etiquetas de `tipo_hogar` son códigos del INE (no verificados con el diccionario) y no se interpretan.
- Con muestras grandes casi toda diferencia resulta significativa: conviene leer siempre el tamaño del efecto.
- La correlación no implica causalidad.
- Plotly no ofrece hexbin nativo; se usa un mapa de densidad 2D equivalente.

## Fuente

Instituto Nacional de Estadística (INE) de Bolivia, Encuesta Continua de Empleo, trimestre IV de 2025. Microdatos disponibles en el catálogo ANDA del INE.

## Autoría

Nombre del autor/a: ______  
Fecha: ______

