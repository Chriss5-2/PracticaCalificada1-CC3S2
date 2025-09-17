# PracticaCalificada1-CC3S2
# Grupo 2
# Proyecto 2

Para poder ejecutar los comandos, es necesario ejecutar

```bash
mkdir Proyecto
cd Proyecto
git clone https://github.com/Grupo2-CC3S2/Practica_Calificada_1-CC3S2.git
```

Y con eso podremos ejecutar todos los comandos realizados

**Es necesario tener curl, dig instalado y estar en un entorno de Linux tanto como en el mismo Linux o en WSL si se está en Windows**

Mi rol en este proyecto fue más que nada ser el encargado de automatizar los scripts y testearlos para verificar que pueden pasar pruebas básicas con bats, además de crear el pipeline para hacer la integración con DevSecOps y así tener un entorno enfocado más a lo real.

Lo primero que hice fue el [**Makefile**](src/Makefile) en el cual automatice todos los scripts que creó mi compañero para poder ejecutarlos en simples comandos y de manera rápida, esto lo realicé haciendo que algunos comandos se ejecuten en segundo plano en una tarea, y otra tarea estaba designada a detener esa ejecución, por lo que con eso nos ahorramos tiempo y podemos ejecutar y probar todos los scripts en una misma consola y en menos tiempo, además de que seguí la metodologia de 12 Factor App donde en el Makefile, genere tareas robustas encargadas de la instalación de dependencias y la ejecución de varias tareas a la vez que tienen la misma características, así evitamos errores de compilación y mayor velocidad en el análisis de los scripts.
Luego generé un pipeline básico, encargado de ejecutar todos los procesos del Makefile y asi verificar el funcionamiento de cada scripts, además de realizar los testeos en su propio entorno y verificar que la creación de los servidores de los scripts, cumplen con lo requerido,y por último, un **job** en específico del pipeline, se apoyó de la instalaciónd de dependencias del Makefile, para así tener un **job** robusto pero que cumpla con el proceso de instalación de todas las dependencias, permitiendo así su entendimiento.
Los videos se encuentran en la carpeta [videos](videos/README.md) el cual contiene los links de los videos ya que por espacio de github, no se permitió subir los videos en formato mp4

Para las pruebas, ya que tenia que realizar pruebas a archivos bash, lo que se necesitaba fue realizar pruebas bats, por lo que primero instalé la extensión de **Bats** en VS Code, y de ahí empecé a escribir las pruebas bats, para este caso fueron pruebas básicas, las cuales se basaban en verificar si el puerto está abierto, o si está en modo de escucha, o al levantar el servidor, verificar si este da respuesta al realizarse una solicitud HTTP o no, y básicamente eso fue todo lo abarcado para las pruebas, soy consciente que se necesitan más pero por el momento solo pude realizar eso


## Probar los comandos
Al clonar el repositorio, necesitamos ir a la carpeta donde se clonó y a partir de ahí, ejecutar los comandos
```bash
# Levantar el servidor
make run

# Ejecutar solicitud http con curl
make client

#Verificar que el puerto está siendo ocupado
make check

# Bajar el servidor
make stop
```
Estos son los comandos básicos a ejecutar pero para pruebas más avanzadas podemos ejecutar
```bash
# Ejecutar procesos
make run-procesos

# Detener todos los procesos ejecutados
make stop-procesos

# Recolectar los logs
make collect-logs
```
Para prepararnos para el entorno de las pruebas es necesario usar:
```bash
# Instalar bats
make install-bats

# Ejecutar pruebas
make test
```
Luego de eso podremos ver que todas las tareas pasan correctamente y por último será ejecutar los linters
```bash
# Instalar shellcheck que sirve para aplicar linters
make lint

# Aplicarlo en los scripts
make check-lint
```

Y para este proyecto, esa serían las tareas realizadas para la automatización, pruebas bats e integración con DevSecOps.

### Mejoras futuras
Tenía pensado realizar filtraciones para navegadores especificos al momento de entrar a la URL que en este caso era 127.0.0.1:8080 pero por el tiempo no pude lograr pensar en una forma de realizarlo, ya que al ejecutar el curl, el recolector de logs implementados en el makefile, nos ayuda para verificar desde donde proviene la solicitud, y tomando como base desde ahí podríamos empezar a verificar el tema del filtrado de clientes.