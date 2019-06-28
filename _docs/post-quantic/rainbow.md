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
  1. Calcular $$\hat{Y}$$, con $$\hat{Y} = L_{1}^{-1}Y$$
  2. Calcular $$\hat{X}$$, con $$\overline{P}(\hat{X}) = \hat{Y}$$
  3. Calcular $$X$$, con $$X = L_{2}^{-1} \hat{X}$$

 Donde $$X$$ es la firma del mensaje $$Y$$. Es en la parte 2 del calculo de la firma la cual tiene una gran diferencia con BOV y UOV.