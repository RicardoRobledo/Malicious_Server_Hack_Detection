# 🛡️ Predicción de Hackeos Maliciosos en Servidores

## 📋 Descripción del Proyecto

Este proyecto desarrolla un modelo predictivo para identificar patrones que indiquen la probabilidad de hackeos maliciosos en servidores. Con el aumento exponencial de los pagos digitales a nivel global, los ataques cibernéticos se han vuelto cada vez más frecuentes, donde los hackers pueden comprometer datos utilizando únicamente números telefónicos vinculados a cuentas bancarias.

**Objetivo:** Construir un sistema de detección temprana que permita a los equipos de ciberseguridad prevenir ataques antes de que ocurran.

## 🎯 Variable Objetivo

- **`MALICIOUS_OFFENSE`**: Indica si un servidor será víctima de un hackeo malicioso

## 🗂️ Dataset

- **Fuente:** [Malicious Server Hack Dataset](https://www.kaggle.com/datasets/lplenka/malicious-server-hack)
- **Descarga automática:** Utilizando `kagglehub` para reproducibilidad
- **Variables:** Conjunto de características anónimas que permiten la predicción

## 🔧 Metodología y Pipeline

### 1. Preprocesamiento de Datos
- **Imputación de valores faltantes:** `SimpleImputer` (mediana para numéricas, moda para categóricas)
- **Escalado de variables numéricas:** `StandardScaler`
- **Codificación de categóricas:** `OneHotEncoder` con manejo de categorías desconocidas
- **Arquitectura modular:** `ColumnTransformer` para procesamiento paralelo

### 2. Balanceo de Clases
Evaluación exhaustiva de técnicas de balanceo:

**Técnicas de Submuestreo:**
- TomekLinks
- EditedNearestNeighbours (ENN)
- RepeatedEditedNearestNeighbours (RENN)
- OneSidedSelection (OSS)
- NeighbourhoodCleaningRule (NCR)

**Técnicas de Sobremuestreo:**
- RandomOverSampler
- **SMOTE** (Synthetic Minority Oversampling Technique)
- BorderlineSMOTE
- **ADASYN** (Adaptive Synthetic Sampling)

### 3. Modelos Evaluados
- **Logistic Regression (LR)**
- **Linear Discriminant Analysis (LDA)**
- **Random Forest (RF)**
- **Gradient Boosting (GB)** ⭐ *Mejor rendimiento*
- **Support Vector Classifier (SVC)**
- **Gaussian Naive Bayes (NB)**

### 4. Calibración de Probabilidades
- **CalibratedClassifierCV** con método isotónico para obtener probabilidades bien calibradas

## 📊 Resultados Principales

### Rendimiento por Modelo (G-Media):
| Modelo | Media | Desv. Estándar |
|--------|-------|----------------|
| Gradient Boosting | **0.989** | 0.003 |
| Random Forest | 0.928 | 0.015 |
| SVC | 0.730 | 0.017 |
| LDA | 0.583 | 0.016 |
| Logistic Regression | 0.546 | 0.009 |
| Naive Bayes | 0.559 | 0.014 |

### Rendimiento por Técnica de Balanceo:
| Técnica | G-Media | Desv. Estándar |
|---------|---------|----------------|
| **RandomOverSampler** | **0.995** | 0.002 |
| SMOTE | 0.994 | 0.003 |
| BorderlineSMOTE | 0.994 | 0.003 |
| ADASYN | 0.994 | 0.003 |
| RENN | 0.992 | 0.003 |

### Modelo Final: Gradient Boosting + ADASYN + Calibración
- **Distribución de predicciones en conjunto de prueba:**
  - Clase 0 (No hackeo): 8,004 instancias (33.55%)
  - Clase 1 (Hackeo): 7,899 instancias (33.11%)

## 🛠️ Tecnologías y Librerías

```python
# Core ML
scikit-learn
imbalanced-learn
numpy
pandas

# Modelos específicos
RandomForestClassifier
GradientBoostingClassifier
SVM, Logistic Regression, etc.

# Balanceo de clases
SMOTE, ADASYN, TomekLinks, etc.

# Evaluación
RepeatedStratifiedKFold
geometric_mean_score
CalibratedClassifierCV
```

## 🎯 Métricas de Evaluación

- **Métrica principal:** G-Media (Geometric Mean Score)
- **Justificación:** Ideal para problemas de clasificación con clases desbalanceadas
- **Validación:** Validación cruzada estratificada repetida (5 folds, 3 repeticiones)
- **Robustez:** Análisis de estabilidad a través de múltiples ejecuciones

## 📈 Conclusiones Clave

1. **Gradient Boosting** demostró ser el modelo más efectivo para este problema
2. Las técnicas de **sobremuestreo** superaron consistentemente a las de submuestreo
3. **RandomOverSampler** alcanzó el mejor rendimiento (G-Media: 0.995)
4. La **calibración de probabilidades** mejora la confiabilidad de las predicciones
5. El pipeline es robusto y generalizable para datos de producción

## 🔮 Aplicaciones Prácticas

- **Detección preventiva** de intentos de hackeo
- **Alertas tempranas** para equipos de ciberseguridad
- **Monitoreo continuo** de la seguridad de servidores
- **Optimización de recursos** de seguridad basada en riesgo

## 📝 Notas Técnicas

- Pipeline completamente automatizado con `ColumnTransformer` e `imblearn.Pipeline`
- Manejo robusto de datos categóricos y numéricos
- Evaluación comparativa exhaustiva de técnicas de balanceo
- Código modular y reutilizable para diferentes conjuntos de datos

---

*Este proyecto forma parte de un sistema integral de ciberseguridad predictiva, diseñado para anticipar y prevenir ataques maliciosos en infraestructuras críticas.*
