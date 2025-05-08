FROM python:3.12-slim
WORKDIR /api

#ARG MODELS_PORT
#ENV MODELS_PORT=${MODELS_PORT}


RUN apt-get update
RUN apt-get install ffmpeg libsm6 libxext6  -y
RUN yes | ln -s /usr/bin/python3 /usr/bin/python && python -m pip install poetry
RUN python --version
ARG CODEARTIFACT_TOKEN
RUN poetry config http-basic.aws aws ${CODEARTIFACT_TOKEN} > /dev/null 2>&1

COPY pyproject.toml poetry.lock /api/
RUN poetry env use 3.12   ############### auto to line to eixame prosthesei me tou Jouke
                          ####otan eixa ena error sto docker build pou elege oti h python 3.11 den kanei, enw sto docker kai sto env eixa mono 3.12 ...
RUN poetry config virtualenvs.create false && poetry install --no-interaction

#########epishs me to Jouke vazoume twra edw to COPY . /api gia na einai pio grhgoro kathe fora to build kai na vlepei ta pio panw grhgora ap to cache..
COPY . /api

# CUDA
#RUN yes | pip install torch==1.11.0+cu113 torchvision==0.12.0+cu113 torchaudio==0.11.0 --extra-index-url https://download.pytorch.org/whl/cu113 --default-timeout=3600
#RUN yes | pip install torch==1.11.0+cpu torchvision==0.12.0+cpu torchaudio==0.11.0 segmentation_models_pytorch pytorch_lightning --extra-index-url https://download.pytorch.org/whl/cpu

#CMD uvicorn app:app --host 0.0.0.0 --port ${MODELS_PORT}
CMD uvicorn app:app --host 0.0.0.0 --port 8002
