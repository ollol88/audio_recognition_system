# Title:

EmoLock:Voice & emotion recognition system for personnel identification
 - Propulsion Academy Final Project DSWD-2019-09 for https://www.oto.ai/
 - Authors: Thibault Mattera & Lorenzo Verstraeten

## Install
We build a docker container with all the required installations. the structure of the project is the following:

 ###### emo
        - log
             - embeddings_temp.csv
        -src
             - static
             - templates
             - EMBEDDINGS_DATABASE
             - record
###### venv
        - Dockerfile


The same structured is provided in the folder "emo". The folder "Graph" contains files that we use for exploration and to test the AI technology we used.

Be sure to have docker installed in your machine.
The command to build and run the docker file are (for ubuntu):

docker build -t ds .

docker run -p 5000:5000 -it --rm -v $(pwd)/log:/log -ti --rm -v /dev/snd:/dev/snd --privileged --network=emolock ds

## Project description
We build a secure lock system for the OTO office so employees can unlock the door using a combination
 of an arbitrary text prompt and a predefined emotion. We use OTO's softwares only. The system requires
 a recording of an audio file as input (the recording is also contained in the docker). The audio is read as a
 a time series, filtered to eliminate noise and after processed through DeepTone (a deep neural network developed by
 OTO's AI team). The result is a matrix of embeddings. We use these embeddings to build speakers' and emotions' clusters. We do that using the database EMBEDDINGS_DATABASE (csv file containing all the embeddings with their corresponding labels), that was constructed using records of the two of us.

## Goals
Develop a proof of concept of speaker identification and emotion recognition. Create an easy-to-use UI and make the product ready for production (everything on device).

## Structure

The "dockerfile" contains all the requirements needed. The Python file "record"  is the main component of the project. The following functions are used:
- record_identification_median
   - it takes the embeddings produced by the model and compare with the one saved in the database, it returns the predictions for speaker identification and emotion recognition.


- record_processing
  - it takes the raw audio file, filter it through OTO's model for speech identification and return through DeepTone the matrix of embeddings for that audio.


- save_embeddings_to_database
 - it is used to store the new audio in the database


- random_words_generator
 - generate random words that the speaker will be asked to pronounce


 - visualize_embeddings_mean
   - used to output graphical predictions of the new audio for speaker identification


   -visualize_emotions
    - - used to output graphical predictions of the new audio for speaker emotions


The remaining part of the code uses these functions and Flask to interact with the user interface.

The video file "EmoLock_demo" shows how the interface looks like and which interactions the user can do.

The folders "static" and "templates" are used to render in html the outputs and the "log" folder to save temporary results.
