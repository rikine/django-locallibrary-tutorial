# pull official base image
FROM python:3.9.5-slim

RUN apt-get update \
    && apt-get -y install libpq-dev gcc \
    && pip install psycopg2

# set work directory
WORKDIR /usr/src/app

# set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# create directory for the app user
RUN mkdir -p /home/app

# install dependencies
RUN pip install --upgrade pip
COPY ./requirements.txt .
RUN pip install -r requirements.txt

# create the appropriate directories
ENV HOME=/home/app
ENV APP_HOME=/home/app/web
RUN mkdir $APP_HOME
RUN mkdir $APP_HOME/staticfiles
WORKDIR $APP_HOME

# copy project
COPY . $APP_HOME
