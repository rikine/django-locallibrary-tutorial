# pull official base image
FROM python:3.9.6-alpine

RUN apk update \
    && apk add postgresql-dev gcc python3-dev musl-dev

# set work directory
WORKDIR /usr/src/app

# set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# create directory for the app user
RUN mkdir -p /home/app

RUN addgroup -S app && adduser -S app -G app

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

RUN chown -R app:app $APP_HOME

USER app