FROM python:3.10-slim

RUN adduser --disabled-password --gecos "" app

RUN apt-get update && \
    apt-get install -y build-essential && \
    rm -rf /var/lib/apt/lists/* && \
    pip install pipenv

RUN mkdir -p /var/www/app && mkdir /app

COPY Pipfile /app

RUN cd /app && pipenv install --system --skip-lock

COPY . /app/backend

WORKDIR /app

USER app

CMD ["uwsgi", "--http", "0.0.0.0:5000", "--module", "backend:app"]