
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

|customerID|gender|Partner|Dependents|Contract|tenure|Prob Churn Sí|Prob Churn No|Conclusión|
|---|---|---|---|---|---|---|---|---|
|6368-XYZ|Female|No|No|Month-to-month|4|54\.835601753950016|45\.164398246049984|Abandona|
|8147-XYZ|Male|Yes|Yes|One year|2|68\.08477383050534|31\.915226169494638|Abandona|
|6283-XYZ|Female|No|Yes|Month-to-month|1|50\.91046146362185|49\.08953853637816|Abandona|
|1494-XYZ|Male|No|Yes|One year|4|52\.12211712341105|47\.87788287658896|Abandona|
|7845-XYZ|Male|No|No|Two year|6|16\.599381118924736|83\.40061888107526|No abandona|
|8058-XYZ|Female|Yes|No|Month-to-month|3|82\.32023111142516|17\.679768888574834|Abandona|
|7841-XYZ|Female|Yes|Yes|Two year|1|50\.60853908877754|49\.391460911222474|Abandona|
|7614-XYZ|Female|Yes|Yes|Two year|0|51\.97490331047058|48\.02509668952943|Abandona|
|2060-XYZ|Female|No|No|One year|4|38\.292381453340354|61\.707618546659674|No abandona|
|3193-XYZ|Male|Yes|No|One year|4|38\.02543198201495|61\.974568017985064|No abandona|


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
