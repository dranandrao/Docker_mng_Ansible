FROM ubuntu
#Setting proxy.
ENV http_proxy http://172.16.19.10:80/
ENV https_proxy https://172.16.19.10:80/
RUN apt-get update 

# MySQL
ENV MYSQL_PWD Pwd123
RUN echo "mysql-server mysql-server/root_password password $MYSQL_PWD" | debconf-set-selections
RUN echo "mysql-server mysql-server/root_password_again password $MYSQL_PWD" | debconf-set-selections
RUN apt-get -y install mysql-server
ENTRYPOINT service mysql start && /bin/bash
EXPOSE 3306