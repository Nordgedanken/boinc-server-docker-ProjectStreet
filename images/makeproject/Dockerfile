FROM debian:jessie

MAINTAINER Marius Millea <mariusmillea@gmail.com>

# install necessary packages
RUN apt-get update && apt-get install -y \
        curl \
        dh-autoreconf \
        git \
        libcurl4-gnutls-dev \
        libmysqlclient-dev \
        libssl-dev \
        m4 \
        make \
        php5-cli \
        php5-mysql \
        pkg-config \
        python \
        python-mysqldb


# get source and compile server
COPY boinc /root/boinc
RUN cd /root/boinc && ./_autosetup && ./configure --disable-client --disable-manager && make

# build configuration
ENV USER=root PROJHOME=/root/project

# make project
RUN cd /root/boinc/tools \
    && ./make_project --url_base http://ProjectStreet.dynu.com \
                      --project_host ProjectStreet \
                      --db_host mysql \
                      --db_user root \
                      --no_db \
                      --no_query \
                      --project_root $PROJHOME \
                      ProjectStreet \
    && sed -i -e 's/Deny from all/Require all denied/g' \
           -e 's/Allow from all/Require all granted/g' \
           -e '/Order/d' \
           -e '$a\ ProxyRequests Off' \
           -e '$a\ ProxyPreserveHost On' \
           -e '$a\ ProxyVia Full' \
           -e '$a\ <Proxy *>' \
           -e '$a\ Require all granted' \
           -e '$a\ </Proxy>' \
           -e '$a\ <Location /auth>' \
           -e '$a\ ProxyPass http://127.0.0.1:8080/auth' \
           -e '$a\ ProxyPassReverse http://127.0.0.1:8080/auth' \
           -e '$a\ </Location>' $PROJHOME/ProjectStreet.httpd.conf \
    && echo 'admin:$apr1$1WD6Y5z3$S.uU54R1EuMiczW6xl7JE.' > $PROJHOME/html/ops/.htpasswd \
    && rm -r $PROJHOME/log_ProjectStreet \
    && sed -i -e '$a\ RedirectMatch ^/$ /ProjectStreet/' /etc/apache2/apache2.conf

# project files
RUN mkdir $PROJHOME/html/stats_archive
COPY db_dump_spec.xml $PROJHOME/
COPY html $PROJHOME/html
COPY bin $PROJHOME/bin

# finish up
WORKDIR $PROJHOME
COPY postbuild.py /root/
CMD /root/postbuild.py
