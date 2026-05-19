# Análisis de Sentimiento en Prensa Uruguaya con Redes Neuronales
Este proyecto implementa y compara diversas arquitecturas de redes neuronales (MLP) para la clasificación de polaridad (Positivo, Negativo y Neutro) en un corpus de noticias de la prensa uruguaya.

## Objetivos del Proyecto
* Desarrollar un clasificador multiclase robusto para lenguaje natural.
* Comparar técnicas de representación de texto: desde métodos clásicos (Bag-of-Words/TF-IDF) hasta representaciones semánticas densas (Word Embeddings).
* Optimizar hiperparámetros para maximizar la métrica Macro-F1 debido al desbalance de clases.
## Metodología y Experimentos
### 1. Representaciones de Texto
* Línea Base (TF-IDF): Uso de n-gramas (unigramas y bigramas) con filtrado de frecuencias. Se implementó una red MLP con pesos en la función de pérdida para compensar la escasez de ejemplos 'Neutros'.
* Centroide de Embeddings: Representación de documentos mediante el promedio de vectores preentrenados del Spanish Billion Words (300d) y Wikipedia (100d).
### 2. Arquitectura del Modelo
* Tipo: Multi-Layer Perceptron (MLP).
* Configuración Óptima:
  * Capa oculta: 150-200 neuronas.
  * Activación: ReLU.
  * Regularización: Dropout y Weight Decay.
  * Optimización: Adam con tasa de aprendizaje de 0.005.
## Resultados Obtenidos

| Modelo  | Representación    | Macro F1 (Dev) | Accuracy (Test) |
|---------|-------------------|---------------:|----------------:|
| MLP v1  | TF-IDF            | 0.52           | -               |
| MLP v2  | Embeddings SBW    | 0.63           | 0.76            |
| MLP v3  | Embeddings Wiki   | 0.53           | -               |

El modelo final basado en Word Embeddings (SBW) demostró una capacidad superior para capturar el contexto semántico, logrando un Accuracy del 76.7% y un Macro F1 de 75.0% en datos nunca antes vistos.

## Conclusiones
* La representación mediante Embeddings preentrenados supera significativamente a los métodos de frecuencias de palabras.
* La clase Neutro representó el mayor desafío de aprendizaje, aunque el ajuste de hiperparámetros permitió mitigar el sesgo hacia las clases mayoritarias.
