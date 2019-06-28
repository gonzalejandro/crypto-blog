---
title: Oil and Vinegar
category: Criptografía Post Cuántica
order: 3
---

Dentro de los esquemas de criptograficos en base a polinomios multivariables, el esquema de autenticacion Unbalanced Oil and Vinegar (UOV) es uno de los mas conocidos, principalmente porque aun no se a diseñado un ataque que pueda romperlo. Por otro lado, el esquema original, Oil and Vinegar o Balanced Oil and Vinegar (BOV), fue quebrado poco tiempo despues de ser propuesto.

En esta seccion nos concentraremos en explicar como funcionan BOV y su version modificada UOV.

# Balanced Oil and Vinegar

La idea de este esquema proviene de un ataque, realizado sobre un esquema tambien basado en polinomios multivariables, el esquema Matsumoto-Imai, siendo esta idea la linearizacion de ecuaciones.

El esquema BOV se basa principalmente en dos problemas, MQ e IP:
 - Dado $$Y$$ y un set de polinomios cuadraticos multivariables $$P$$ tal que 

 \begin{equation}
 	P(X) = (p_{1}(X), ..., p_{m}(X))
 \end{equation}

 con $$X$$ un vector de $$n$$ variables. El MQ-problem consiste en encontrar $$X$$ tal que

 \begin{equation}
 	P(X) = (p_{1}(X), ..., p_{m}(X)) = Y
 \end{equation}

 MQ-problem es NP-completo.

 - Sean dos set de polinomios, $$P$$ y $$\overline{P}$$, de $$m$$ polinomios y $$n$$ variables, el IP-problem consiste en encontras dos transformaciones lineales afines, $$L_{1}$$ y $$L_{2}$$, tales que 

 \begin{equation}
 	P = L_{1} \circ \overline{P} \circ L_{2}
 \end{equation} 

 No se cree que este problema se pueda solucionar en tiempo polinomial, pero tampoco pertenece a la clase NP-hard.

## Construccion

El esquema BOV se basa en la dificultad de los problemas MQ e IP, para ello define dos sets de polinomios, $$P$$ y $$\overline{P}$$, donde ambos sets continen $$m$$ polinomios multivariables cuadraticos de $$n$$ variables, donde $$P$$ puede contener cualquier polinomio, pero $$\overline{P}$$ contiene polinomios especiales, los cuales facilitaran el uso de la llave privada. La relacion entre estos dos sets de polinomios esta dada por las transformaciones afines invertibles $$L_{1}$$ y $$L_{2}$$ tal que:

\begin{equation}
	P = L_{1} \circ \overline{P} \circ L_{2}
\end{equation}

Teniendo en cuenta lo anterior, podemos definir las llaves publicas y privadas como:
 - Llave publica: set de polinomios $$P$$
 - Llave privada: set de polinomios cuadraticos $$\overline{P}$$ y las transformaciones afines $$L_{1}$$ y $$L_{2}$$.

La idea es utilizar la clave privada para firmar algun mensaje $$y$$, y utilizar la dificultad del problema MQ para que no se pueda falsificar una firma a traves de la llave publica $$P$$. Con esto solo falta definir $$\overline{P}$$ para ser utilizado como la llave privada.

La construccion de los polinomios en el set $$\overline{P}$$ se basa en separar las variables en dos conjuntos, las variables oil y vinegar, y definir el polinomio de forma especial. Sean las variables oil $$X = (x_{1}, ..., x_{o})$$ y las variables vinegar $$Z = (z_{1}, ..., z_{v})$$, tal que $$n = o + v$$ y $$o = v$$, el polinomio $$p_{i} \in \overline{P}$$ esta definido como:

\begin{equation}
	p_{i}(X, Z) = \sum\limits_{h=1}^o \sum\limits_{j=1}^v \alpha_{h,j}^{(i)}x_{h}z_{j} + \sum\limits_{j=1}^v (\beta_{j}^{(i)}z_{j}^{2} + \gamma_{j}^{(i)}z_{j}) + \sum\limits_{h=1}^o \delta_{h}^{(i)}x_{h} + \eta^{(i)}
\end{equation}

### Firma y verificación

Una vez definido el set de polinomios $$\overline{P}$$, las transformaciones afines $$L_{1}$$ y $$L_{2}$$, y la llave publica $$P = L_{1} \circ \overline{P} \circ L_{2}$$, podemos empezar a definir el proceso de firma y verificacion.

 1. Verificacion
 Dado un mensaje $$Y = (y_{1}, ..., y{m})$$ y una firma $$X = (x_{1}, ..., x{n})$$, verificar si la firma corresponde al mensaje, basta con determinar si:

 \begin{equation}
 	P(X) = Y
 \end{equation}

 2. Firma
 El proceso de firma es un poco mas complejo, dado que tenemos el mensaje $$Y$$, queremos encontrar una firma $$X$$ tal que:

 \begin{equation}
 	L_{1} \circ \overline{P} \circ L_{2} (X) = Y
 \end{equation}
