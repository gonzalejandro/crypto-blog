---
title: Oil and Vinegar
category: Criptografía Post Cuántica
order: 3
---

Dentro de los esquemas de encriptacion en base a polinomios multivariables, Unbalanced Oil and Vinegar (UOV) es uno de los mas conocidos, principalmente porque aun no se a diseñado un ataque que pueda romperlo. Por otro lado, el esquema original, Oil and Vinegar o Balanced Oil and Vinegar (BOV), fue quebrado poco tiempo despues de ser propuesto.

En esta seccion nos concentraremos en explicar como funcionan BOV y su version modificada UOV.

## Balanced Oil and Vinegar

La idea de este esquema proviene de un ataque, realizado sobre un esquema tambien basado en polinomios multivariables, el esquema Matsumoto-Imai, siendo esta idea la linearizacion de ecuaciones.

El esquema BOV se basa principalmente en dos problemas, MQ e IP:
 - Dado $$Y$$ y un conjunto de polinomios cuadraticos multivariables $$P$$ tal que 

 \begin{equation}
 	P(X) = (p_{1}(X), ..., p_{m}(X))
 \end{equation}

 con $$X$$ un vector de $$n$$ variables. El MQ-problem consiste en encontrar $$X$$ tal que

 \begin{equation}
 	P(X) = (p_{1}(X), ..., p_{m}(X)) = Y
 \end{equation}

 MQ-problem es NP-completo.

 - IP-problem hace referencia al problema de, dado el conjunto de polinomios $$P$$ y $$\overline{P}$$, encontrar un par de transformaciones afines $$L_{1}$$ y $$L_{2}$$ es un problema dificil.