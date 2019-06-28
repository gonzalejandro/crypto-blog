---
title: Criptografía de Llave Pública Multivariable
category: Criptografía Post Cuántica
order: 2
---

## 1. Introducción

Un sistema criptográfico de llave pública multivariable (MPKC por sus 
siglas en inglés) es un esquema de encriptación cuya llave pública está
conformada por un sistema de polinomios multivariables. Un sistema de 
polinomios multivariable no es más que un simple polinomio cuya forma
viene dada por más de una variable. Por ejemplo, un posible polinomio 
multivariable de grado dos podría ser el siguiente:

$$p(x,y) = x^2 + y^2 + 3xy + 4x + 7y + 2$$

Dicho lo anterior, dado un conjunto compuesto de $$m$$ polinomios 
multivariable, cada uno de $$n$$ variables, la llave pública de un MPKC 
se vería de la siguiente forma:

$$P(x_1,...,x_n)=(p_1(x_1,...,x_n),...,p_m(x_1,...,x_n))$$

Un MPKC puede ser utilizado para encriptar y/o autenticar mensajes. 
Siendo el último uno de los usos más desarrollados teóricamente.


## 2. Encriptación con MPKC


### 2.1 Encriptación
Para llevar a cabo la encriptación de un mensaje utilizando un MPKC, se 
asumirá que el texto a cifrar posee tantos símbolos como variables del
sistema de polinomios. Formalmente, sea $$M=(x_1,...,x_n)$$ el mensaje 
que se quiere cifrar y sea $$P$$ un sistema de polinomios multivariable
compuesto de $$m$$ polinomios cada uno de $$n$$ variables. Para cifrar
$$M$$ basta con:

$$P(M) = (p_1(x_1,...,x_n),...,p_m(x_1,...,x_n)) = (c_1,...,c_m)$$

Notar que los $$x_i$$ de arriba representan los símbolos del mensaje 
(y no las variables del sistema, como en la sección anterior) y que el 
largo del texto cifrado depende de la cantidad $$m$$ de polinomios.

### 2.2 Desencriptación
El proceso de desencriptación se necesita saber una trapdoor de manera 
que sea víable invertir el mapeo para encontrar el texto plano

$$M=(x_1,...,x_n) = P^{-1}(c_1,...,c_m)$$

Más adelante se hablará más con respecto a esta parte.


## 3. Autenticación con MPKC

### 3.1 Llave Pública
Nuevamente, la llave pública es de la forma:

$$P(x_1,...,x_n)=(p_1(x_1,...,x_n),...,p_m(x_1,...,x_n))$$

### 3.2 LLave Privada
Mientras que la llave privada es una trapdoor para calcular $$P^{-1}$$.

### 3.3 Firma
Ahora, para firmar, sea $$(h_1,...,h_m)$$ el hash de un mensaje. Se debe
computar:

$$(x_1,...,x_n) = P^{-1}(h_1,...,h_m)$$

Finalmente, se retorna el vector $$(x_1,...,x_n)$$

### 3.4 Verificación
Simplemente se debe chequear que:

$$(h_1,...,h_m) = P(x_1,...,x_n)$$

## 4. Seguridad de MPKC