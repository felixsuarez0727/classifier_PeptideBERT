# CLASIFICADOR-PeptideBERT

## Tabla de contenidos
1. [Modelo utilizado](#modelo-utilizado)
2. [Requisitos previos](#requisitos-previos)
3. [Flujo de trabajo principal](#flujo-de-trabajo-principal)
4. [Resultados del entrenamiento y test](#resultados-del-entrenamiento-y-test)

Proyecto de clasificación de péptidos utilizando el modelo PeptideBERT. Este repositorio contiene el flujo principal de trabajo basado en el notebook `PeptideBERT-CPP.ipynb`.

## Modelo utilizado

El modelo utilizado es una adaptación de [ProtBERT] con una cabeza de clasificación personalizada. El modelo contiene:

- **BertModel**: Base pre-entrenada de ProtBERT para representación de secuencias peptídicas
- **Cabeza de clasificación**:
  - Capa Linear (tamaño oculto → 1)
  - Capa Sigmoid para salida de probabilidad binaria

## Requisitos previos

### Instalación de dependencias
Instala las dependencias necesarias ejecutando:
```bash
pip install -r PeptideBERT/requirements.txt
```

## Flujo de trabajo principal

Sigue estos pasos para ejecutar el análisis:

1. **Abrir el notebook principal**:
   ```bash
   jupyter notebook PeptideBERT-CPP.ipynb
   ```

2. **Usar datos propios**:
   - El notebook contiene una configuración para usar datos personalizados.
   - Edita la siguiente celda en el notebook para apuntar a tu directorio de PeptideBERT:
     ```python
     %cd /content/drive/MyDrive/...  # Edita esta ruta a tu directorio PeptideBERT
     ```

3. **Construir el conjunto de datos**:
   - Procesa tus datos personalizados para generar los archivos `own_data-positive.npz` y `own_data-negative.npz` en el directorio `data/`.
   - Ejecuta el script `split_augment.py` para dividir los datos en conjuntos de entrenamiento, validación y prueba:
     ```bash
     python data/split_augment.py
     ```
     Esto generará los archivos `train.npz`, `val.npz` y `test.npz` en `data/{task}/`.

4. **Entrenar el modelo**:
   ```bash
   python PeptideBERT/train.py
   ```

## Resultados del entrenamiento y test

### Modelo con datos CPP
Resultados obtenidos con el modelo entrenado en datos CPP:

| Métrica       | Valor   |
| ------------- | ------- |
| train_loss    | 0.63495 |
| val_loss      | 0.5449  |
| val_accuracy  | 50.00%  |
| test_accuracy | 48.64%  |

---

### Modelo con datos RFU discretizadas
Resultados de clasificación con PeptideBERT sobre el dataset B:

| Métrica      | Media (1.54) | Mediana (1.64) |
| ------------ | ------------ | -------------- |
| **Exactitud**| 0.81         | 0.91           |
| **Precisión**| 0.72         | 0.88           |
| **Recall**   | 0.90         | 0.95           |
| **F1 Score** | 0.79         | 0.91           |
