Vagrant.configure(2) do |config|
  
	# Disable synced folders (prevents an NFS error on "vagrant up")
	config.vm.synced_folder ".", "/vagrant", disabled: true

	# Configure the Docker provider for Vagrant
	config.vm.provider "docker" do |docker|
		docker.vagrant_machine = "dockerhost"
		docker.vagrant_vagrantfile = "host/Vagrantfile"
	end
  
	## ElasticSearch Container
	#config.vm.define "elastic-container" do |container|
	#	# Configure the Docker provider for Vagrant
	#	container.vm.provider "docker" do |docker|
	#		#docker.image = "elasticsearch:2.1"
	#		docker.build_dir = "./elastic"
	#		docker.ports = ['9200:9200','9300:9300']
	#		docker.name = 'elastic-container'
#
	#		docker.create_args = ["-v", "/src/elastic/data:/usr/share/elasticsearch/data"]
    #    end
	#end
	#
	## Kibana Container
	#config.vm.define "kibana-container" do |container|
	#	# Configure the Docker provider for Vagrant
	#	container.vm.provider "docker" do |docker|
	#		#docker.image = "elasticsearch:2.1"
	#		docker.build_dir = "./kibana"
	#		docker.ports = ['5601:5601']
	#		docker.name = 'kibana-container'
	#		docker.link("elastic-container:elastic-container")
    #    end
	#end
	
	# Logstash Container
	config.vm.define "logstash-container" do |container|
		# Configure the Docker provider for Vagrant
		container.vm.provider "docker" do |docker|
			#docker.image = "logstash:2.1"
			docker.build_dir = "./logstash"
			#docker.ports = ['5601:5601']
			docker.name = 'logstash-container'
			#docker.link("elastic-container:elastic-container")

			docker.create_args = ["-v", "/src/logstash:/var/local/logstash"]
        end
	end
  
end
