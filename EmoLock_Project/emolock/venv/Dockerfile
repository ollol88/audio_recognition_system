FROM python:3.7

RUN apt-get update

RUN apt-get install -y \
            portaudio19-dev \
            libportaudio2  \
            portaudio19-dev \
            wget -y \
            gcc \
            libsndfile1 \
            install sox \
            --yes \
            g++


RUN pip install scikit-learn \
  pandas \
  numpy \
  xlrd \
  requests \ 
  scipy \
  sounddevice librosa \
  pyaudio \
  setuptools \
  Flask ap \
  seaborn \
  bokeh \
  panel \
  cffi \
  subprocess.run

CMD sudo apt-get install libsndfile1

COPY /src/templates /app
COPY /src/static /app
COPY src/ /app


WORKDIR /app
VOLUME /app


CMD python record