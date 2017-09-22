FROM tensorflow/tensorflow:latest-devel-gpu-py3
ARG PORT=8888
ENV PORT=$PORT


ENV NB_USER keras
ENV NB_UID 1000

RUN useradd -m -s /bin/bash -N -u $NB_UID $NB_USER && \
    mkdir -p /code && \
    chown keras /code && \
    mkdir -p /home/keras/.jupyter && \
    chown -R keras /home/keras/.jupyter


RUN pip install keras

USER keras
COPY jupyter_notebook_config.json /home/keras/.jupyter/
WORKDIR /code

EXPOSE 8888

CMD jupyter notebook --port=$PORT --ip=0.0.0.0