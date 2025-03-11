FROM python:3.12-bookworm

ENV AIRFLOW_USER="airflow"
ENV AIRFLOW_USER_HOME="/usr/local/$AIRFLOW_USER"

USER root

RUN useradd --shell /bin/bash -d "$AIRFLOW_USER_HOME" -m -u 1001 "$AIRFLOW_USER"

RUN apt-get update && apt-get upgrade && apt-get install -y --no-install-recommends \
    curl \
    git \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN chown -R "$AIRFLOW_USER": "$AIRFLOW_USER_HOME"

USER $AIRFLOW_USER

WORKDIR "$AIRFLOW_USER_HOME"