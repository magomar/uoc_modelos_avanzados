FROM continuumio/miniconda3:latest
# $ docker build . -t magomar/uoc-modelos-avanzados:latest
# $ docker push magomar/uoc-modelos-avanzados:latest
# $ docker run --rm -it -p 8888:8888 magomar/uoc-modelos-avanzados
# $ docker run --rm -it -p 8888:8888 -v ${PWD}:/opt/notebooks magomar/uoc-modelos-avanzados

LABEL maintainer = "Mario Gómez <magomar@gmail.com>"
LABEL build_date = "2019-02-04"

# Install packages: we install tensorflow first because it would probably downgrade some packages
RUN conda install -yq tensorflow \
    keras \
    numpy \
    pandas \
    scipy \
    scikit-learn \
    matplotlib \
    seaborn \
    jupyter && \
    conda clean -tipsy && \
    mkdir /opt/notebooks && \
    jupyter notebook --generate-config && \
    echo "c.NotebookApp.notebook_dir = '/opt/notebooks'" >> ~/.jupyter/jupyter_notebook_config.py && \
    echo "c.NotebookApp.ip = '0.0.0.0'" >> ~/.jupyter/jupyter_notebook_config.py && \
    echo "c.NotebookApp.port = 8888" >> ~/.jupyter/jupyter_notebook_config.py && \
    echo "c.NotebookApp.open_browser = False" >> ~/.jupyter/jupyter_notebook_config.py && \
    echo "c.NotebookApp.allow_root = True" >> ~/.jupyter/jupyter_notebook_config.py

VOLUME "/opt/notebooks"

# Add Tini
ENV TINI_VERSION v0.18.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /tini
RUN chmod +x /tini
ENTRYPOINT ["/tini", "--"]

EXPOSE 8888

CMD ["/bin/bash", "-c", "jupyter notebook"]
