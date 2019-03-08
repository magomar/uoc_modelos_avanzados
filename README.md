# Entorno de ejecución para la asignatura de Modelos avanzados de minería de datos de la UOC

Las siguientes instrucciones sirven crear un entorno de ejecución para la asignatura de **Modelos avanzados de minería de datos**, la cual se basa en Jupyter Notebook sobre Python. Aunque sería posible gestionar el entorno utilizando `pip` como gestor de paquetes python, prefiero utilizar el gestor de paquetes y entorno virtuales `conda`, el cual viene incluido, junto con `pip`, tanto en **Anaconda** como en **Miniconda**.

Aunque ya existe una versión 3.7 de Python y la mayoría de librerías utilizadas son compatibles con dicha versión, **TensorFlow** no lo es, y como es necesario (o muy conveniente al menos) para la asignatura, vamos a crear un entorno basado en **Python 3.6**.

## Requisitos y enfoque

Como hemos comentado, el entorno de trabajo que necesitamos debe contener Vamos a preparar un entorno de trabajo para la asignatura utilizando el gestor de paquetes y entornos virtuales `conda`, el cual podemos encontrar tanto en Anaconda como en Miniconda. Como vamos a utilizar Python 3.6, debemos instalar una versión de Anaconda o Miniconda para Python 3, pues también existen versiones para Python 2.

Las instrucciones para instalar Anaconda o Miniconda pueden variar dependiendo del sistema operativo utilizado y de la distribución concreta.
A continuación incluyo los scripts necesarios para instalar Miniconda o Anaconda en Linux, para otros sistemas operativos remito a la página oficial.

```sh
cd ~/Downloads && \
wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh && \
bash Miniconda3-latest-Linux-x86_64.sh
```

Sugiero responder que sí cuando nos pregunté si queremos inicializar Miniconda3 (añadirá conda al `PATH` para que podamos ejecutarlo desde cualquier terminal).

La instalación de Anaconda es similar, solo cambia el archivo a descargar.

```sh
cd ~/Downloads/ && \
wget https://repo.anaconda.com/archive/Anaconda3-2018.12-Linux-x86_64.sh && \
sh Anaconda3-2018.12-Linux-x86_64.sh
```

Para trabajar con Jupyter Notebook con un kernel determinado (el kernel lo que permite ejecutar un lenguaje de programación en particular, en nuestro caso Python 3.6, pero también podría ser R, Julia, etc.) necesitamos, por un lado, el propio Jupyter Notebook, y por otro lado, un entorno con el kernel y las librerías que queramos utilizar compatibles con ese kernel. Una opción sería instalar todo en un único entorno virtual. Sin embargo, esto tiene el inconveniente de que para cada entorno de ejecución tendremos que instalar Jupyter Notebook, que ocupa bastante espacio de almacenamiento.

Un enfoque mucho menos redundante es tener un entorno virtual específico para ejecutar Jupyter Notebook, y un entorno virtual específico por cada kernel y conjunto de librerías que queramos utilizar. Este último es el enfoque que prefiero y recomiendo.

Y por último, cabe mencionar que el entorno que presento se basa en la versión de TensorFlow para CPU, y no en la versión para GPU. En el caso de querer utilizar la GPU para la ejecución de TensorFlow será necesario instalar `tensorflow-gpu`, pero previamente habrá que asegurarse de tener una GPU compatible e instalar los drivers y librerías específicas necesarias, como CUDA para NVIDIA.

## Entorno virtual para Juptyer Notebook

Este entorno lo uso únicamente para ejecutar Jupyter Notebook. Para ello necesitamos un entorno basado en Python. Hay que instalar el propio Jupyter Notebook (el paquete `jupyter`), y resulta muy práctica instalar un paquete adicional que permite detectar automáticamente los kernels disponibles en otros entornos de ejecución (`nb_conda_kernels`).

Podemos crear el entorno con ambos paquetes en un único paso con el siguiente script (notebook es el nombre que le doy al entorno):

```sh
conda create -n notebook python=3.7 nb_conda_kernels
```

Podemos comprobar que el entorno se ha creado correctamente activándolo y ejecutando Jupyter. Pero antes recomiendo situarse en el directorio de trabajo donde tengamos o queramos guardar los *notebooks*.

```sh
conda activate notebook && jupyter notebook
```

Tras ejecutar dicho comando veremos unas instrucciones, incluyendo una url que nos permitirá acceder a nuestro entorno Jupyter Notebook, y tendrá una forma similar a esta: <http://localhost:8888/?token=d0bf1cb7467893152151c5c7e3952236384f231ac567cb59>. Para copiar dicha url desde un terminal puedes usar la combinación de teclas <Ctrl +C>

Ya tenemos list el entorno para ejecutar Juptyer Notebook. A continuación vamos a crear un entorno específico para el kernel de Python 3.6 con las librerías necesarias para la asignatura. 

## Opción 1: Crear el entorno desde cero

Creamos un nuevo entorno sobre Python 3.6 y lo activamos

```sh
conda create -n uoc_modelos_avanzados python=3.6 && conda activate uoc_modelos_avanzados
```

Instalamos los paquetes necesarios para las tareas más comunes en minería de datos, lo que se conoce como el ecosistema **SciPy** (Scientific Python)

```sh
conda install numpy pandas scikit-learn matplotlib seaborn
```

Ese comando resultará en la instalación de los siguientes paquetes

```sh
package                    |            build
---------------------------|-----------------
cycler-0.10.0              |           py36_0          13 KB
kiwisolver-1.0.1           |   py36hf484d3e_0          83 KB
matplotlib-3.0.2           |   py36h5429711_0         6.5 MB
mkl_fft-1.0.10             |   py36ha843d7b_0         170 KB
mkl_random-1.0.2           |   py36hd81dba3_0         407 KB
numpy-1.15.4               |   py36h7e9f1db_0          47 KB
numpy-base-1.15.4          |   py36hde5b4d6_0         4.3 MB
pandas-0.24.0              |   py36he6710b0_0        11.1 MB
patsy-0.5.1                |           py36_0         380 KB
pyparsing-2.3.1            |           py36_0         105 KB
pyqt-5.9.2                 |   py36h05f1152_2         5.6 MB
python-dateutil-2.7.5      |           py36_0         275 KB
pytz-2018.9                |           py36_0         260 KB
scikit-learn-0.20.2        |   py36hd81dba3_0         5.7 MB
scipy-1.2.0                |   py36h7c811a0_0        17.8 MB
seaborn-0.9.0              |           py36_0         379 KB
sip-4.19.8                 |   py36hf484d3e_0         290 KB
statsmodels-0.9.0          |   py36h035aef0_0         9.0 MB
tornado-5.1.1              |   py36h7b6447c_0         663 KB
------------------------------------------------------------
                                        Total:        63.0 MB
```

Para la PEC3 de la asignatura, dedicada a los *métodos supervisados*, hay que implementar algunas redes neuronales, así es que necesitamos instalar algunos paquetes adicionales. En particular, se recomienda utilizar la api de `keras`, y `tensorflow` como motor de procesamiento o *backend*, aunque existen otras alternativas, como  `theano`.

```sh
conda install keras tensorflow
```

Como resultado se instalarán los siguientes paquetes:

```sh
package                    |            build
---------------------------|-----------------
_tflow_select-2.3.0        |              mkl           2 KB
absl-py-0.7.0              |           py36_0         156 KB
astor-0.7.1                |           py36_0          43 KB
c-ares-1.15.0              |       h7b6447c_1          98 KB
gast-0.2.2                 |           py36_0         138 KB
grpcio-1.16.1              |   py36hf8bcb03_1         1.1 MB
h5py-2.9.0                 |   py36h7918eee_0         1.2 MB
hdf5-1.10.4                |       hb1b8bf9_0         5.3 MB
keras-2.2.4                |                0           5 KB
keras-applications-1.0.6   |           py36_0          49 KB
keras-base-2.2.4           |           py36_0         457 KB
keras-preprocessing-1.0.5  |           py36_0          52 KB
libprotobuf-3.6.1          |       hd408876_0         4.1 MB
markdown-3.0.1             |           py36_0         107 KB
protobuf-3.6.1             |   py36he6710b0_0         616 KB
pyyaml-3.13                |   py36h14c3975_0         178 KB
tensorboard-1.12.2         |   py36he6710b0_0         3.1 MB
tensorflow-1.12.0          |mkl_py36h69b6ba0_0           4 KB
tensorflow-base-1.12.0     |mkl_py36h3c3e929_0        98.5 MB
termcolor-1.1.0            |           py36_1           7 KB
werkzeug-0.14.1            |           py36_0         423 KB
------------------------------------------------------------
                                        Total:       115.5 MB
```

Finalmente, para poder utilizar nuestro entorno con Jupyter Notebook deberemos de instalar el kernel de Python, `ipykernel`.

```sh
conda install ipykernel
```

Si hemos instalado `nb-conda-kernels` en el entorno con Jupyter Notebook, entonces no será necesario hacer nada más; sino habrá que añadir el kernel manualmente (ver [documentación](https://ipython.readthedocs.io/en/stable/install/kernel_install.html#kernels-for-different-environments)):

Con esto habremos terminado de configurar nuestro entorno de desarrollo para la asignatura de **Modelos Avanzados de Minería de Datos**.

## Opción 2: Crear el entorno a partir de un archivo con la especificación de las dependencias

Además de crear un entorno de forma manual, instalando los paquetes necesarios, `conda` nos ofrece la posibilidad de definir los paquetes que queremos instalar en un archivo de texto. Hay varias formas de generar y obtener dichos archivos, pero la más fácil es mediante el lenguaje YAML.

En este repositorio se proporciona un archivo YAML con la especificación básica del entorno: `uoc_modelos_avanzados.yml`, entonces para crear el entorno debemos hacer lo siguiente.

    conda env create -f uoc_modelos_avanzados.yml

Con fines informativos, se ha incluido también la especificación completa en el archivo `uoc_modelos_avanzados-full.yml`, pero el resultado final sería el mismo, ya que los paquetes no incluidos en la especificación básica son archivos básicos preinstalados en cualquier entorno conda, o son dependencias de las librerías instaladas.

## Opción 3: Imagen para contenedor Docker

Finalmente, se ha creado una imagen Docker con el entorno de desarrollo preinstalado. Dicha imagen se puede generar a partir del Dockerfile incluido en el directorio `docker` de este repositorio, o se puede descargar directamente desde [Docker Hub](https://cloud.docker.com/repository/docker/magomar/uoc-modelos-avanzados).

Las instrucciones se pueden consultar en el [README](https://github.com/magomar/uoc_modelos_avanzados/blob/master/docker/README.md) del directorio `docker`.

## Referencias

- Guía oficial sobre gestión de entornos con `conda`: [User guide > Manage environments](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html)
- Portal [Scipy.org](https://www.scipy.org/), dedicado al ecosistema de librerías Python para matemáticas, ciencia e ingeniería. Desde este portal podremos así mismo acceder a la información específica de la mayoría de las librerías que componen este ecosistema:
  - [numpy](http://docs.scipy.org/doc/numpy/)
  - [pandas](http://pandas.pydata.org/pandas-docs/stable/)
  - [scipy](http://docs.scipy.org/doc/scipy/reference/)
  - [simpy](http://docs.sympy.org/)
  - [matplotlib](http://matplotlib.org/contents.html)
  - [ipython](http://ipython.org/ipython-doc/stable/index.html)