# Imagen **docker** con para la asignatura de Modelos Avanzados de Minería de Datos, del Máster de Ciencia de Datos de la UOC

Esta imagen ofrece un entorno Python con todo lo necesaria para completar con éxito la asignatura de **Modelos Avanzados de Minería de Datos** (código M2.855), incluida en el [**Máster de Ciencia de Datos**](https://estudios.uoc.edu/es/masters-universitarios/data-science/presentacion) de la **UOC**.

Esta imagen para docker está basada en la imagen oficial de **Miniconda**, versión reducida de la plataforma [Anaconda](https://www.anaconda.com/) que únicamente incluye su sistema de gestor de paquetes, entornos y dependencias, [Conda](https://conda.io/en/latest/). Se ha escogido dicha imagen por ser una imagen oficial y porque ofrece un buen equilibrio entre tamaño, funcionalidad incluida y facilidad de uso. Otra opción era utilizar una imagen oficial de Jupyter Notebook, pero las mismas resultan muy abultadas en tamaño, complejas, y con mucha funcionalidad innecesaria.

Los interesados pueden consultar los detalles de la imagen base en su repositorio oficial en [Docker Hub](https://hub.docker.com/r/continuumio/miniconda3). Básicamente, se trata de un distribución **Debian** con el añadido del gestor de paquetes **Conda**, en su versión **Miniconda**. Es una distribución de tamaño moderado, bastante más pesada que una distribución basada en **Alpine**, pero mucho más ligera que una distribución basada en **Ubuntu**. No me parece muy útil para nuestros fines tirar de una distribución super ligera porque los paquetes que hay que instalar son mucho más pesados en comparación, especialmente la plataforma Jupyter Notebook.

Sobre la base de la distribución de Debian + Miniconda vamos a añadir, por un lado, la plataforma Jupyter Notebook, y por otro lado los paquetes necesarios para la asignatura, las cuales combinan las librerías más habituales usadas en *Minería de Datos* y *Aprendizaje Automático*, como las librerías más utilizadas para Deep Learning.

En concreto, se incluyen por un lado las librerías más habituales del ecosistema [SciPy](https://www.scipy.org/), con el añadido de la librería seaborn para visualización:

    - numpy
    - pandas
    - scipy
    - scikit-learn
    - matplotlib
    - seaborn

Por otro lado, para Deep Learning se incluyen [TensorFlow](https://www.tensorflow.org/) y la API de [Keras](https://keras.io/):

    - tensorflow
    - keras

La versión usada de Python es la 3.6, pues la 3.7 no es oficialmente compatible con TensorFlow

Puedes construir la imagen tu mismo a partir del Dockerfile proporcionado en este repositorio de GitHub, o la puedes descargar lista para su ejecución desde [Docker Hub](https://cloud.docker.com/u/magomar/repository/docker/magomar/uoc-modelos-avanzados) with:

    docker pull magomar/uoc-modelos-avanzados:latest

Una vez obtenida la imagen la puedes ejecutar con

    docker run --rm -p 8888:8888 --name notebook magomar/uoc-modelos-avanzados

Esta imagen utiliza `/opt/notebooks` como directorio inicial para el entorno de Jupyter Notebook, así es que resulta conveniente es montar un volumen con esa ruta, o enlazarlo con un directorio local. Por ejemplo, para enlazarlo con tu directorio actual puedes usar el siguiente comando:

    docker run --rm -p 8888:8888 -v ${PWD}:/opt/notebooks --name notebook magomar/uoc-modelos-avanzados

Deberás copiar el *token* desde el terminal y usarlo para acceder al notebook desde tu navegador, en la dirección  <http://localhost:888>