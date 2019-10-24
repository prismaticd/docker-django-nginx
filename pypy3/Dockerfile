FROM pypy:3

MAINTAINER Prismatic Digital <>

RUN ln -s /usr/local/bin/pypy /usr/local/bin/python

RUN apt-key adv --no-tty --keyserver keyserver.ubuntu.com --recv-keys ABF5BD827BD9BF62 > /dev/null \
	&& echo "deb http://nginx.org/packages/debian/ stretch nginx" >> /etc/apt/sources.list \
	&& echo "deb http://ftp.debian.org/debian stretch-backports main " >> /etc/apt/sources.list.d/backports.list \
	&& apt-get update \
	&& apt-get install -y -t stretch-backports openssl libssl-dev \
	&& apt-get install -y ca-certificates nginx gettext-base \
        && apt-get install -y libev-dev \
        && apt-get install -y default-libmysqlclient-dev \
        && apt-get install -y python3-dev \
	&& rm -rf /var/lib/apt/lists/*
# forward request and error logs to docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log \
	&& ln -sf /dev/stderr /var/log/nginx/error.log
EXPOSE 80 443
# Finished setting up Nginx
RUN rm /etc/nginx/conf.d/default.conf

RUN python --version && nginx -v && pip --version
