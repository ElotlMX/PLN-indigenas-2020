# Etiquetadores automáticos

* Los etiquetadores automáticos son una tarea común del Procesamiento de Lenguaje
Natural (PLN)

. . .

* Es usual que se utilicen métodos de *Machine Learning (ML)* para su
  construcción

. . .

* En particular métodos basados en gráficas, por ejemplo Modelos Ocultos de
  Markov (*Hidden Markov Models, HMM*)


## Glosado

* El glosado es un tipo de etiquetado que asigna etiquetas a las unidades que
  conforman una palabra
* El glosado de textos es de suma importancia para el análisis y la
  documentación lingüística



# El lenguaje natural
 
* No obstante, el lenguaje natural es **complejo**
  * Presenta fenómenos que hacen de la construcción de etiquetadores
    automáticos una tarea difícil

. . .

* Tradicionalmente el glosado se hace manualmente
  * Esto es lento y costoso ya que requiere de habilidades de un
    lingüista y un trabajo intimo con hablantes nativos, los cuales, requieren
    capacitación en lingüística básica y de software (Moeller, 2018)

. . . 

* Adicionalmente, existen escenarios donde los métodos tradicionales no son
  efectivos como es el caso de los **bajos recursos digitales**
  
. . .

* La construcción de modelos automáticos que asistan este tipo de etiquetado
  surgen como **una tarea urgente**

# El reto: Bajos recursos digitales

* Los bajos recursos digitales son un escenario común en las lenguas mexicanas
  * A pesar de la gran diversidad lingüística, gran parte de las lenguas
    originarias no poseen contenido web ni publicaciones digitales
  * Esto propicia que carezcan de tecnologías del lenguaje

. . .

* Este entorno de experimentación supone importante **reto de invetigación** 
  * Los métodos tradicionales de etiquetado automático requieren grandes
    cantidades de datos para funcionar correctamente
  * La escasez de los corpus y falta de normalización puede complicar la tarea

# Objetivo

* En este trabajo esta en el marco de los bajos recursos digitales. 

. . .

* Nos enfocamos en la construcción de un **glosador automático para el otomí de
Toluca**

. . .

* Bucamos diseñar e implementar un etiquetador morfológico para el otomí de
Toluca basado en métodos de aprendizaje estructurado débilmente supervisado.

. . .

* Específicamente, *Conditional Random Fields (CRFs)* (Lafferty et al., 2001)
para el etiquetado morfológico

# Corpus 

:::::::::::::: {.columns}
::: {.column width="60%"}
* Para este trabajo se utilizó un corpus en otomí basado en el trabajo de
  Lastra (1992).

. . . 

* El corpus fue etiquetado y glosado manualmente por el
  lingüista Víctor Germán Mijangos Cruz.

. . .

* El corpus es un subconjunto del corpus paralelo español-otomí que
se encuentra en la plataforma web Tsunkua (`https://tsunkua.elotl.mx/`)
:::
::: {.column width="40%"}
![Portada de "El otomí de Toluca" de Lastra](img/otomi_toluca.png){height=50%}
:::
::::::::::::::



## Datos cualitativos del corpus

* La variante en particular es de la región de San Andrés Cuexcontitlan
* Incluye información morfosintáctica (etiquetas POS) y glosa.
* Se agregaron 81 casos con fenómenos poco frecuentes y, por tanto,
  particularmente difíciles de predecir.
 

## Datos cuantitativos del corpus

\begin{table}
	\centering
	\begin{tabular}{| c | c |}\hline
		\textbf{Categoría} & \textbf{Cuenta} \\ \hline
		Tokens (POS) & 8578\\
		Tipos (POS) & 44\\
		Tokens (Glosa) & 14477\\
		Tipos (Glosa) & 112\\
		\textbf{Total de oraciones etiquetadas} & \textbf{1786} \\ \hline
	\end{tabular}
	\caption{Tamaño del corpus}
	\label{table:corpus_length:1}
\end{table}

\begin{table}
	\centering
	\begin{tabular}{| c | c |}\hline
		\textbf{Textos} & \textbf{Número} \\ \hline
		Narrativos & 32 \\
		Dialogados & 4  \\
		\textbf{Total de textos}  & \textbf{36} \\\hline
	\end{tabular}
	\caption{Textos del corpus}
	\label{table:corpus_text:1}
\end{table}

# Arquitectura

1. Obtención del corpus en otomí

. . .

2. Codificación

. . .

3. Preprocesamiento

. . . 

4. Fase de entrenamiento

. . .

5. Fase de evaluación

---

![Arquitectura de aprendizaje](img/arquitectura.png "opt title")

## *Feature Functions*

### "hi tótsogí" (*No lo he dejado*) 

```
[
  'bias',
  'letterLowercase=ó',
  'EOS',
  'letterposition=-5',
  'prevletter=t>',
  'nxtletter=<t',
  'nxt2letters=<ts',
  'nxt3letters=<tso',
  'nxt4letters=<tsog'
]
```

Se obtuvieron *feature functions* por cada letra. Estas son las
correspondientes a la letra `ó`

# Evaluación

Se propusieron tres entornos de evaluación:

1. **Baseline**: Las *feature functions* fueron reducidas al mínimo
2. **POSLess**: Las *feature functions* fueron construidas ignorando la
   información de las etiquetas POS
3. **LinearCRF**: Toda la información lingüística del etiquetado manual es
   utilizada para la construcción de las *feature functions*

Para validar el desempeño utilizamos la técnica de *K-folds cross-validation*
con $K=10$ para cada modelo generado. 

# Resultados

Reportamos el *accuracy* promedio de cada modelo generado

# Conclusiones


---
title: "Glosador automático usando aprendizaje estructurado para el otomí de Toluca"
author: 
- Diego A. Barriga Martínez$^1$\newline
- Victor Mijangos Crúz$^1$\newline
- Ximena Gutierrez-Vasques$^2$
institute: 
- Universidad Nacional Autónoma de México$^1$
- Universidad de Zúrich$^2$
theme: metropolis
colortheme: default 
date: "5 de Noviembre 2020"
navigation: horizontal
incremental: true
---
