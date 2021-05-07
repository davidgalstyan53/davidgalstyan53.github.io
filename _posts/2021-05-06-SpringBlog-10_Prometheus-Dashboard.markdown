Picking up from where we left off last time, we can see that we are able to visit both the Node Exporter and Prometheus landing pages on ports 9100 and 9090, respectfully.

If we look up port 9100, the Node Exporter landing page, we'll see that there is a "Metrics" section. If we open that, we'll find a massive wall of text. While the text is human readable, it's not ideal to look at, especially if we're trying to monitor system metrics, like Node Exporter is doing. Prometheus, meanwhile, is scraping these metrics off of Node Exporter, and for that, we can go to port 9090.

If we go to "Status" and then "Targets", we will see that Prometheus is targeting itself, and Node Exporter. There are a couple of routes we can take from here:
- We can try to use Prometheus queries
- Or we can try to implement a GUI dashboard that we can visit in the browser

Grafana is a tool that allows us to use GUI dashboards in order to visualize our Prometheus metrics. Installing Grafana with docker is extremely simple (be sure that port 3000 is open). The following command will pull and run the latest version of Grafana:

	sudo docker run -d -p 3000:3000 grafana/grafana
	
We can then navigate to port 3000 in the web browser, and we'll be greeted with the Grafana landing page. Default uname and passwd are "admin", so after logging in you'll be able to get started.

We now want to have Grafana listen in on port 9090 and take the metrics from Prometheus. For that, we will have to "Add our first Data Source" by navigating to it on Grafana, pick "Prometheus" as our source, and use the full URL of the location where prometheus is hosted (EXAMPLE: http://192.168.1.147:9090). Once the data source is tested and running, we are good to go in regards to connecting Grafana to Prometheus. But we still need a dashboard.

You can either create a dashboard, or you can use a template that somebody else has created. For this, you can simply look up "Prometheus Grafana dashboard templates". In this case, you will want a Node Exporter one because this is supposed to be for monitoring system metrics. There is a short numerical code that comes with each template, and you can simply copy paste the code into the section that asks you to import a dashboard. Once that is imported and you save the changes, you'll be met with a super cool OS system metrics monitoring dashboard. 
