FROM amazonlinux:2017.03

RUN yum update -y && \
    yum clean all
## httpd
RUN yum install -y httpd && \
    yum clean all

## service on boot
RUN chkconfig httpd on

### php70 prepare
## epel
RUN yum install -y epel-release && \
    yum clean all
RUN sed -i -e "s/enabled *= *1/enabled=0/g" /etc/yum.repos.d/epel.repo

## remi
RUN yum install -y http://rpms.famillecollet.com/enterprise/remi-release-6.rpm && \
    yum clean all
RUN sed -i -e "s/enabled *= *1/enabled=0/g" /etc/yum.repos.d/remi.repo

## php70 install
# need library
RUN yum install -y --enablerepo=epel --disablerepo=amzn-main libwebp && \
    yum clean all
RUN yum install -y libtiff libXpm libpng libwebp freetype fontconfig compat-libtiff3 libevent libtool-ltdl libxslt libedit compat-gmp4 && \
    yum clean all

#install gd-last
RUN yum install -y --enablerepo=remi,remi-php70,epel --disablerepo=amzn-main gd-last && \
    yum clean all

# install php70
RUN yum install -y --enablerepo=remi-php70,remi,epel --disablerepo=amzn-main php php-cli php-common php-gd php-mbstring php-mcrypt php-mysqlnd php-pdo php-pecl-igbinary php-pecl-memcached php-process php-xml php-gmp mod_ssl && \
    yum clean all

#RUN echo "It Works, maybe" >> /var/www/html/index.html

# strat httpd
#RUN /etc/rc.d/init.d/httpd start


####create NEXT-IC Project####
#RUN useradd ec2-user
#RUN rm -rf cgi-bin error icons html
#ENTRYPOINT ["/usr/sbin/httpd","-DFOREGROUND"]