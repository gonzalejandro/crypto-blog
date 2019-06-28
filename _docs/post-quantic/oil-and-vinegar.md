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
 - MQ-problem hace referencia al problema de, dado $$y$$ y un conjunto de polinomios cuadraticos multivariables $$P$$, encontrar $$x$$ tal que $$P(x) = y$$ es NP-completo.