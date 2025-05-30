# Análisis de Abandono de Clientes (Customer Churn)

## 📋 Descripción del Proyecto

Este proyecto implementa modelos de **Árbol de Decisión** y **Bosque Aleatorio (Random Forest)** para predecir el abandono de clientes en una empresa de telecomunicaciones. El objetivo es identificar los factores que influyen en la pérdida de clientes y evaluar la capacidad predictiva de ambos modelos.

## 📊 Dataset

- **Fuente**: Telecom Customer Churn (2023) - Kaggle IBM Dataset
- **Registros**: 7,032 clientes (después de limpieza)
- **Variables**: 20 características después del preprocesamiento
- **Variable objetivo**: Valor de abandono (0 = permanece, 1 = abandona)

## 🛠️ Metodología

### 1. Preprocesamiento de Datos
- Limpieza y eliminación de columnas irrelevantes
- Tratamiento de valores faltantes
- Conversión de tipos de datos
- Simplificación de variables categóricas ("No internet service" → "No")

### 2. Análisis Exploratorio
- Análisis de frecuencias y proporciones
- Identificación de desbalance de clases (73.42% permanecen, 26.58% abandonan)
- Visualización de patrones por tipo de contrato, servicio de internet y antigüedad

### 3. Balanceado de Datos
- Aplicación de **submuestreo (undersampling)** para equilibrar las clases
- Reducción de la clase mayoritaria a 2x la clase minoritaria

### 4. Codificación de Variables
- **One-Hot Encoding**: Variables categóricas nominales
- **Ordinal Encoding**: Variable "Contrato" (Month-to-month < One year < Two year)
- **Variables numéricas**: Conservadas sin transformación

### 5. Entrenamiento de Modelos

#### Árbol de Decisión
- `max_depth=3`
- `class_weight='balanced'`
- **Accuracy**: 77% (train y test)

#### Random Forest
- `n_estimators=40`
- `max_depth=5`
- `class_weight='balanced'`
- **Accuracy**: 78% (train), 76% (test)

## 📈 Resultados Principales

### Variables Más Importantes
1. **Contrato** (importancia: 0.65) - Factor más determinante
2. **Servicio de internet Fiber optic** (importancia: 0.18)
3. **Dependientes** (importancia: 0.12)

### Insights del Negocio
- Los clientes con contrato **mes a mes** tienen mayor tasa de abandono
- Clientes con **fibra óptica** muestran alta propensión al abandono
- **Clientes nuevos** (baja antigüedad) son más propensos a irse
- Clientes **sin dependientes** abandonan más frecuentemente

### Comparación de Modelos

| Métrica | Árbol de Decisión | Random Forest |
|---------|------------------|---------------|
| Accuracy | 77% | 76% |
| Recall (Abandonan) | 76% | 84% |
| Precision (Abandonan) | 63% | 59% |
| Falsos Negativos | 131 | 85 |

## 🎯 Conclusiones

- **Random Forest** es más eficiente para detectar clientes que abandonan (mayor recall)
- **Árbol de Decisión** es más simple e interpretable
- El **tipo de contrato** es el factor más crucial para predecir el abandono
- Para estrategias de retención, se recomienda enfocarse en:
  - Clientes con contratos mes a mes
  - Usuarios de fibra óptica
  - Clientes nuevos sin dependientes

## 🚀 Uso del Código

```python
# Cargar y ejecutar el notebook
# 1. Instalar dependencias
pip install pandas scikit-learn matplotlib seaborn

# 2. Cargar el dataset
df_churn = pd.read_excel("data_churn.xlsx")

# 3. Seguir los pasos del notebook para:
#    - Preprocesamiento
#    - Entrenamiento de modelos
#    - Evaluación y predicción
```

## 📁 Estructura del Proyecto

```
├── notebook-churn.ipynb    # Notebook principal con análisis completo
├── data_churn.xlsx        # Dataset de clientes
└── README.md             # Este archivo
```

## 🤝 Contribuciones

Este proyecto fue desarrollado como parte de un taller educativo sobre árboles de decisión y bosques aleatorios aplicados a problemas de abandono de clientes.
