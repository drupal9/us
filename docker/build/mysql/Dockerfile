FROM mysql:5.7


## Basic tools
#RUN apt-get update -y && \
#    apt-get upgrade -y && \
#    apt-get install -y procps \
#            bash \
#            curl \
#            wget \
#            ca-certificates \
#            vim \
#            git \
#            nano

RUN chown -R mysql:root /var/lib/mysql/

ARG MYSQL_ROOT_PASSWORD

RUN /etc/init.d/mysql start && \
         mysql -u root -p$MYSQL_ROOT_PASSWORD -e "GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY '$MYSQL_ROOT_PASSWORD';FLUSH PRIVILEGES;"

EXPOSE 3306
