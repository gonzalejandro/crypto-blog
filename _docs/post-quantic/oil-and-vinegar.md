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
 - Llave publica: set de polinomios cuadraticos $$P$$
 - Llave privada: set de polinomios cuadraticos $$\overline{P}$$, y las transformaciones afines $$L_{1}$$ y $$L_{2}$$.

La idea es utilizar la clave privada para firmar algun mensaje $$y$$, y utilizar la dificultad del problema MQ para que no se pueda falsificar una firma a traves de la llave publica $$P$$. Con esto solo falta definir $$\overline{P}$$ para ser utilizado como la llave privada.

La construccion de los polinomios en el set $$\overline{P}$$ se basa en separar las variables en dos conjuntos, las variables oil y vinegar, y definir el polinomio de forma especial. Sean las variables oil $$X = (x_{1}, ..., x_{o})$$ y las variables vinegar $$Z = (z_{1}, ..., z_{v})$$, tal que $$n = o + v$$ y $$o = v$$, el polinomio $$p_{i} \in \overline{P}$$ esta definido como:

\begin{equation}
	p_{i}(X, Z) = \sum\limits_{h=1}^o \sum\limits_{j=1}^v \alpha_{h,j}^{(i)}x_{h}z_{j} + \sum\limits_{j=1}^v \sum\limits_{h=j}^v (\beta_{j}^{(i)}z_{j}z_{h} + \gamma_{j}^{(i)}z_{j}) + \sum\limits_{h=1}^o \delta_{h}^{(i)}x_{h} + \eta^{(i)}
\end{equation}

## Firma y verificación

Una vez definido el set de polinomios $$\overline{P}$$, las transformaciones afines $$L_{1}$$ y $$L_{2}$$, y la llave publica $$P = L_{1} \circ \overline{P} \circ L_{2}$$, podemos empezar a definir el proceso de firma y verificacion.

 1. Verificacion<br>
 Dado un mensaje $$Y = (y_{1}, ..., y{m})$$ y una firma $$X = (x_{1}, ..., x{n})$$, verificar si la firma corresponde al mensaje, basta con determinar si:

 \begin{equation}
 	P(X) = Y
 \end{equation}

 2. Firma<br>
 El proceso de firma es un poco mas complejo, dado que tenemos el mensaje $$Y$$, queremos encontrar una firma $$X$$ tal que:

 \begin{equation}
 	L_{1} \circ \overline{P} \circ L_{2} (X) = Y
 \end{equation}

 Primero, invertimos la transformacion afin $$L_{1}$$, con lo cual tenemos

 \begin{equation}
 	\hat{Y} = L_{1}^{-1}(Y)
 \end{equation}

 Ahora, necesitamos encontrar un $$\hat{X}$$ tal que

 \begin{equation}
 	\overline{P}(\hat{X}) = \hat{Y}
 \end{equation}

 Para ello, nos aprovechamos de la construccion de los polinomios en $$\overline{P}$$ y como interactuan las variables oil y vinegar, para lo cual, elegimos valores aleatorios dentro del espacio finito que asignamos a las variables vinegar. Producto de la construccion de los polinomios, el asignar valores a las variables vinegar produce que los polinomios pase a ser polinomios multivariables lineales, los cuales son posibles de resolver (eliminacion gaussiana) con una alta probabilidad (en el caso que no se pueda resolver, se repite el proceso)

 Finalmente, una vez obtenido un valor para $$\hat{X}$$, invertimos la ultima transformacion, con lo cual

 \begin{equation}
 	X = L_{2}^{-1}(\hat{X})
 \end{equation}

 siendo $$X$$ la firma del mensaje $$Y$$.

# Unbalanced Oil and Vinegar

Si bien el esquema BOV a primera vista pareciera ser muy robusto, este no es el caso, ya que fue quebrado poco despues de ser propuesto. Este ataque (Kipnis & Shamir) se aprovecho de la igualdad $$o = v$$, logrando recuperar una copia isomorfa de la clave privada.

Frente a este ataque se tiene dos opciones, elegimos $$o \lt v$$ ó $$o \gt v$$. El segundo caso no es posible, ya que se puede utilizar el mismo ataque para lograr obtener la clave, mientras que, la primera opcion, si bien puede ser atacada, este seria una versión probabilistica del ataque original, y su complejidad es del orden $$O(q^{v-o-1}o^{4})$$, siendo $$q$$ el tamaño del espacio finito.

Eligiendo el segundo caso, llegamos a la variante Unbalanced Oil and Vinegar, la cual tiene $$o \lt v$$, siendo la diferencia entre ambos lo suficiente como para que el ataque anterior no sea factible.

Ahora, teniendo un esquema que es seguro (hasta el momento), nos falta responder la pregunta ¿Es eficiente este esquema?, y la respuesta es no, este esquema no es eficiente en el sentido del tamaño de las claves. Es facil ver que, solo en la llave privada, esta es del orden de $$O(n^{2})$$ en memoria para $$L_{1}$$, $$O(m^{2})$$ para $$L_{2}$$ y $$O(mn^{2}})$$ para el set de polinomios $$\overline{P}$$.
Sabiendo lo anterior, ¿Se podra mejorar este esquema criptografico?