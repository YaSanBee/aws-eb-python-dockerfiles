# Copyright 2016 YaSanBee
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#    http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

# YaSanBee/aws-eb-python-dockerfiles
#
# VERSION 0.0.1

FROM    python:3.4.2

MAINTAINER    YaSanBee

WORKDIR    /var/app

RUN    pip install --download-cache /src uwsgi

RUN    useradd uwsgi -s /bin/false
RUN    mkdir /var/log/uwsgi
RUN    chown -R uwsgi:uwsgi /var/log/uwsgi

ONBUILD    ADD    . /var/app
ONBUILD    RUN    if [ -f /var/app/requirements.txt ]; then pip install -r /var/app/requirements.txt; fi

ENV    UWSGI_NUM_PROCESSES    1
ENV    UWSGI_NUM_THREADS      15
ENV    UWSGI_UID              uwsgi
ENV    UWSGI_GID              uwsgi
ENV    UWSGI_LOG_FILE         /var/log/uwsgi/uwsgi.log

EXPOSE    8080

ADD    uwsgi-start.sh /

ENTRYPOINT    ["/uwsgi-start.sh"]
