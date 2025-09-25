#Dockerfile
FROM python:3.10

RUN mkdir /src
RUN mkdir /static

WORKDIR /src


RUN apt-get update && apt-get install -y gettext libgettextpo-dev zlib1g libjpeg-dev

ENV PYTHONUNBUFFERED=1
RUN python3 -m pip install --upgrade pip

COPY ./requirements.txt .
RUN pip install -r requirements.txt
#RUN python -m pip install uwsgi
COPY . /src/

## Copy the wait-for-it script
#COPY ./wait-for-it.sh /wait-for-it.sh
#RUN chmod +x /wait-for-it.sh
# Copy wait-for-it script và cấp quyền
COPY ./wait-for-it.sh /usr/local/bin/wait-for-it.sh
RUN chmod +x /usr/local/bin/wait-for-it.sh

# Copy entrypoint script và cấp quyền
COPY ./docker-entrypoint.sh /usr/local/bin/docker-entrypoint.sh
RUN chmod +x /usr/local/bin/docker-entrypoint.sh

ENV PYTHONPATH=/src/src

#COPY docker-entrypoint.sh /src/
#RUN chmod +x ./docker-entrypoint.sh
#
#ENTRYPOINT ["./docker-entrypoint.sh"]

ENTRYPOINT ["/usr/local/bin/docker-entrypoint.sh"]