FROM        python:3.4.2

MAINTAINER        YaSanBee

WORKDIR        /var/app

RUN        pip install --download-cache /src uwsgi

RUN        useradd uwsgi -s /bin/false
RUN        mkdir /var/log/uwsgi
RUN        chown -R uwsgi:uwsgi /var/log/uwsgi

ONBUILD    ADD        ./app /var/app
ONBUILD    RUN        if [ -f /var/app/requirements.txt ]; then pip install -r /var/app/requirements.txt; fi

ENV        UWSGI_NUM_PROCESSES    1
ENV        UWSGI_NUM_THREADS      15
ENV        UWSGI_UID              uwsgi
ENV        UWSGI_GID              uwsgi
ENV        UWSGI_LOG_FILE         /var/log/uwsgi/uwsgi.log

EXPOSE        8080

ADD        uwsgi-start.sh /

ENTRYPOINT        ["/uwsgi-start.sh"]
