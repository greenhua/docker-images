FROM ubuntu:16.04

RUN apt -y update
RUN  apt -y install php apache2 wget libapache2-mod-php7.0
RUN wget -O /root/installer https://getcomposer.org/installer
RUN /usr/bin/php /root/installer  --install-dir=/usr/bin

RUN echo 'mysql-server mysql-server/root_password password root' | debconf-set-selections
RUN echo  'mysql-server mysql-server/root_password_again password root' | debconf-set-selections

#RUN  DEBIAN_FRONTEND=noninteractive apt install -y  mysql-server supervisor
RUN  apt install -y  mysql-server supervisor


RUN mkdir /var/run/mysqld
RUN chmod 777 /var/run/mysqld




ADD etc/supervisor/conf.d/supervisord.conf /etc/supervisor/conf.d/supervisord.conf
ADD etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/000-default.conf
ADD etc/apache2/apache2.conf /etc/apache2/apache2.conf


# expose mysql port
EXPOSE 22 3306


CMD ["/usr/bin/supervisord"]
