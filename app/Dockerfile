# syntax=docker/dockerfile:1.4
FROM --platform=$BUILDPLATFORM python:3.12-slim-buster AS builder

WORKDIR /app

COPY requirements.txt /app
RUN --mount=type=cache,target=/root/.cache/pip \
    pip3 install -r requirements.txt

COPY . /app

ENTRYPOINT ["python3"]
CMD ["app.py","--port=3000"]

FROM builder as dev-envs

RUN <<EOF
apk update
apk add git
EOF

RUN <<EOF
addgroup -S docker
adduser -S --shell /bin/bash --ingroup docker vscode
EOF
# install Docker tools (cli, buildx, compose)
COPY --from=gloursdocker/docker / /



# # syntax=docker/dockerfile:1.4
# FROM python:3.8-slim-buster

# WORKDIR /app

# COPY requirements.txt /app
# RUN pip3 install -r requirements.txt

# COPY . /app

# ENTRYPOINT ["python3"]
# CMD ["app.py"]


# # # syntax=docker/dockerfile:1

# # FROM python:3.8-slim-buster

# # WORKDIR /python-docker

# # COPY requirements.txt requirements.txt
# # RUN pip3 install -r requirements.txt

# # COPY . .

# # CMD [ "python3", "-m" , "flask", "run", "--host=0.0.0.0"]
