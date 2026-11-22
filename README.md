# Proyecto 02 — Fine-tuning NLP

Proyecto de procesamiento de lenguaje natural con tres tareas: clasificación de reseñas, reconocimiento de entidades nombradas (NER) y traducción automática de chino a español. Se parte de modelos Transformer preentrenados y se realiza **fine-tuning supervisado** para cada tarea.

## Problemas y modelos

| Tarea                   | Dataset                                                                            | Modelo base                                                                   | Entrada → salida                                 |
| ----------------------- | ---------------------------------------------------------------------------------- | ----------------------------------------------------------------------------- | ------------------------------------------------- |
| Sequence Classification | [Amazon Reviews ES](https://huggingface.co/datasets/SetFit/amazon_reviews_multi_es) | [BETO uncased](https://huggingface.co/dccuchile/bert-base-spanish-wwm-uncased) | Reseña → calificación de 1 a 5 estrellas       |
| Sequence Labeling (NER) | [CoNLL-2002 ES](https://huggingface.co/datasets/BramVanroy/conll2002)               | [BETO cased](https://huggingface.co/dccuchile/bert-base-spanish-wwm-cased)     | Secuencia de tokens → etiquetas BIO de entidades |
| Sequence-to-Sequence    | [UN Parallel Corpus, es-zh](https://huggingface.co/datasets/Helsinki-NLP/un_pc)     | [M2M100-418M](https://huggingface.co/facebook/m2m100_418M)                     | Texto en chino → traducción al español         |

## Resultados en Test

| Tarea          | Métricas            | Resultado                                       |
| -------------- | -------------------- | ----------------------------------------------- |
| Clasificación | Accuracy / F1 macro  | 0,5898 / 0,5928 (4.934 reseñas)                |
| NER            | F1 micro por entidad | 0,8966 (1.527 secuencias)                       |
| Traducción    | SacreBLEU / chrF++   | 41,0292 / 62,1839 (muestra fija de 1.000 pares) |

En traducción, M2M100 sin ajuste obtuvo **24,9684 SacreBLEU** sobre la misma muestra de Test; tras el fine-tuning obtuvo **41,0292**. Estos resultados corresponden al dominio y a las particiones evaluadas, no a una garantía de rendimiento en cualquier texto.

## Contenido

- `Proyecto_02_NLP.ipynb`: preparación de datos, EDA, selección de hiperparámetros, fine-tuning, evaluación y demostraciones de inferencia
