# Entorno `conda` para la asignatura de Modelos avanzados de minería de datos de la UOC

Las siguientes instrucciones sirven tanto para **Anaconda** como para **Miniconda**, en ambos casos en su versión 3. Aunque ya existe una versión 3.7 de Python y la mayoría de librerías utilizadas son compatibles, tensorflow no lo es, por lo que vamos a realizar toda la instalación sobre **Python 3.6**.

## Opción 1: Crear el entorno desde cero

Creamos un nuevo entorno sobre Python 3.6 y lo activamos

    conda create -n uoc_modelos_avanzados python=3.7 && conda activate scipy

Y añadimos los paquetes necesarios para la mayoría de tareas de minería de datos y visualización

    conda install numpy pandas scikit-learn matplotlib seaborn

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

    conda install keras tensorflow

Copmo resultado se instalarán los siguientes paquetes:

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

Finalmente, si queremos utilizar nuestro entorno con **Jupyter notebook** deberemos de instalar el kernel de Python, `ipykernel`.

    conda install ipykernel

Con esto habremos terminado de configurar nuestro entorno de desarrollo para la asignatura de Modelos Avanzados de Minería de Datos con Python y Jupyter Notebook.


## Opción 2: Crear el entorno a partir de un archivo con la especificación de las dependencias

Además de crear un entorno de forma manual, instalando los paquetes necesarios, conda nos ofrece la posibilidad de definir los paquetes que queremos instalar en un archivo de texto. Hay varias formas de generar y obtener dichos archivos, pero la más fácil es mediante el lenguaje YAML.

Si nuestra especificación se encuentra en el archivo `uoc_modelos_avanzados.yml`, entonces para crear el entorno debemos hacer lo siguiente

    conda env create -f uoc_modelos_avanzados.yml

## Referencias

- Guía oficial sobre gestión de entornos con `conda`: [User guide > Manage environments](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html)
- Portal [Scipy.org](https://www.scipy.org/), dedicado al ecosistema de librerías Python para matemáticas, ciencia e ingeniería. Desde este portal podremos así mismo acceder a la información específica de la mayoría de las librerías que componen este ecosistema:
  - [numpy](http://docs.scipy.org/doc/numpy/)
  - [pandas](http://pandas.pydata.org/pandas-docs/stable/)
  - [scipy](http://docs.scipy.org/doc/scipy/reference/)
  - [simpy](http://docs.sympy.org/)
  - [matplotlib](http://matplotlib.org/contents.html)
  - [ipython](http://ipython.org/ipython-doc/stable/index.html)