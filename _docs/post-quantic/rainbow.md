---
title: Rainbow
category: Criptografía Post Cuántica
order: 4
---

Anteriormente, se vio el esquema Balanced Oil and Vinegar, el cual ya ha sido roto, y su variante Unbalanced Oil and Vinegar, que aun no ha sido roto. De la misma manera, tambien se vio que el esquema UOV no es un esquema muy eficiente, debido a lo grande que pueden llegar a ser las claves que utiliza, es por ello que se desarrollo una nueva variante, la cual se denomina Rainbow.

# Idea general

El problema principal de UOV es lo masivo que pueden llegar a ser la claves usadas, por lo que el principal objetivo del esquema Rainbow es reducir el tamaño de las llaves, para ello, Rainbow modifica el set de polinomios $$\overline{P}$$ utilizado en UOV.

La modificacion que se realiza consiste en separar los polinomios del set en distintas capaz, donde la cantidad de variables utilizadas en una capa es menor a la cantidad de variables utilizadas en la siguiente capa.

La idea central de Rainbow es el de calcular las variables de una capa, y estos resultados utilizarlos para calcular las variables que se encuentran en la siguiente capa, y para ello, en cada capa se resuelven los polinomios como si fuera un firma del esquema UOV.

## Llaves

Manteniendo las llaves usadas en UOV, sean las transformaciones afines $$L_{1}$$ y $$L_{2}$$ y los sets de polinomios $$P$$ y $$\overline{P}$$, tales que

\begin{equation}
	P = L_{1} \circ \overline{P} \circ L_{2}
\end{equation}

Entonces las llaves privadas y publicas son:

 - Llave publica: set de polinomios cuadraticos $$P$$.
 - Llave privada: set de polinomios cuadraticos $$\overline{P}$$, y las transformaciones afines $$L_{1}$$ y $$L_{2}$$.

## Firma y verificacion

Una vez definido el set de polinomios $$\overline{P}$$, las transformaciones afines $$L_{1}$$ y $$L_{2}$$, y la llave publica $$P = L_{1} \circ \overline{P} \circ L_{2}$$, podemos empezar a definir el proceso de firma y verificacion.

 1. Verificación
 Al igual que en BOV y UOV, la verificacion de una firma $$X$$ y un mensaje $$Y$$ se realiza al evaluar la firma con la llave publica, y comprobar la igualdad

 \begin{equation}
 	P(X) = Y
 \end{equation}

 2. Firma
 Se mantiene la idea de calcular la firma a partir de resolver las mismas ecuaciones que en UOV:
	- Calcular $$\hat{Y}$$, con $$\hat{Y} = L_{1}^{-1}Y$$
	- Calcular $$\hat{X}$$, con $$\overline{P}(\hat{X}) = \hat{Y}$$
	- Calcular $$X$$, con $$X = L_{2}^{-1} \hat{X}$$

 Donde $$X$$ es la firma del mensaje $$Y$$. Es en la parte 2 del calculo de la firma la cual tiene una gran diferencia con BOV y UOV.

 Como se dijo anteriormente, la idea de Rainbow es aplicar UOV capa por capa, para ello definimos los valores $$v_{i}$$, $$1 \leq i \leq u$$, con $$u-1$$ la cantidad de capas en Rainbow, y donde los valores $$v_{i}$$ cumplen

 \begin{equation}
 	0 \lt v_{1} \lt ... \lt v_{u} = n
 \end{equation}

 Adicionalmente, definimos los valores $$o_{i}$$, $$1 \leq i \leq u$$, de forma tal que

 \begin{equation}
 	o_{i} = v_{i+1} - v_{i}
 \end{equation}

 A partir de los valores definidos anteriormente, podemos definir lo que son las capas dentro del esquema:
  1. El esquema posee $$u-1$$ capas.
  2. La i-esima capa esta compuesta por $$o_{i}$$ polinomios.
  3. Todos los polinomios dentro de la i-esima capa tienen $$v_{i+1}$$ variables, donde las primeras $$v_{i}$$ corresponde a variables vinegar y las siguientes o_{i} variables son variables oil.
  4. Las $$v_{i+1}$$ variables dentro de la i-esima capa, son variables vinegar dentro de la (i+1)-esima capa.

 Con las capas ya definidas, podemos explicar el procedimiento con el cual se resuelve la ecuacion $$\overline{P}(\hat{X}) = \hat{Y}