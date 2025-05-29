# CLASIFICADOR-PeptideBERT

Proyecto de clasificación de péptidos utilizando el modelo PeptideBERT. Este repositorio contiene el flujo principal de trabajo basado en el notebook `PeptideBERT-CPP.ipynb`.

## Modelo utilizado

El modelo utilizado es una adaptación de [ProtBERT] con una cabeza de clasificación personalizada. El modelo contiene:

- **BertModel**: Base pre-entrenada de ProtBERT para representación de secuencias peptídicas
- **Cabeza de clasificación**:
  - Capa Linear (tamaño oculto → 1)
  - Capa Sigmoid para salida de probabilidad binaria

## Requisitos previos

1. Instala dependencias desde el subdirectorio PeptideBERT:
   ```bash
   pip install -r PeptideBERT/requirements.txt
   ```

## Flujo de trabajo principal

**Ejecutar análisis**:

- Abres el notebook principal:

  ```bash
  jupyter notebook PeptideBERT-CPP.ipynb
  ```

- **Datos propios**: El notebook ya contiene la configuración para usar datos personalizados.

  - Edita la ruta en la celda que contiene:
    ```python
    %cd /content/drive/MyDrive/...  #edit this path to your PeptideBERT directory
    ```

- **Construcción de conjunto de datos**:
  - Procesa los datos personalizados y genera `own_data-positive.npz` y `own_data-negative.npz` en `data/`.
- El script `split_augment.py` divide los datos en train/val/test y los almacena en `data/{task}/train.npz`, `data/{task}/val.npz` y `data/{task}/test.npz`
  - Ejecuta `python data/split_augment.py` y `python PeptideBERT/train.py` para preparar datos y entrenar el modelo.

## Resultados del entrenamiento y test

- **Modelo con datos CPP**:

| Métrica         | Valor   |
| --------------- | ------- |
| `train_loss`    | 0.63495 |
| `val_loss`      | 0.5449  |
| `val_accuracy`  | 50.00%  |
| `test_accuracy` | 48.64%  |

---

- **Modelo con datos RFU discretizadas a partir de la mediana**:

| Métrica         | Valor  |
| --------------- | ------ |
| `train_loss`    | 0.25   |
| `val_loss`      | 0.34   |
| `val_accuracy`  | 79.06% |
| `test_accuracy` | 91.66% |
