FROM centos:7.9.2009

MAINTAINER apmosys_nextcloud__

RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == \
systemd-tmpfiles-setup.service ] || rm -f $i; done); \
rm -f /lib/systemd/system/multi-user.target.wants/*;\
rm -f /etc/systemd/system/*.wants/*;\
rm -f /lib/systemd/system/local-fs.target.wants/*; \
rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
rm -f /lib/systemd/system/basic.target.wants/*;\
rm -f /lib/systemd/system/anaconda.target.wants/*;
VOLUME [ "/sys/fs/cgroup" ]

RUN yum -y update; yum install -y centos-release-scl; yum -y install vim wget telnet  yum-utils bzip2 zip unzip net-toolis httpd mod_ssl; yum update -y; yum clean all;

RUN yum install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
RUN  yum install -y http://rpms.famillecollet.com/enterprise/remi-release-7.rpm

RUN yum-config-manager --disable remi-php72
RUN yum-config-manager --enable remi-php74

RUN yum -y install vim httpd php php-cli php-mysqlnd php-zip php-devel php-gd php-mcrypt php-mbstring php-curl php-xml php-pear php-bcmath php-json php-pdo php-pecl-apcu php-pecl-apcu-devel php-ldap



RUN cd /tmp
RUN  wget  https://download.nextcloud.com/server/releases/latest.tar.bz2

RUN tar -jxvf latest.tar.bz2

RUN mv nextcloud /var/www/html/
RUN mkdir /var/www/html/nextcloud/data

RUN chown apache:apache -R /var/www/html/nextcloud/data
RUN chown -R apache:apache /var/www/html/nextcloud/

RUN  echo "<VirtualHost *:80>"  >> /etc/httpd/conf/httpd.conf
RUN  echo ServerAdmin nextcloud >> /etc/httpd/conf/httpd.conf
RUN  echo DocumentRoot /var/www/html/nextcloud >> /etc/httpd/conf/httpd.conf
RUN  echo ServerName dummy-host2.example.com  >>  /etc/httpd/conf/httpd.conf
RUN  echo ErrorLog "/var/log/httpd/dummy-host2.example.com-error_log"  >> /etc/httpd/conf/httpd.conf
RUN  echo CustomLog "/var/log/httpd/dummy-host2.example.com-access_log" common >> /etc/httpd/conf/httpd.conf
RUN  echo "</VirtualHost>" >> /etc/httpd/conf/httpd.conf












#RUN  mkdir /run/httpd
RUN chown root:apache /run/httpd
RUN  echo > /etc/httpd/logs/error_log







EXPOSE 8080
CMD ["/usr/sbin/init"]
CMD ["/usr/sbin/httpd","-D","FOREGROUND" ]

