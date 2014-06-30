FROM centos 
MAINTAINER "Langdon White" <lwhite@fishjump.com>

RUN yum -y update; yum clean all
RUN yum -y install httpd; yum clean all
RUN echo "Apache" >> /var/www/html/index.html

EXPOSE 80

#RUN echo currentsMillies

RUN yum -y install ruby rubygems oniguruma oniguruma-devel ruby-devel gcc-c++ make libxml2 libxml2-devel libxslt libxslt-devel
RUN gem install bundler
RUN mkdir devopsdays-webby
RUN cd devopsdays-webby
WORKDIR /devopsdays-webby
ADD Gemfile  /devopsdays-webby/Gemfile
ADD Gemfile.lock /devopsdays-webby/Gemfile.lock

RUN bundle install

RUN rm /etc/httpd/conf.d/welcome.conf
ADD virt-host.conf /etc/httpd/conf.d/
ADD run-apache.sh /run-apache.sh
RUN chmod -v +x /run-apache.sh
CMD ["/run-apache.sh"]
