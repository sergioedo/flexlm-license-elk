# flexlm-license-elk
Analize flexlm license files with ELK stack.

## Getting Started

You will need Logstash for extracting information from license files and process it into diferent ways:

* Text files: in a custom format you could adjust in flexlm.conf, you can analize with any software that processes text.
* ElasticSearch: indexing data into Elastic, you can make querys with Elastic API or build dashboards with Kibana.

Follow nexts steps to make it run.

### Prerequisities

For run in a virtual environment, you will need:

* Virtualbox
* Vagrant

If you have a Logstash instance or and ELK stack, you only have to adjust input and output in conf/flexlm.conf and launch logstash:

```
logstash -f <path_to_file>/flexlm.conf -w 1
```

### Running (vagrant+docker)

Edit 'host/Vagrantfile', to point to the local path of this project on your disk. Then, inside vagrant environment, you can acces to this project resources in /src.

```
...
config.vm.synced_folder "c:/src/flexlm-license-elk", "/src"
...
```

As vagrant/docker environment is configured, just run: 

```
vagrant up
```

This will launch a Logstash instance (docker inside vagrant image), that process al *.log files on the /data directory.

As a result, in the same directory, a 'processed' directory will be created with one file per day with information of all the 'check in' and 'check out' licenses detected in the original log file:

```
/data/processed/>
flexlm_2016-03-30.txt
flexlm_2016-03-31.txt
flexlm_2016-04-01.txt
flexlm_2016-04-02.txt
...
```

With this content per line: [DATE] [TIME] [TIME_ZONE] [VENDOR] [IN or OUT] [FEATURE] [USER] [MACHINE]
```
2016-03-31 06:15:20 +0000 adskflex OUT 64300ACD_F USER14 COMPUTER13
2016-03-31 06:15:20 +0000 adskflex OUT 85730ACD_2012_0F USER14 COMPUTER13
2016-03-31 06:15:20 +0000 adskflex OUT 64300ACD_F USER14 COMPUTER13
2016-03-31 06:15:20 +0000 adskflex OUT 85730ACD_2012_0F USER14 COMPUTER13
2016-03-31 06:16:04 +0000 adskflex OUT 64300ACD_F USER23 COMPUTER19
2016-03-31 06:16:04 +0000 adskflex OUT 85730ACD_2012_0F USER23 COMPUTER19
...
```

## Contributing

Please, feel free to open issues and give feedback, pull requests...

## License

This project is licensed under the Apache License 2.0 - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

* [alcanzar](https://github.com/alcanzar) by his [memorize plugin](https://github.com/alcanzar/logstash-filter-memorize)

