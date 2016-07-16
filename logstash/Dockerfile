FROM logstash:2.3.3
MAINTAINER sergioedo

#Set Time Zone
RUN echo "Europe/Madrid" | tee /etc/timezone && dpkg-reconfigure --frontend noninteractive tzdata

#Install Git & Ruby
RUN apt-get update && apt-get -y install git && apt-get -y install ruby-full

#Get memorize plugin and compile plugin
WORKDIR /opt/local/logstash
RUN git clone https://github.com/alcanzar/logstash-filter-memorize.git logstash-filter-memorize \
	&& cd logstash-filter-memorize && gem build logstash-filter-memorize.gemspec

#Install memorize plugin
WORKDIR /opt/local/logstash/bin
RUN plugin install /opt/local/logstash/logstash-filter-memorize/logstash-filter-memorize-0.9.2.gem

# Add config file by param
CMD ["logstash", "agent", "-f", "/var/local/logstash/conf/flexlm.conf", "-l","/var/local/logstash/log/ls.log", "-w", "1"]