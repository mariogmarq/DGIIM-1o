## CONSTRUCCIÓN DE UN CUERPO DE 9 ELEMENTOS

*Autor: Daniel Pérez Ruiz*

### 0. PRELIMINARES

Partimos de que $9 = 3^2$. La base $3$ indica que vamos a trabajar en el conjunto $\Z_2[x]$, de polinomios con coeficientes en $\Z_2$. 

El expontente $2$ nos indica el grado de un polinomio irreducible que vamos a emplear para definir la segunda operación. En este caso $p(x)=x^2+1 \in \Z_2[x]$

### 1. DEFINICIÓN DEL CUERPO

Para definir un cuerpo necesitamos un conjunto y dos operaciones.

El **CONJUNTO**, en este caso estará formado por los polinomios de $\Z_3[x]$ de grado menor que 2 con coeficientes en $\Z_3$.
$$
K_9=\left\lbrace 0,1,2,x,x+1,x+2,2x,2x+1,2x+2 \right\rbrace
$$
La **PRIMERA OPERACIÓN** será la suma habitual de polinomios.

La **SEGUNDA OPERACIÓN** será el producto de dos polinomios, que no será el usual, sino el resto de dividir el producto habitual por el polinomio $p(x)$.

### 2. REALIZACIÓN DE LA TABLA

|        | $0$  |  $1$   |  $2$   |  $x$   | $x+1$  | $x+2$  |  $2x$  | $2x+1$ | $2x+2$ |
| :----: | :--: | :----: | :----: | :----: | :----: | :----: | :----: | :----: | :----: |
|  $0$   | $0$  |  $0$   |  $0$   |  $0$   |  $0$   |  $0$   |  $0$   |  $0$   |  $0$   |
|  $1$   | $0$  |  $1$   |  $2$   |  $x$   | $x+1$  | $x+2$  |  $2x$  | $2x+1$ | $2x+2$ |
|  $2$   | $0$  |  $2$   |  $1$   |  $2x$  | $2x+2$ | $2x+1$ |  $x$   | $x+2$  | $x+1$  |
|  $x$   | $0$  |  $x$   |  $2x$  |  $2$   | $x+2$  | $2x+2$ |  $1$   | $x+1$  | $2x+1$ |
| $x+1$  | $0$  | $x+1$  | $2x+2$ | $x+2$  |  $2x$  |  $1$   | $2x+1$ |  $2$   |  $x$   |
| $x+2$  | $0$  | $x+2$  | $2x+1$ | $2x+2$ |  $1$   |  $x$   | $x+1$  |  $2x$  |  $2$   |
|  $2x$  | $0$  |  $2x$  |  $x$   |  $1$   | $2x+1$ | $x+1$  |  $2$   | $2x+2$ | $x+2$  |
| $2x+1$ | $0$  | $2x+1$ | $x+2$  | $x+1$  |  $2$   |  $2x$  | $2x+2$ |  $x$   |  $1$   |
| $2x+2$ | $0$  | $2x+2$ | $x+1$  | $2x+1$ |  $x$   |  $2$   | $x+2$  |  $1$   |  $2x$  |

