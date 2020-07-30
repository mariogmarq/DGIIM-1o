## EXAMEN DE FUNDAMENTOS DEL SOFTWARE: TEMAS 4 Y 5

*Autor: Daniel Pérez Ruiz*

#### 1. Definición de archivo, registro, campo, operaciones que se pueden realizar sobre un archivo.

* *ARCHIVO:* es conjunto de información sobre un mismo tema, tratada como una unidad
  de almacenamiento en memoria secundaria y organizada de forma estructurada para la
  búsqueda de un dato individual.
  * *PROPIEDADES DE UN ARCHIVO (NO SE PIDE EN ESTE EJERCICIO, PERO VIENE BIEN):*
    * El S.O permite que el usuario pueda aludir al archivo mediante un nombre, independientemente de la forma en que se almacene en el dispositivo.
    * Todo archivo tiene asociados unos atributos, además del nombre, como: tamaño, fecha de
      creación y de modificación, propietario, permisos de acceso, etc.
  * *OPERACIONES SOBRE UN ARCHIVO:*
    * Crear/copiar/borrar/renombrar un archivo.
    * Establecer/obtener atributos de un archivo.
    * Abrir/cerrar un archivo para el procesamiento de su contenido.
    * Leer/escribir un registro de un determinado archivo.
* *REGISTRO:* estructura o unidad que forma el archivo y que contiene la información
  correspondiente a un elemento individual.
* *CAMPO:* es un dato que forma parte de un registro y representa una información unitaria o independiente.

#### 2. Clasificación de los archivos según el tipo de sus registros.

* **LONGITUD FIJA:** los registros tienen la misma longitud.
* **LONGITUD VARIABLE:** los registros no tienen la misma longitud. Sin embargo, si se sabe la
  longitud que tiene cada registro, ya que el sistema reserva una palabra al comienzo de cada
  registro para anotar su longitud.
  * **Con delimitador**: un determinado carácter llamado delimitador marca el fin de un
    registro (suelen usarse como delimitadores el salto de línea, nulo…).
  * **Con cabecera**: cada registro contiene un campo inicial que almacena el número de
    bytes del registro.
* **LONGITUD INDEFINIDA**: los registros no tienen la misma longitud y no sabemos la longitud que
  van a tener. 
  * El SO no realiza ninguna gestión sobre la longitud de los registros ya que el
    archivo no tiene realmente ninguna estructura interna. 
  * En cada operación de lectura/escritura se transfiere una determinada subcadena del archivo y será el programa de usuario quien indique al SO el principio y final de cada registro.
* Una posibilidad añadida: disponer de un campo clave (o llave) que permita localizar
  rápidamente un registro.

#### 3. Organización secuencial de archivos: concepto, operaciones que soporta, ventajas e inconvenientes.

* *CONCEPTO:* Los registros se encuentran en cierto orden y yuxtapuestos consecutivamente.
  Los registros han de ser leídos necesariamente según este orden.
* *OPERACIONES QUE SOPORTA:*
  * **AÑADIR:** Solo es posible escribir al final del archivo, después del último registro escrito.
  * **CONSULTA O RECUPERACIÓN**: Se realiza en orden secuencial, es decir, el orden en el que se
    hubieran escrito determina el orden en el que se leen los registros. Para leer el registro que
    ocupa la posición n en el archivo es necesario leer previamente los n-1 registros que hay
    antes que él.
  * **INSERCIÓN, MODIFICACIÓN Y ELIMINACIÓN:** 
    * La modificación de un registro solo es posible si no se aumenta su longitud.
    * No es posible eliminar un registro del archivo, pero se puede realizar un borrado lógico,
      es decir, marcarlo de tal forma que al leer se identifique como no válido.
    * En otros casos es necesario crear un archivo nuevo con las actualizaciones que se
      quieran realizar.
    * No se puede insertar los registros en el medio.
* **VENTAJAS:**
  * Buen aprovechamiento del espacio.
  * Sencilla de utilizar.
  * Se puede utilizar con dispositivos secuenciales que son de bajo precio.
* **INCONVENIENTES:**
  * (Ver modificación, inserción, eliminación).

#### 4. Organización secuencial encadenada de archivos: concepto, operaciones que soporta, ventajas e inconvenientes.

- *CONCEPTO:* Junto a cada registro se almacena un puntero con la dirección física del registro siguiente, dando lugar a una cadena de registros. El último registro de la cadena contiene una marca especial en el lugar del puntero indicando que ya no hay más registros en el archivo.
- *OPERACIONES QUE SOPORTA:*
  - **CONSULTA O RECUPERACIÓN:** La consulta es secuencial, al igual que en un archivo con
    organización secuencial pura. Cada vez que se lee un registro se lee la posición del
    siguiente, lo que permite seguir la secuencia lógica del archivo.
  - **INSERCIÓN**: Para insertar un registro hay que seguir los siguientes pasos:
    1. Localizar la posición donde se desea insertar, es decir, entre qué dos registros debe
       estar el nuevo registro del archivo.
    2. Escribir el registro en una zona libre de memoria.
    3. Asignar al nuevo registro como puntero la dirección física del registro siguiente.
    4. Modificar el registro anterior para actualizar el valor de su puntero de forma que
       contenga la dirección del nuevo registro.
  - **BORRADO:** Para borrar un registro se asigna al puntero del registro anterior la dirección del
    registro siguiente al que se desea borrar.
  - **MODIFICACIÓN:** Si el cambio no implica un aumento de longitud del registro, éste puede
    reescribirse en el mismo espacio. En caso contrario, se debe insertar el registro y luego
    borrar la versión anterior al cambio.
- **VENTAJAS:**
  - Facilidad de inserción y borrado de registros.
- **INCONVENIENTES:**
  - Limita las consultas de forma secuencial.

#### 5. Organización secuencial indexada de archivos: concepto, operaciones que soporta, ventajas e inconvenientes.

- *CONCEPTO:* Se utiliza un índice para obtener la ubicación de la zona del archivo donde se
  encuentra del registro buscado. Esto permite localizar un registro sin leer previamente todos
  los que le preceden (solo los de su zona).
- *ESTRUCTURAS POR LAS QUE ESTÁ FORMADA LA ORGANIZACIÓN SECUENCIAL INDEXADA:*
  - **ZONA DE REGISTROS:** Se encuentran los registros en sí, ordenados según el valor de una llave.
    Es una zona donde se direccionan los registros del archivo y está dividida en tramos (conjunto de registros consecutivos). Por cada tramo hay un registro en un la zona de índices.
  - **ZONA DE ÍNDICES:** Es una zona en la que por cada tramo de la zona de registros hay un
    registro que contiene:
    - El mayor valor de la llave del tramo (valor de llave del último registro del tramo).
    - La dirección del primer registro del tramo.
- *OPERACIONES QUE SOPORTA:*
  - **AÑADIR:** Solo es posible escribir al final del archivo, después del último registro escrito.
  - **CONSULTA**: Se realiza por llave (esto es, localizar un registro conocida su llave) sin necesidad
    de leer los registros que no se encuentran en su mismo tramo. El procedimiento a seguir para
    realizar una consulta por llave es:
    1. Leer secuencialmente las llaves en la zona de índices hasta encontrar una mayor o igual
       a la del registro buscado.
    2. Obtener la dirección de comienzo del tramo donde está el registro.
    3. Leer secuencialmente el tramo de la zona de registros a partir de la dirección obtenida
       en la zona de índices hasta encontrar el registro buscado o uno con valor de llave mayor
       que el buscado (en este último caso el registro no se encuentra en el archivo).
  - **INSERCIÓN:**. Dado que ambas zonas son secuenciales, no es posible insertar un registro en
    archivos con esta organización. En algunos casos se permite la escritura de nuevos registros
    al final de la zona de registros. Estos registros, como es lógico, no podrán ser consultados
    por llave con el procedimiento descrito anteriormente.
  - **BORRADO**. Al estar los registros escritos en secuencia no es posible borrar un registro. La
    única forma de eliminar la información contenida en un registro es marcándolo, lo que se
    conoce como borrado lógico.
  - **MODIFICACIÓN:** Las modificaciones son posibles tan sólo si el registro no aumenta de longitud
    al ser modificado y no se altera el valor de la llave del mismo.
- **VENTAJAS:**
  - Resulta útil cuando se debe combinar consultas a registros concretos y el
    procesamiento secuencial de todo archivo.
- **INCONVENIENTES:**
  - Imposibilidad de realizar actualizaciones.

#### 6. Organización directa o aleatoria de archivos: concepto, operaciones que soporta, ventajas e inconvenientes.

* *CONCEPTO:* En la organización directa o aleatoria un archivo está escrito sobre un soporte de acceso directo para el que existe una función de transformación que genera la dirección de cada registro en el archivo a partir de un campo que se usa como llave.
* *OPERACIONES QUE SOPORTA:*
  * **CONSULTA:** Se realiza por llave.
  * **BORRADO:** Siempre se realiza un borrado lógico.
  * **MODIFICACIÓN E INSERCIÓN:** Siempre se puede realizar, siempre que se realice también la transformación de la llave correspondiente.
* **VENTAJAS:** Útil para archivos donde los accesos deben realizarse por llave, accediéndose siempre a registros concretos.
* **INCONVENIENTES:** No es conveniente utilizar esta organización si la información se va a procesar en conjunto.

#### 7. Bases de datos: concepto, requisitos que debe cumplir un buen sistema de base de datos.

* *CONCEPTO:*  Una base de datos es un sistema formado por un conjunto de datos y un paquete software para gestión de dicho conjunto de datos de tal modo que:

  * Se controla el almacenamiento de datos redundantes;
  * Los datos resultan independientes de los programas que los usan;
  * Las relaciones entre los datos se almacenan junto a ellos;
  * Se puede acceder a los datos de diversas formas.

* *REQUISITOS PARA UNA BUENA BASE DE DATOS:*

  1. **ACCESO MÚLTIPLE**. Diversos usuarios pueden acceder a la base de datos, sin que se
     produzcan conflictos, ni visiones incoherentes.

  2. **UTILIZACIÓN MÚLTIPLE**. Cada usuario podrá tener una imagen o visión particular de la
      estructura de la base de datos.
  3. **FLEXIBILIDAD**. Se podrán usar distintos métodos de acceso, con tiempos de respuesta
      razonablemente pequeños.
  4. **SEGURIDAD**. Se controlará el acceso a los datos (a nivel de campo), impidiéndoselo a los
      usuarios no autorizados.
  5. **PROTECCIÓN CONTRA FALLOS**. Deben existir mecanismos concretos de recuperación en caso de fallo de la computadora.
  6. **INDEPENDENCIA FÍSICA**. Se puede cambiar el soporte físico de la base de datos sin que esto
      repercuta en la base de datos ni en los programas que la utilizan.
  7. **INDEPENDENCIA LÓGICA**. Se pueden modificar los datos contenidos en la base, las relaciones
      existentes entre ellos o incluir nuevos datos, sin afectar a los programas que la usan.
  8. **REDUNDANCIA CONTROLADA**. Los datos se almacenan una sola vez. (¿La redundancia es
      indirecta???)
  9. **INTERFAZ DE ALTO NIVEL**. Existe una forma sencilla y cómoda de utilizar la base al menos
      desde un lenguaje de programación de alto nivel.
  10. **INTERROGACIÓN DIRECTA ("QUERY")**. Existe una utilidad que permite el acceso a los datos de forma interactiva o conversacional.

#### 8. Estructura de una base de datos: entidades, atributos, identificador o clave primaria, relación y cardinalidad de una relación.

* *ENTIDADES*: Cualquier ente sobre el que se almacena información.
* *ATRIBUTOS:* Datos referidos a una entidad que se almacenan en una base de datos. Cualquier atributo de una entidad representa una propiedad de la misma.
* *IDENTIFICADOR:* Se dice que uno o más atributos de una entidad es un identificador o clave primaria si el valor de dichos atributos determina de forma unívoca cada uno de los elementos de dicha entidad, y no existe ningún subconjunto de él que permita identificar a la entidad de manera única.

#### 9. Concepto de: esquema de una base de datos, vista o subesquema.

* *ESQUEMA:* Se especifica qué información se guarda en la base de datos, incluyendo todos los datos almacenados en ella y las relaciones entre ellos. 
* *VISTA O SUBESQUEMA:* Parte de la base de datos que interesa a un determinado grupo de usuarios.

#### 10. Describa los distintos tipos de bases de datos.

* *MODELO DE DATOS JERÁRQUICO:* Permite especificar una base de datos jerárquica, donde se establece una relación jerárquica entre los datos en forma de árbol, y no es posible definir relaciones muchos a muchos.
* *MODELO DE DATOS EN RED:* Permite especificar una base de datos en red, donde pueden darse relaciones binarias con cualquier cardinalidad y no es necesario que la estructura tenga forma de árbol.
* *MODELO DE DATOS RELACIONAL:* Permite especificar una base de datos relacional, que estará formada por tablas. Una tabla es una estructura bidimensional formada por una sucesión de registros del mismo tipo.

#### 11. Concepto de Sistema de Gestión de Bases de Datos (SGBD). Lenguajes que debe soportar un SGDB.

* *SGDB:* Conjunto de software destinado a la creación, control y manipulación de la información de una base de datos.
* *LENGUAJES QUE DEBE SOPORTAR:*
  * *Lenguaje de descripción de datos (DDL):* Se usa para la descripción del esquema y de los subesquemas.
  * *Lenguaje de manipulación de datos (DML):* Se utiliza para el acceso a la base de datos desde lenguajes de alto nivel o en modo conversacional.

#### 12. Concepto de: plataforma, entorno integrado de desarrollo (IDE), marco de trabajo (framework).

* *PLATAFORMA:* Concepto de hardware y/o software utilizada para ejecutar aplicaciones software.
* *IDE:* Aplicación que proporciona un conjunto de herramientas relacionadas para el desarrollo del software: creación y edición de código fuente, generadores de código objeto, y despliegue y depuración de programas.
* *FRAMEWORK:* Abstracción que proporciona software con funcionalidad genérica que puede cambiarse selectivamente mediante código de usuario para la creación de aplicaciones.

