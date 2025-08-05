# 📊 INFORME DE ANÁLISIS Y LIMPIEZA DE DATOS - TelecomX

**Proyecto:** Análisis de Churn de Clientes TelecomX  
**Fecha:** 4 de Agosto, 2025  
**Analista:** Samuel  
**Entorno:** Python 3.13, Jupyter Lab, Windows

---

## 📋 RESUMEN EJECUTIVO

Este informe documenta el proceso completo de extracción, transformación y limpieza de datos del dataset TelecomX, enfocado en el análisis de churn de clientes. Se identificaron y resolvieron múltiples inconsistencias en los datos, preparándolos para análisis posteriores.

### 🎯 Objetivos Principales
- Extraer y estructurar datos anidados del archivo JSON
- Identificar y corregir inconsistencias en los datos
- Preparar el dataset para análisis de churn
- Documentar el proceso de limpieza para reproducibilidad

---

## 📁 ESTRUCTURA DEL PROYECTO

```
telecomx/
├── data/
│   └── TelecomX_Data.json          # Dataset original
├── notebooks/
│   └── telecom_x_latam.ipynb       # Notebook principal de análisis
├── requirements.txt                # Dependencias del proyecto
└── INFORME_ANALISIS_TELECOMX.md   # Este informe
```

---

## 🔧 ENTORNO TÉCNICO

### Librerías Principales Utilizadas
- **pandas 2.3.1** - Manipulación y análisis de datos
- **numpy 2.3.1** - Operaciones numéricas
- **ast** - Evaluación segura de strings a diccionarios
- **json** - Procesamiento de datos JSON

### Configuración del Entorno
- **Entorno virtual:** `telecom` (conda)
- **Python:** 3.13
- **Jupyter Lab:** 4.4.4
- **Sistema Operativo:** Windows

---

## 📊 ANÁLISIS INICIAL DEL DATASET

### Características del Dataset Original
- **Archivo fuente:** `TelecomX_Data.json`
- **Total de registros:** 7,267 clientes
- **Estructura inicial:** Datos anidados en formato JSON

### Columnas Anidadas Identificadas
El dataset contenía 4 columnas con estructuras JSON anidadas:
1. `customer` - Información demográfica del cliente
2. `phone` - Servicios telefónicos
3. `internet` - Servicios de internet
4. `account` - Información de facturación y contrato

---

## 🔄 PROCESO DE EXTRACCIÓN Y TRANSFORMACIÓN

### 1. Expansión de Columnas Anidadas

**Problema:** Los datos estaban almacenados como strings JSON dentro de columnas.

**Solución:** Implementación de la función `expandir_columns()`:

```python
def expandir_columns(df, column_name):
    # Convertir strings a dictionaries
    df[column_name] = df[column_name].apply(
        lambda x: ast.literal_eval(x) if isinstance(x, str) else x
    )
    
    # Expandir el column_name en múltiples columnas 
    columns_expanded = pd.json_normalize(df[column_name])
    
    # Usar directamente los nombres de las claves sin prefijo
    # Eliminar la columna original y concatenar las nuevas
    df.drop(column_name, axis=1, inplace=True)
    df[columns_expanded.columns] = columns_expanded
```

**Resultado:** 
- Dataset expandido de 4 a 21 columnas
- Estructura tabular estándar para análisis

### 2. Conversión de Tipos de Datos

**Columnas Numéricas Identificadas:**
- `SeniorCitizen`: Convertido a `int64`
- `tenure`: Convertido a `int64`

---

## 🚨 IDENTIFICACIÓN Y RESOLUCIÓN DE INCONSISTENCIAS

### 1. Problema en la Columna `Churn`

**Inconsistencia Detectada:**
- 224 registros con valores vacíos (`''`)
- Imposibilidad de determinar el estado real de churn

**Investigación Realizada:**
Se analizaron los clientes con Churn vacío usando tres criterios:
1. **Tenure > 0:** Evidencia de historial como cliente
2. **Charges.Total > 0:** Evidencia de consumo de servicios
3. **Servicios Activos:** Evidencia de servicios contratados

**Decisión Tomada:**
```python
df['Churn'] = df['Churn'].replace('', 'Desconocido')
df['Churn'] = df['Churn'].str.strip()
```

**Justificación:** Clasificar como 'Desconocido' mantiene la integridad de los datos sin hacer suposiciones incorrectas.

### 2. Problema en la Columna `Charges.Total`

**Inconsistencia Detectada:**
- 11 registros con espacios en blanco (`' '`)
- Error al intentar conversión a tipo numérico

**Solución Implementada:**
```python
df['Charges.Total'] = df['Charges.Total'].replace(' ', np.nan)
df['Charges.Total'] = df['Charges.Total'].astype(np.float64)
df['Charges.Total'] = df['Charges.Total'].fillna(0.0)
```

**Resultado:**
- Conversión exitosa a `float64`
- 7,256 valores válidos de 7,267 registros
- 11 valores faltantes tratados como 0.0

### 3. Conversión de Variables Categóricas a Binarias

**Objetivo:** Preparar variables categóricas para análisis numérico.

**Variables Procesadas:**
- Partner, Dependents, PhoneService
- MultipleLines, OnlineSecurity, OnlineBackup
- DeviceProtection, TechSupport, StreamingTV
- StreamingMovies, PaperlessBilling

**Función de Conversión:**
```python
def binamizar(valor):
    if valor == 'Yes':
        return 1
    elif valor == 'No':
        return 0
    elif valor in ['No phone service', 'No internet service']:
        return 0
    else:
        return valor
```

**Lógica Aplicada:**
- `'Yes'` → `1`
- `'No'` → `0`
- `'No phone service'` / `'No internet service'` → `0`

---

## 📈 ESTADO FINAL DEL DATASET

### Distribución de Churn
| Estado | Cantidad | Porcentaje |
|--------|----------|------------|
| No | ~5,174 | ~71.2% |
| Yes | ~1,869 | ~25.7% |
| Desconocido | 224 | ~3.1% |

### Columnas Numéricas Finales
- **SeniorCitizen:** int64
- **tenure:** int64  
- **Charges.Total:** float64
- **Variables binarias:** int64 (0/1)

### Calidad de Datos
- ✅ **Sin valores faltantes críticos**
- ✅ **Tipos de datos consistentes**
- ✅ **Estructura tabular estándar**
- ✅ **21 columnas bien definidas**

---

## 🔍 HALLAZGOS PRINCIPALES

### 1. Problemas de Calidad de Datos
- **3.1%** de registros con estado de Churn desconocido
- **0.15%** de registros con problemas en facturación
- Datos anidados requirieron procesamiento especializado

### 2. Preparación para Análisis
- Dataset completamente limpio y estructurado
- Variables categóricas convertidas a formato numérico
- Listo para algoritmos de machine learning

### 3. Documentación del Proceso
- Proceso completamente reproducible
- Decisiones documentadas y justificadas
- Código reutilizable para datasets similares

---

## 🛠️ HERRAMIENTAS Y METODOLOGÍA

### Control de Versiones
- **Git** configurado para el proyecto
- Commits documentados del proceso de limpieza
- Configuración: `core.autocrlf = true` para Windows

### Jupyter Notebook
- Análisis interactivo paso a paso
- Visualización inmediata de resultados
- Documentación inline del proceso

### Buenas Prácticas Aplicadas
- ✅ Análisis exploratorio antes de transformaciones
- ✅ Validación de cada paso de limpieza
- ✅ Preservación de datos originales
- ✅ Documentación de decisiones críticas

---

## 🎯 RECOMENDACIONES FUTURAS

### 1. Análisis Adicionales Sugeridos
- **Análisis de correlación** entre variables
- **Segmentación de clientes** por características
- **Modelo predictivo** de churn
- **Análisis temporal** si hay datos de fechas

### 2. Mejoras en el Pipeline de Datos
- Automatización del proceso de limpieza
- Validación automática de calidad de datos
- Pipeline de transformación escalable

### 3. Monitoreo de Calidad
- Implementar checks automáticos de inconsistencias
- Alertas para nuevos patrones de datos faltantes
- Dashboard de calidad de datos

---

## 📝 CONCLUSIONES

El proceso de limpieza y preparación de datos del dataset TelecomX se completó exitosamente. Se identificaron y resolvieron inconsistencias críticas que habrían impactado negativamente cualquier análisis posterior.

### Logros Principales:
1. ✅ **Extracción exitosa** de datos anidados complejos
2. ✅ **Resolución inteligente** de datos faltantes
3. ✅ **Conversión adecuada** de tipos de datos
4. ✅ **Preparación completa** para análisis avanzados
5. ✅ **Documentación exhaustiva** del proceso

### Impacto en el Proyecto:
- **Reducción significativa** del riesgo de errores en análisis posteriores
- **Mejora en la confiabilidad** de resultados futuros
- **Base sólida** para modelos de machine learning
- **Proceso reproducible** para datasets similares

El dataset está ahora **listo para análisis avanzados** de churn de clientes y implementación de modelos predictivos.

---

## 📧 CONTACTO

**Analista:** Samuel  
**Fecha de Finalización:** 4 de Agosto, 2025  
**Proyecto:** TelecomX Data Analysis  

---

*Este informe fue generado como parte del proceso de análisis de datos del proyecto TelecomX. Todos los códigos y metodologías están disponibles en el notebook correspondiente.*
