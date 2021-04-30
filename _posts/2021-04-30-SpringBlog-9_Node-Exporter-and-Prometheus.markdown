Prometheus is an open-source, real-time monitoring tool that can be configured to handle specific queries. It can be used in conjunction with many other tools, in this case Node Exporter. Node exporter is used to scrape OS-level metrics from the host machine, and forward the results to Prometheus. This will be a quick rundown on how to easily set up and put these tools together on a machine using docker.

First, let's spin up a Node Exporter docker container. Note that Node Exporter runs on port 9100 by default:

	docker run -d --net="host" --pid="host" -v "/:/host:ro,rslave" quay.io/prometheus/node-exporter:latest --path.rootfs=/host
	
Essentially we're running a detached container, setting our network as the "host" network (as in the host machine), same with the process ID, and at the end we'll specify the /host directory on our local machine as the root filesystem for node exporter.

We'll have to make a yml file to install and configure prometheus properly. I was able to find an example online, and I made just a minor change to it (changing the IP addresses to 'localhost', and keeping the ports the same). Save this as "prometheus.yml":

	global:
	  scrape_interval: 5s
	  external_labels:
	    monitor: 'node'
	scrape_configs:
	  - job_name: 'prometheus' 
	    static_configs: 
	      - targets: ['localhost:9090']
	  - job_name: 'node-exporter' 
	    static_configs: 
	      - targets: ['localhost:9100']

Prometheus will be scraping at 5 second intervals, and will be running at port 9090, so we created a job for that. We've also done the same for port 9100, which will serve Node Exporter. Save the file. Now let's start up the instance with this command from the prometheus documentation:

	docker run \
    -p 9090:9090 \
    -v /path/to/prometheus.yml:/etc/prometheus/prometheus.yml \
    prom/prometheus
    
Give it a few seconds. After it's launched, check your browser by navigating to your local ip at port 9090. You'll see that both Node Exporter and Prometheus are up. Prometheus can be a bit difficult to use, but for the next blog I'll be talking about how to set up a GUI Grafana dashboard for host OS metric monitoring.
