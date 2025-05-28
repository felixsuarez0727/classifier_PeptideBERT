# CLASIFICADOR-PeptideBERT

Proyecto de clasificación de péptidos utilizando el modelo PeptideBERT. Este repositorio contiene el flujo principal de trabajo basado en el notebook `PeptideBERT-CPP.ipynb`.

## Requisitos previos

1. Instala dependencias desde el subdirectorio PeptideBERT:
   ```bash
   pip install -r PeptideBERT/requirements.txt
   ```

## Flujo de trabajo principal

1. **Ejecutar análisis**:

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
     - Ejecuta `python data/split_augment.py` y `python PeptideBERT/train.py` para preparar datos y entrenar el modelo.

## Resultados del entrenamiento

- **Métricas del modelo**:

  - `train_loss`: 0.63495
  - `val_accuracy`: 50.0%
  - `val_loss`: 0.5449

- **Evaluación en test**:
  - `Accuracy`: 48.64%
