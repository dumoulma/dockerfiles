FROM python:3.6
LABEL maintainer="Jose Rivera <jose@launchpadrecruits.com>"

ENV MLFLOW_VERSION 1.3.0
ENV BACKEND_URI db_type://<user_name>:<password>@<host>:<port>/<database_name>
ENV TERM linux
ENV BUCKET bucket

RUN pip install mlflow==$MLFLOW_VERSION

RUN mkdir -p /mlflow/

ADD extra-requirements.txt /mlflow/

WORKDIR /mlflow/

RUN pip install -r extra-requirements.txt

EXPOSE 5000

CMD mlflow server \
  --backend-store-uri ${BACKEND_URI} \
  --default-artifact-root s3://${BUCKET}/mlflow-artifacts \
  --host 0.0.0.0

# # If access logs needed:
# CMD mlflow server \
#     --file-store /mlflow \
#     --default-artifact-root s3://${BUCKET}/mlflow-artifacts \
#     --host 0.0.0.0 --gunicorn-opts "--access-logfile -"
