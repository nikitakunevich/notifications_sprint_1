FROM python:3.9.1-slim

ENV PYTHONUNBUFFERED 1

ARG UID=2000
ARG GID=2000
ARG USER=fastapi
ARG GROUP=application
ARG ROOT_APP=/app

RUN groupadd -g $GID $GROUP && \
    useradd -u $UID -g $GID -m $USER && \
    mkdir $ROOT_APP

COPY api/Pipfile $ROOT_APP/Pipfile
COPY api/Pipfile.lock $ROOT_APP/Pipfile.lock

WORKDIR $ROOT_APP
RUN pip install pipenv && \
    pipenv install --system --ignore-pipfile

COPY api/src $ROOT_APP/

RUN chown -R $USER:$GROUP $ROOT_APP

USER $USER
ENTRYPOINT ["uvicorn", "main:app", "--port", "8000", "--host", "0.0.0.0"]
