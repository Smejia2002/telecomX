# 📊 TelecomX - Análisis de Churn de Clientes

![Python](https://img.shields.io/badge/Python-3.13-blue)
![Pandas](https://img.shields.io/badge/Pandas-2.3.1-green)
![Matplotlib](https://img.shields.io/badge/Matplotlib-3.9.2-orange)
![Seaborn](https://img.shields.io/badge/Seaborn-0.13.2-red)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange)

## 🎯 Propósito del Análisis

Este proyecto realiza un **análisis integral de churn (evasión de clientes)** para la empresa de telecomunicaciones TelecomX. El objetivo principal es identificar los factores que influyen en la decisión de los clientes de cancelar sus servicios y desarrollar estrategias basadas en datos para mejorar la retención.

### Objetivos Específicos

- 🔍 **Identificar patrones** en el comportamiento de clientes que cancelan vs. los que permanecen
- 📈 **Analizar variables clave** como tenure, tipo de contrato, método de pago y servicios contratados
- 💰 **Evaluar la relación** entre gasto diario y propensión al churn
- 🎯 **Desarrollar recomendaciones estratégicas** para reducir la tasa de evasión
- 📊 **Crear visualizaciones** que faciliten la toma de decisiones empresariales

### Contexto del Problema

La **tasa de churn del 25.7%** identificada en TelecomX representa una pérdida significativa de ingresos recurrentes. Considerando que retener un cliente cuesta entre 5-10 veces menos que adquirir uno nuevo, este análisis proporciona insights críticos para optimizar las estrategias de retención.

## 📁 Estructura del Proyecto

```
telecomx/
├── 📄 README.md                       # Este archivo - Documentación del proyecto
├── 📊 INFORME_ANALISIS_TELECOMX.md   # Informe completo con conclusiones y recomendaciones
├── 📋 requirements.txt                # Dependencias de Python
├── 📂 data/
│   └── 🔢 TelecomX_Data.json         # Dataset original (7,267 registros)
└── 📂 notebooks/
    └── 🐍 telecom_x_latam.ipynb      # Notebook principal de análisis
```

### Descripción de Archivos

- **`telecom_x_latam.ipynb`**: Notebook principal con todo el análisis paso a paso
- **`TelecomX_Data.json`**: Dataset con información de 7,267 clientes de telecomunicaciones
- **`INFORME_ANALISIS_TELECOMX.md`**: Informe académico completo con insights y recomendaciones
- **`requirements.txt`**: Lista de todas las dependencias necesarias para ejecutar el proyecto

## 📈 Ejemplos de Gráficos e Insights Obtenidos

### 🔍 Hallazgos Principales

#### 1. **Distribución del Churn**
- ✅ **71.2% de clientes NO cancelan** (~5,174 clientes)
- ❌ **25.7% de clientes SÍ cancelan** (~1,869 clientes)
- ❓ **3.1% estado desconocido** (224 clientes)

#### 2. **Factor Más Crítico: Tenure (Permanencia)**
```
👥 Clientes que NO cancelan: Promedio de 37.6 meses
🚪 Clientes que SÍ cancelan: Promedio de 17.9 meses
📊 Diferencia: ~20 meses de permanencia
```

#### 3. **Insights Contraintuitivos**
- 💰 **El gasto diario NO predice el churn** (diferencia no significativa: ~$2.28 vs $2.29)
- 🌐 **Fibra óptica muestra mayor churn** que DSL (paradoja del servicio premium)
- 📄 **Contratos mes-a-mes tienen 3x más churn** que contratos de 2 años

### 📊 Visualizaciones Clave Incluidas

1. **Gráfico de Distribución de Churn**
   - Countplot mostrando la proporción de clientes por estado
   - Incluye números absolutos y porcentajes

2. **Análisis de Variables Categóricas**
   - Comparación por género, tipo de contrato, método de pago
   - Gráficos de barras agrupados con estadísticas

3. **Boxplots Comparativos**
   - Distribución de tenure y charges total por grupo de churn
   - Incluye estadísticas descriptivas superpuestas

4. **Análisis de Cuentas Diarias**
   - Boxplot, histogramas, violin plots y gráfico de barras
   - Comparación detallada entre grupos de churn

5. **Tabla de Estadísticas Descriptivas**
   - Resumen numérico de variables clave por grupo
   - Media, mediana, desviación estándar y conteos

### 🎯 Segmentación de Riesgo Identificada

#### 🔴 **Alto Riesgo de Churn**
- Tenure < 12 meses
- Contrato mes a mes
- Método de pago: Cheque electrónico
- Servicio de fibra óptica

#### 🟢 **Bajo Riesgo de Churn**
- Tenure > 36 meses
- Contratos de 1-2 años
- Débito automático
- Servicios DSL

## 🚀 Instrucciones para Ejecutar el Notebook

### Prerrequisitos

- **Python 3.13** o superior
- **Jupyter Notebook** o **VS Code** con extensión de Python
- **Git** (opcional, para clonar el repositorio)

### Opción 1: Instalación desde Cero

#### 1. **Clonar o Descargar el Proyecto**
```bash
# Si tienes git instalado
git clone https://github.com/Smejia2002/telecomX.git
cd telecomX

# O descarga el ZIP desde GitHub y extrae los archivos
```

#### 2. **Crear Entorno Virtual (Recomendado)**
```bash
# Con conda
conda create -n telecom python=3.13
conda activate telecom

# O con venv
python -m venv telecom
# Windows
telecom\Scripts\activate
# macOS/Linux
source telecom/bin/activate
```

#### 3. **Instalar Dependencias**
```bash
pip install -r requirements.txt
```

#### 4. **Lanzar Jupyter Notebook**
```bash
# Opción 1: Jupyter Notebook
jupyter notebook

# Opción 2: Jupyter Lab
jupyter lab

# Opción 3: VS Code
code .
```

### Opción 2: Ejecución Directa (Si ya tienes el entorno)

#### 1. **Navegar al Directorio**
```bash
cd c:\Users\skybl\Desktop\telecomx
```

#### 2. **Activar Entorno Virtual**
```bash
# Si usas conda
conda activate telecom

# Si usas venv (Windows)
telecom\Scripts\activate
```

#### 3. **Abrir el Notebook**
```bash
jupyter notebook notebooks/telecom_x_latam.ipynb
```

### 🔧 Dependencias Principales

```
pandas==2.3.1          # Manipulación de datos
numpy==2.3.1           # Operaciones numéricas
matplotlib==3.9.2      # Visualizaciones básicas
seaborn==0.13.2        # Visualizaciones estadísticas
jupyter>=1.0.0         # Entorno de notebook
ast                    # Procesamiento de JSON (built-in)
```

### 🏃‍♂️ Orden de Ejecución

1. **Ejecutar celdas secuencialmente** desde el inicio
2. **Sección de Extracción**: Carga y expansión de datos JSON
3. **Sección de Transformación**: Limpieza y preparación de datos
4. **Sección de Análisis**: Visualizaciones y análisis estadístico
5. **Informe Final**: Resumen de conclusiones y recomendaciones

### ⚠️ Notas Importantes

- **Tiempo de ejecución estimado**: 5-10 minutos
- **Memoria requerida**: ~500MB RAM
- **Dataset incluido**: No es necesario descargar datos adicionales
- **Jupyter Kernel**: Asegúrate de seleccionar el kernel del entorno virtual creado

### 🐛 Solución de Problemas Comunes

#### Problema: "ModuleNotFoundError"
```bash
# Solución: Instalar dependencias faltantes
pip install pandas numpy matplotlib seaborn
```

#### Problema: "FileNotFoundError" para el dataset
```bash
# Verificar que estés en el directorio correcto
pwd  # Linux/macOS
cd    # Windows

# El archivo debe estar en: data/TelecomX_Data.json
```

#### Problema: Kernel no conecta en Jupyter
```bash
# Instalar ipykernel en el entorno virtual
pip install ipykernel
python -m ipykernel install --user --name=telecom
```

## 📋 Resultados y Métricas Clave

### 🎯 **KPIs Principales Identificados**
- **Tasa de Churn Actual**: 25.7%
- **Objetivo Propuesto**: Reducir al 20%
- **ROI Esperado**: 305% con las recomendaciones implementadas
- **Clientes en Riesgo**: ~400 clientes identificados

### 💡 **Recomendaciones Estratégicas**
1. **Programa de Onboarding Intensivo** (0-12 meses)
2. **Migración a Contratos a Largo Plazo** (+15% descuento)
3. **Optimización del Servicio de Fibra Óptica**
4. **Incentivos para Débito Automático** (5% descuento)
5. **Sistema de Alertas Tempranas** (score de riesgo)

## 🤝 Contribuciones y Contacto

### 👨‍💻 Autor
**Samuel Mejia**
- 📧 Email: [Tu email aquí]
- 💼 LinkedIn: [Tu LinkedIn aquí]
- 🐙 GitHub: [@Smejia2002](https://github.com/Smejia2002)

### 🛠️ Tecnologías Utilizadas
- **Lenguaje**: Python 3.13
- **Análisis de Datos**: Pandas, NumPy
- **Visualización**: Matplotlib, Seaborn
- **Entorno**: Jupyter Notebook, VS Code
- **Control de Versiones**: Git, GitHub

### 📄 Licencia
Este proyecto está disponible bajo la licencia MIT. Ver el archivo `LICENSE` para más detalles.

### 🤝 Contribuir
¡Las contribuciones son bienvenidas! Si encuentras algún error o tienes sugerencias de mejora:

1. Haz fork del proyecto
2. Crea una rama para tu feature (`git checkout -b feature/AmazingFeature`)
3. Commit tus cambios (`git commit -m 'Add some AmazingFeature'`)
4. Push a la rama (`git push origin feature/AmazingFeature`)
5. Abre un Pull Request

---

## 📚 Referencias y Recursos Adicionales

- [Documentación de Pandas](https://pandas.pydata.org/docs/)
- [Guía de Seaborn](https://seaborn.pydata.org/tutorial.html)
- [Best Practices para Customer Churn Analysis](https://towardsdatascience.com/customer-churn-analysis-and-prediction-using-machine-learning-e5f9a3b9893e)
- [Jupyter Notebook Documentation](https://jupyter-notebook.readthedocs.io/)

---

⭐ **¡No olvides dar una estrella al proyecto si te resultó útil!** ⭐

*Última actualización: 5 de Agosto, 2025*
