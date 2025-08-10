
# 🎯 Desafío Telecom X (parte 2)

<p align="center">
  <img src="https://drive.google.com/uc?export=view&id=1l5Ux2MaZCnJ7gHQSGb_vhqE_KR66PGio" 
       alt="Imagen de portada" 
       width="600" />
</p>

**Autor:** Miguel Ángel Toro Romo  
**Fecha:** 8-ago-2025  

---

## 📝 Descripción del Desafío

Este proyecto tiene como objetivo construir un modelo de clasificación que prediga si un cliente abandonará o no los servicios de la compañía, a partir de sus características sociodemográficas y de uso de servicios.

La empresa quiere anticiparse al problema de la cancelación, y debemos construir un pipeline robusto para esta etapa inicial de modelado.


---

### 🔍 Análisis de Problema.

🔷 Este es un problema de **clasificación binaria**.

🔷 Variable objetivo binaria (Churn = 1 o 0): ¿El cliente se irá o no?

🔷 Modelos recomendados: **Modelos de clasificación**.

🔷 Probaremos:

 *   DecisionTreeClassifier
 *   RandomForestClassifier
 *   CatBoost

 ---

## 📝 Tareas del Desafío

✅ Preparar los datos para el modelado (tratamiento, codificación, normalización).


✅ Realizar análisis de correlación y selección de variables.


✅ Entrenar dos o más modelos de clasificación.


✅ Evaluar el rendimiento de los modelos con métricas.


✅ Interpretar los resultados, incluyendo la importancia de las variables.


✅ Crear una conclusión estratégica señalando los principales factores que influyen en la cancelación.

---



## ⚙️ Tecnologías Utilizadas

- Python 3.11.13 - Lenguaje principal
- pandas 2.2.2, numpy 2.0.2- Manipulación de datos
- scikit-learn 1.6.1 - Machine Learning
- Statsmodels 0.14.5 - Machine Learning
- ImbLearn 0.13.0 - Machine Learning
- Scipy 1.16.1 - Machine Learning
- matplotlib 3.10.0, seaborn 0.13.2 - Visualización
- Google Colab - Entorno de ejecución

---

## 🔍 Análisis preliminar de la información

✅ Disponemos de un conjunto de 7043 registros con información de clientes

✅ Cada registro tiene las siguientes columnas:
```
'customerID',
'Churn',
'gender',
'SeniorCitizen',
'Partner',
'Dependents',
'tenure',
'PhoneService',
'MultipleLines',
'InternetService',
'OnlineSecurity',
'OnlineBackup',
'DeviceProtection',
'TechSupport',
'StreamingTV',
'StreamingMovies',
'Contract',
'PaperlessBilling',
'PaymentMethod',
'Charges.Monthly',
'Charges.Total'
```
### ✅ Estos registros tienen la siguiente distribución de Churn:

<p align="center">
  <img src="https://drive.google.com/uc?export=view&id=1zibE0FeRSsXAllv2Q1LaKqPiueGni8z_" 
       alt="Distribución de Churn" 
       width="700" />
</p>


### ✅ Es un conjunto de datos muy desbalanceado en sus categorías de la variable objetivo Churn


### 📈 Variables Categóricas iniciales

- `gender: 'Female', 'Male'`
- `Partner: 'Yes', 'No'`
- `Dependents: 'Yes', 'No'`
- `PhoneService: 'Yes', 'No'`
- `MultipleLines: 'No', 'Yes', 'No phone service'`
- `InternetService: 'DSL', 'Fiber optic', 'No'`
- `OnlineSecurity: 'No', 'Yes', 'No internet service'`
- `OnlineBackup: 'Yes', 'No', 'No internet service'`
- `DeviceProtection: 'No', 'Yes', 'No internet service'`
- `TechSupport: 'Yes', 'No', 'No internet service'`
- `StreamingTV: 'Yes', 'No', 'No internet service'`
- `Streaming Movies: 'No', 'Yes', 'No internet service'`
- `Contract: 'One year' 'Month-to-month', 'Two year'`
- `PaperlessBilling: 'Yes', 'No'`
- `PaymentMethod: 'Mailed check', 'Electronic check', 'Credit card (automatic)',  'Bank transfer (automatic)'`

### 📈 Variables Numéricas iniciales

- `Charges.Monthly: valores decimales mayores que cero`
- `Charges.Total: valores decimales mayores que cero'`
---

## 🧪 Evaluación de Modelos

🔷 Modelos evaluados:

 - `RandomForestClassifier`
 - `DecisionTreeClassifier`
 - `CatBoost`

🔷 Se construyó un pipeline completo para cada modelo que incluyen:

 - Eliminación de columnas irrelevantes (`customerID`, `tenure`, `Charges.Monthly`)
 - Codificación categórica con `OneHotEncoder` 
- Balanceo de clases con `class_weight='balanced` para `RandomForestClassifier` y `SMOTE` para `DecisionTreeClassifier`
- Validación cruzada (`StratifiedKFold`)

---

### 🔢 Métricas claves

|Modelo|Accuracy|Precision\_Clase\_1|Recall\_Clase\_1|F1-Score\_Clase\_1|
|---|---|---|---|---|
|DecisionTree|72\.69%|49\.12%|79\.68%|60\.77%|
|CatBoost|75\.44%|52\.43%|80\.75%|63\.58%|
|RandomForest|68\.49%|45\.22%|88\.50%|59\.86%|

<p align="left">
  <img src="https://drive.google.com/uc?export=view&id=1cKZOQlssR_2jhgS88xirx74eCqe7OuGs" 
       alt="Imagen de portada" 
       width="600" />
</p>

## ✔️ Modelo Seleccionado

### **`RandomForestClassifier`**
- En función de las métricas obtenidas en los entrenamientos de los modelos, se elige este modelo como el más eficiente para la clasificación de la clase 1 (clientes que abandonan).
- Mejores parámetros RandomForest:
```
    'n_estimators': 100
    'max_depth': 10
    'min_samples_split': 5
    'min_samples_leaf': 4
    'max_features': 'sqrt'
    'bootstrap': True
    'class_weight': {0: 1, 1: 3}
    'random_state': 42
```
---



### 📈 Importancia de Variables codificadas

<p align="center">
  <img src="https://drive.google.com/uc?export=view&id=1E7Fv6JqBvJcV2-i07TrgM6vHe3GSbMx2" 
       alt="Importancia de variables" 
       width="600" />
</p>

---

### 📊 Matriz de Confusión

<p align="center">
 <img src="https://drive.google.com/uc?export=view&id=1KwCMW0Rj9pS1-tPO-7vvLyBlUaUEq00M" 
       alt="Matriz de Confusión" 
       width="600" />
</p>

---

### 📊 Curva ROC

<p align="center">
 <img src="https://drive.google.com/uc?export=view&id=1Nhcch6II5I9xTgzKj5ETRBljYeA-R5Ss" 
       alt="Curva ROC" 
       width="450" />
</p>

---

## 📦 Uso del Modelo Exportado

1. Cargar el modelo con `pickle`
2. Asegurarse de que los datos tengan la estructura original esperada
3. Usar `predict()` sobre el dataframe

```python
import pickle
import pandas as pd

with open("pipeline_final_RandomForest_produccion.pkl", "rb") as f:
    modelo = pickle.load(f)

nuevos_datos = pd.read_csv("data/nuevos_clientes.csv")
resultado = modelo.predict(nuevos_datos)
```

## 📦 Ejemplo de uso con datos nuevos

```
Probabilidades de Churn para nuevos datos
customerID	gender	Partner	Dependents	Contract	tenure	Prob Churn Sí	Prob Churn No	Conclusión
0	7857-XYZ	Female	No	No	One year	4	72.649390	27.350610	Abandona
1	6564-XYZ	Male	Yes	Yes	Two year	1	22.736765	77.263235	No abandona
2	8995-XYZ	Female	No	Yes	One year	2	39.875755	60.124245	No abandona
3	9331-XYZ	Female	Yes	Yes	Two year	6	23.767110	76.232890	No abandona
4	5424-XYZ	Female	Yes	Yes	One year	4	60.257756	39.742244	Abandona
5	7835-XYZ	Male	No	No	Month-to-month	6	88.197841	11.802159	Abandona
6	3060-XYZ	Male	Yes	No	One year	0	49.720079	50.279921	No abandona
7	3613-XYZ	Female	Yes	No	Two year	6	20.036170	79.963830	No abandona
8	7906-XYZ	Male	No	Yes	One year	5	59.317361	40.682639	Abandona
9	5342-XYZ	Female	Yes	Yes	One year	6	38.706768	61.293232	No abandona

```

---

## 📝 Notas

- La columnas `Charges.Total` fue evaluada, y se incluyó porque daba mejor resultado que al excluirla.
- El modelo fue entrenado en un pipeline que realiza todo el preprocesamiento internamente.
- No es necesario transformar numéricamente las columnas `Yes` / `No`, ya que el pipeline lo hace automáticamente.
- En datos de clientes nuevos se deben ingresar con tenure=0, Charges.Total = 0 y Charges.Monthly = 0

---

## 📷 Créditos de Imágenes

Las imágenes de métricas y gráficos se encuentran en Google Drive y se insertan usando el enlace con formato:

```
https://drive.google.com/uc?export=view&id=ID_DE_LA_IMAGEN
```

---
## 📂 Estructura del Repositorio

```
Telecom_X_part_2
├── data/           # Datos crudos
├── notebooks/      # Colab
├── src/            # Código fuente
├── output/         # Gráficos generados por scripts
│   ├── exploratory/
│   └── results/
├── models/         # modelos generados
├── docs/           # Documentación
│   ├── figures/    # Gráficos para documentos
│   └── report.md
└── README.md      
```

---
## 📫 Contacto

Para consultas o colaboración: [miguel.toro.romo@gmail.com](mailto:miguel.toro.romo@gmail.com)
