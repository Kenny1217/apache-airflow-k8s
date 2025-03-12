FROM python:3.12-bookworm

ARG AIRFLOW_USER="airflow"
ARG AIRFLOW_HOME_DIRECTORY="/usr/local/$AIRFLOW_USER"
ARG AIRFLOW_VERSION="2.10.5"
ARG PYTHON_VERSION="3.12"

ENV AIRFLOW_HOME="$AIRFLOW_HOME_DIRECTORY"

USER root

RUN useradd --shell /bin/bash -d "$AIRFLOW_HOME" -m -u 1001 "$AIRFLOW_USER"

RUN apt-get update && apt-get upgrade && apt-get install -y --no-install-recommends \
    curl \
    git \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*


RUN pip3 install "apache-airflow[amazon,cnfc.kubernetes,postgres,sftp,slack,ssh]==$AIRFLOW_VERSION" \
    --constraint "https://raw.githubusercontent.com/apache/airflow/constraints-$AIRFLOW_VERSION/constraints-$PYTHON_VERSION.txt" \
    --no-cache-dir

RUN chown -R "$AIRFLOW_USER": "$AIRFLOW_USER_HOME"

EXPOSE 8080

USER $AIRFLOW_USER

WORKDIR "$AIRFLOW_USER_HOME"

#ENTRYPOINT [ "./entrypoint.sh" ]