FROM centos:7.9.2009

MAINTAINER APMOSYS_zunny_1

WORKDIR /mnt

#ENV container docker

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

RUN yum -y update; yum -y install vim wget telnet epel-release zip unzip net-tools httpd mod_ssl; yum update -y; yum clean all;


RUN yum install -y http://repo.openfusion.net/centos7-x86_64/openfusion-release-0.8-1.of.el7.noarch.rpm; yum install -y http://repo.openfusion.net/centos7-x86_64/perl-namespace-clean-0.27-1.of.el7.noarch.rpm; yum clean all

RUN yum install -y perl-Moo   "perl(Text::CSV_XS)" "perl(Archive::Zip)" "perl(Crypt::SSLeay)" "perl(IO::Socket::SSL)" "perl(LWP::UserAgent)" "perl(Net::DNS)" "perl(Net::LDAP)" "perl(Template)" "perl(XML::LibXML)" "perl(XML::LibXSLT)" "perl(XML::Parser)" "perl(YAML::XS)" "perl(Authen::NTLM)" "perl(Mail::IMAPClient)" "perl(JSON::XS)" "perl(Encode::HanExtra)"  "perl(DBD::Pg)" "perl(Crypt::Eksblowfish::Bcrypt)" perl-core procmail "perl(DBD::mysql)" "perl(Authen::NTLM)" "perl(ModPerl::Util)" "perl(CSS::Minifier::XS)" "perl(JavaScript::Minifier::XS)" "perl(Spreadsheet::XLSX)"


RUN yum install -y https://download.znuny.org/releases/RPMS/rhel/7/znuny-6.2.2-01.noarch.rpm; yum update -y; yum clean all

RUN echo $? yes | perl -MCPAN -e 'install Template::Stash::XS'
RUN echo $? yes | perl -MCPAN -e 'install  Net::SMTP'
RUN echo $? yes | perl -MCPAN -e 'install  DateTime::TimeZone'
RUN echo $? yes | perl -MCPAN -e 'install  DateTime'
RUN echo $? yes | perl -MCPAN -e 'install  Net::LDAP' 
RUN echo $? yes | perl -MCPAN -e 'install  Mail::IMAPClient'
RUN echo $? yes | perl -MCPAN -e 'install  IO::Socket::SSL'
#RUN  mkdir /run/httpd
RUN chown root:apache /run/httpd
RUN  echo > /etc/httpd/logs/error_log


RUN echo "ServerName localhost" >> /etc/httpd/conf/httpd.conf
RUN  sed -i 's/SSLEngine on/SSLEngine off/g' /etc/httpd/conf.d/ssl.conf
RUN chown -R root:apache /opt/otrs
EXPOSE 82
EXPOSE 443
CMD ["/usr/sbin/init"] 
CMD ["/usr/sbin/httpd","-D","FOREGROUND"]
