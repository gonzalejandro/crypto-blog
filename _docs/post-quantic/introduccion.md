---
title: Introducción
category: Criptografía Post Cuántica
order: 1
---
Debido al inminente avance de los computadores cuánticos y algoritmos 
tales como el algoritmo de Shor, algunos de los esquemas de encriptación y 
firmas criptográficas más utilizados actualmente podrían ser quebrados en un
tiempo más que razonable en comparación a lo que se podría lograr con 
computadores convencionales.


## El fin de la Criptografía?
Mucho se ha hablado acerca de los computadores cuánticos y las posibles
consecuencias que podría generar utilizar estos para romper los esquemas
criptográficos actuales, pero la verdad es que, si bien es un riesgo
inminente, estos pueden servir para atacar eficientemente a un grupo
acotado de sistemas criptográficos.

Los sistemas criptográficos que pueden ser quebrados por este medio, son
aquellos construídos bajo la asunción de que ciertos problemas son 
difíciles de resolver para un adversario poseedor de una cantidad de 
recursos computacionales razonables (relativos a computación clásica).
Entre aquellos problemas se encuentran el __problema de factorización__ 
y el __problema del logaritmo discreto__, cuyos mejores ataques no dejan
de ser de orden exponencial para computadores normales.

Si se llegase a crear un computador cuántico lo suficientemente potente
(cosa que por suerte hasta el día de hoy no ha pasado), estas asunciones
dejarían de ser válidas y por ende habría que encontrar reemplazos para
muchos de los sistemas criptográficos más utilizados hoy en día. Entre 
ellos, los mayores afectados serían esquemas de encriptación de llave 
pública tales como RSA o el protocolo Diffie Hellman, que se basan en 
los problemas mencionados más arriba y que son ampliamente utilizados
hoy en día.

Lo anterior, no significa el fin de la criptografía tal como la 
conocemos, pero sí implica una necesidad de encontrar alternativas. 


## Algoritmos de Encriptación Post Cuántica

Para suerte de todos, existe una amplia gama de clases de sistemas 
criptográficos resistentes a ataques (eficientes) por parte de
computadores cuánticos. Entre las principales se encuentran:

1. Hash-Based Cryptography
2. Code-Based Cryptography
3. Criptografía basada en retículos (lattices)
4. Criptografía de llave secreta
5. Criptografía de llave pública multivariable

En este blog, de momento nos enfocaremos en la última clase.
