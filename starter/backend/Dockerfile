FROM public.ecr.aws/docker/library/python:3.10-alpine
ENV FLASK_RUN_HOST=0.0.0.0

WORKDIR /
RUN adduser -u 1000 -D app
RUN apk update && \
  apk add \
  pcre \
  pcre-dev \
  build-base \
  gcc \
  linux-headers \
  openssl \
  libffi-dev \
  && pip install pipenv

RUN mkdir -p /var/www/app && mkdir /app

ENV CFLAGS="-Wno-error=incompatible-pointer-types"
RUN cd /app && pip install flask uwsgi==2.0.26 flask-cors

COPY . /app

CMD uwsgi --http :5000 --master --enable-threads -s /var/www/app/app.sock --manage-script-name --mount /=app:app