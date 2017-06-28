# SiteWhere Platform

This project provides docker compose scripts which enable starting up [SiteWhere]() cluster on the fly. Also It is useful for testing and automatic deployment for SiteWhere components (SiteWhere, MongoDB, and MQTT (mosquito)).

Currently we support SiteWhere 1.9.0

If you are not familiar with Docker, please find the below link

* [Play with Docker](http://training.play-with-docker.com/)
* [Docker Orchestration](http://jpetazzo.github.io/orchestration-workshop/#1)


# Start SiteWhere Cluster

```
        # pull modified sitewhere docker images
	$ sudo docker pull aabdulwahed/sitechain:sitewhere-core && \
	  sudo docker pull aabdulwahed/sitechain:mongo && \
	  sudo docker pull aabdulwahed/sitechain:eclipse-mosquitto

	# run docker compose file
	$ sudo docker-compose -f sitewhere.yml up
``` 

Finally, check out [http://localhost:5000](http://localhost:5000).
