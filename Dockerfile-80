FROM mysql:8.0

ENV MYSQL_ROOT_PASSWORD rootpass
ENV MYSQL_DATABASE test
ENV MYSQL_USER testuser
ENV MYSQL_PASSWORD testpass

COPY ./config/my.conf /etc/mysql/conf.d/my.cnf
