FROM logstash:2.1
MAINTAINER sergioedo

#Set Time Zone
RUN echo "Europe/Madrid" | tee /etc/timezone && dpkg-reconfigure --frontend noninteractive tzdata

#Install Git & Ruby
RUN apt-get update && apt-get -y install git && apt-get -y install ruby-full

#Get memorize plugin, fix gemspec and compile plugin
WORKDIR /var/local/logstash/plugins
RUN git clone https://github.com/alcanzar/logstash-filter-memorize.git logstash-filter-memorize
COPY logstash-filter-memorize.gemspec /var/local/logstash/plugins/logstash-filter-memorize
RUN	cd logstash-filter-memorize && gem build logstash-filter-memorize.gemspec

#Install memorize plugin
WORKDIR /opt/local/logstash/bin
RUN plugin install /var/local/logstash/plugins/logstash-filter-memorize/logstash-filter-memorize-0.9.1.gem

# Add config file by param
CMD ["logstash", "agent", "-f", "/var/local/logstash/conf/flexlm.conf", "-l","/var/local/logstash/log/ls.log", "-w", "1"]