## EXAMEN DE FUNDAMENTOS DEL SOFTWARE: TEMAS 1 Y 2

*Autor: Daniel Pérez Ruiz*



1.- Suponga una máquina (imaginaria) que direcciona por palabras de 32 bits. Su memoria principal está organizada en 256 marcos de página y cada marco es de 1 KB. Por otra parte, las instrucciones máquina usan 8 bits para el código de instrucción. En este supuesto:

* a) ¿Cuántos bits serían necesarios para un acceso a memoria?
* b) ¿Cuántas instrucciones máquina puede tener implementadas como máximo ese procesador?
* c) ¿Qué tipos de instrucciones máquina debería incluir al menos el procesador para ser considerado de propósito general (poder resolver cualquier tipo de problema)?

2.- Diferencias entre lenguaje máquina, ensamblador y lenguaje de alto nivel (de tercera generación).

3.- a) Enumere los componentes principales de una arquitectura básica para un sistema de computación.  b) Describa la funcionalidad de los diversos tipos de registros del procesador.

4.- a) Ciclo de instrucción de una E/S dirigida por interrupciones. b) Diferencias entre monoprogramación, multiprogramación y tiempo compartido.

5.- a) Diferencias entre el modo supervisor y el modo usuario en la ejecución de instrucciones máquina.   En el contexto de los modos de ejecución de instrucciones:

* b) ¿qué se entiende por "trampa"?, 

* c) ¿qué acciones deben llevarse a cabo en una "trampa"?

6.- Concepto de:

* a) Programa / Proceso / Hebra.

* b) ¿Qué información debe contener al menos el Bloque de Control de Proceso (PCB)?

7.- Describa de forma breve, pero completa, el Modelo de Cinco Estados de los procesos.

8.-Pasos seguidos durante un cambio de contexto de ejecución.

9.- a) ¿Qué es la reubicación? b) ¿Qué es la reubicación estática? c) ¿Y la dinámica?

10.- Describa los siguientes conceptos:

* a) Paginación, marco, página de memoria.

* b) Segmentación, segmento de memoria.

* c) Esquema de traducción de direcciones

* d) Swapping

* e) Memoria virtual

11.- Suponga una máquina de memoria de 2GB, marcos de página de 1KB y un proceso que ocupa 6 páginas. Si la table de páginas incluye un bit de protección para cada entrada, ¿cuántos bytes ocuparía dicha tabla?

12.- Considere la siguiente tabla de páginas para un proceso en un sistema con gestión de memoria paginada. Si el tamaño de página es de 2048 bytes, ¿qué dirección física corresponde a cada una de las direcciones lógicas que se dan a continuación? En caso de no poder realizar la traducción, explique por qué no se puede:

| Número Página | Número Marco Página |
| ------------- | ------------------- |
| 0             | 3                   |
| 1             | 13                  |
| 2             | 7                   |
| 3             | 8                   |
| 4             | 14                  |

* a) 2048

* b) 37

* c) 13055

* d) 10128