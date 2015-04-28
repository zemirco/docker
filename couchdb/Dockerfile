
FROM ubuntu:14.10

MAINTAINER Mirco Zeiss <mirco.zeiss@gmail.com>

# update repository
RUN \
  apt-get update && \
  apt-get upgrade -y && \
  apt-get install -y \
    fail2ban \
    ufw \
    build-essential \
    erlang-base-hipe \
    erlang-dev \
    erlang-manpages \
    erlang-eunit \
    erlang-nox \
    libicu-dev \
    libmozjs185-dev \
    libcurl4-openssl-dev

# install couchdb 1.6.1
RUN wget http://apache.mirror.iphh.net/couchdb/source/1.6.1/apache-couchdb-1.6.1.tar.gz
RUN tar -xvzf apache-couchdb-*
WORKDIR apache-couchdb-*
RUN ./configure
RUN make && sudo make install

# create couchdb user
RUN adduser --disabled-login --disabled-password --no-create-home --gecos "" couchdb

# uncomplicated firewall
# allow ssh
RUN ufw allow 22
# allow CouchDB HTTP port
RUN ufw allow 5984
# allow CouchDB HTTPS port
RUN ufw allow 6984
# activate firewall
RUN ufw enable

# change ownership of couchdb directories
RUN chown -R couchdb:couchdb /usr/local/var/lib/couchdb
RUN chown -R couchdb:couchdb /usr/local/var/log/couchdb
RUN chown -R couchdb:couchdb /usr/local/var/run/couchdb
RUN chown -R couchdb:couchdb /usr/local/etc/couchdb

# change permission of couchdb directories
RUN chmod 0770 /usr/local/var/lib/couchdb
RUN chmod 0770 /usr/local/var/log/couchdb
RUN chmod 0770 /usr/local/var/run/couchdb
RUN chmod 0770 /usr/local/etc/couchdb/*.ini
RUN chmod 0770 /usr/local/etc/couchdb/*.d

# setup logrotate and autostart
RUN ln -s /usr/local/etc/logrotate.d/couchdb /etc/logrotate.d/couchdb
RUN ln -s /usr/local/etc/init.d/couchdb /etc/init.d

RUN /etc/init.d/couchdb restart
