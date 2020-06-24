FROM centos:7
RUN yum -y install httpd httpd-devel zlib-devel openssl-devel curl-devel make gcc-c++ wget mariadb-devel && \
 cd /usr/local/src && \
 wget http://pyyaml.org/download/libyaml/yaml-0.1.7.tar.gz && \
 tar zxvf yaml-0.1.7.tar.gz && \
 cd yaml-0.1.7 && \
 ./configure && \
 make && \
 make install && \
 cd /usr/local/src && \
 wget https://ftp.ruby-lang.org/pub/ruby/2.4/ruby-2.4.2.tar.gz && \
 tar zxvf ruby-2.4.2.tar.gz && \
 cd ruby-2.4.2 && \
 ./configure && \
 make && \
 make install && \
 cd /usr/local/src && \
 wget https://rubygems.org/rubygems/rubygems-2.7.3.tgz && \
 tar zxvf rubygems-2.7.3.tgz && \
 cd rubygems-2.7.3 && \
 ruby setup.rb && \
 gem install passenger && \
 passenger-install-apache2-module && \
 passenger-install-apache2-module --snippet > /etc/httpd/conf.d/passenger.conf && \
 cd /usr/local/src && \
 wget --no-check-certificate https://tn123.org/mod_xsendfile/mod_xsendfile.c && \
 apxs -cia mod_xsendfile.c

RUN cd /usr/local && \
 wget "http://www.deco.vc/wp-content/plugins/download-monitor/download.php?id=20" --no-check-certificate -O deco-2.0.12.tar.gz && \
 tar xzvf deco-2.0.12.tar.gz && \
 cd deco && \
 gem install bundler --no-document --force && \
 bundle install && \
 cp /usr/local/deco/config/database.yml.sample /usr/local/deco/config/database.yml && \
 cp /usr/local/deco/config/environments/production.rb.sample /usr/local/deco/config/environments/production.rb && \
 bundle exec rake assets:precompile RAILS_ENV=production && \
 mkdir -p /var/deco/files && \
 chown -R apache:apache /var/deco/files && \
 chown -R apache:apache /usr/local/deco

COPY ./deco.conf /etc/httpd/conf.d/deco.conf

RUN ln -sf /dev/stderr /var/log/httpd/error_log

WORKDIR /usr/local/deco

CMD ["/usr/sbin/httpd", "-D", "FOREGROUND"]
