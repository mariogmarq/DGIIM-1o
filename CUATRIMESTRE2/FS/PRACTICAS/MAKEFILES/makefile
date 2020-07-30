#MAKEFILE2: ARCHIVO MAKEFILE PARA PROGRAMA2
#DEPENDENCIAS: hello.cpp factorial.cpp main.cpp sin.cpp tan.cpp cos.cpp
#USO:	make -f makefile2
#	make -f makefile2 all	      >> construye todo el programa
#	make -f makefile2 library     >> construye librería necesaria
#	make -f makefile2 install_dir >> instala en escritorio
#	make -f makefile2 uninstall   >> desinstala el ejecutable
#	make -f makefile2 debug	      >> permite depuracion de programa
#	make -f makefile2 clean	      >> limpia los archivos objeto
#	make -f makefile2 remove_bin  >> elimina el ejecutable (util si no se usa install_dir)

#DECLARACIÓN DE VARIABLES PARA EL USO DE MAKEFILE

#1. CC: Asigna el compilador a utilizar.
CC=g++
#2. CPPFLAGS: Asigna rutinas de compilacion así como el directorio
#donde se encuentran las librerias necesarias
CPPFLAGS=-c -Wall $(CABECERA_DIR)
#3. CABECERA_DIR: Asigna el directorio de la libreria a buscar
DIRECTORIO_CABECERAS=cabeceras
CABECERA_DIR=-I./$(DIRECTORIO_CABECERAS) -L./
#4. INSTALL_DIR: Asigna la dirección donde instalar el programa
INSTALL_DIR=$(HOME)/Escritorio/
#5. EXECUTABLE: Asigna nombre de ejecutable
EXECUTABLE=programa
EXECUTABLE_DEBUG=programa_debug.out
#6. SOURCE_FILES: Asigna una lista de dependencias del programa final
SOURCE_FILES=main2.cpp sin.cpp cos.cpp tan.cpp factorial.cpp hello.cpp
#7. LIBRARY_FILES: Archivos necesarios para la creación de una librería
LIBRARY_FILES=sin.o cos.o tan.o
LIBRARY=libmates.a
#8. OBJECT_FILES: Asigna los correspondientes archivos objeto de SOURCE_FILES
OBJECT_FILES=$(SOURCE_FILES:.cpp=.o)

#============================================================================

#CONSTRUCCIÓN DEL MAKEFILE

#ALL: CONSTRUYE TODO EL PROGRAMA (DEPENDE DE: $(EXECUTABLE), $(OBJECT_FILES))
#[NOTA: NORMALMENTE EL OBJETIVO "ALL" PUEDE DEPENDER DE LIBRERÍAS]

all: $(OBJECT_FILES) $(EXECUTABLE)

#EXECUTABLE: CONSTRUYE EL CORRESPONDIENTE EJECUTABLE (DEPENDE DE $(OBJECT_FILES))
# $^ : REPRESENTA TODAS LAS DEPENDENCIAS SEPARADAS EN BLANCO
# $@ : NOMBRE DEL 0BJETIVO EN LA REGLA EN LA QUE NOS ENCONTRAMOS

$(EXECUTABLE): $(OBJECT_FILES) $(LIBRARY)
	$(CC) $(LIB_DIR) $^ -o $(EXECUTABLE) $(LIBRARY)

#.o: COMPILA TODOS LOS FICHEROS DE CÓDIGO FUENTE A OBJETO (DEPENDE DE LIBRERIAS)
#[EN CPPFLAGS YA SE INDICA A MAKE CÓMO DEBE ENLAZAR LAS LIBRERÍAS]
# $< : MUESTRA PRIMERA DEPENDENCIA NECESARIA 
#	[ archivo.o: dependencia.cpp ]
#	[ DEVUELVE: dependencia.cpp ]

.o: .cpp
	$(CC) $< -o $@

#$(LIBRARY): GENERA LA LIBRERIA PEDIDA
$(LIBRARY): $(LIBRARY) 
	ar -rvs $@ $^

library: $(LIBRARY_FILES) 
	ar -rvs $(LIBRARY) $(LIBRARY_FILES)
	rm *.o

#install_dir: INSTALA EL EJECTUABLE EN EL DIRECTORIO ASIGNADO

install_dir: $(EXECUTABLE)
	mv $(EXECUTABLE) $(INSTALL_DIR)

#uninstall: DESINSTALA EL PROGRAMA EJECUTABLE PREVIAMENTE INSTALADO
#EN EL DIRECTORIO ASIGNADO

uninstall:
	rm $(INSTALL_DIR)/$(EXECUTABLE)

#debug: PROPORCIONA INFORMACION PARA DEPURAR EL OBJETO EJECUTABLE

debug: $(EXECUTABLE_DEBUG) $(LIBRARY)

$(EXECUTABLE_DEBUG): $(OBJECT_FILES) $(LIBRARY)
	$(CC) -g $(LIB_DIR) -o $@ $(OBJECT_FILES) $(LIBRARY)

#clean: OBJETIVO PARA ELIMINAR TODOS LOS CÓDIGO OBJETO GENERADOS EN EL
#PROCESO DE COMPILACION

clean:
	rm *.o $(LIBRARY)

#remove_bin: OBJETIVO PARA ELIMINAR EL EJECUTABLE GENERADO

remove_bin:
	rm $(EXECUTABLE) $(EXECUTABLE_DEBUG)
