# SiteWhere Platform

This project provides docker compose scripts which enable starting up [SiteWhere]() cluster on the fly. Also It is useful for testing and automatic deployment for SiteWhere components (SiteWhere, MongoDB, and MQTT (mosquito)).

Currently we support SiteWhere 1.9.0

If you are not familiar with Docker, please find the below link

* [Play with Docker](http://training.play-with-docker.com/)
* [Docker Orchestration](http://jpetazzo.github.io/orchestration-workshop/#1)

## Table of Contents

* [Start SiteWhere Cluster](#Start_SiteWhere_Cluster)
* [SiteWhere REST APIs](#SiteWhere_APIs)
  * [Create Site](#Create_Site)

## Start SiteWhere Cluster
<a name="Start_SiteWhere_Cluster"/>

```
        # pull modified sitewhere docker images
	$ sudo docker pull aabdulwahed/sitechain:sitewhere-core && \
	  sudo docker pull aabdulwahed/sitechain:mongo && \
	  sudo docker pull aabdulwahed/sitechain:eclipse-mosquitto \
	  sudo docker pull appropriate/curl

	# run docker compose file
	$ sudo docker-compose -f sitewhere.yml up
``` 

Finally, check out [http://localhost:5000/sitewhere/admin](http://localhost:5000).

## SiteWhere REST APIs
<a name="SiteWhere_APIs"/>
to access the sitWhere server through REST interface, use the following curl commands.

**Create new site**
<a name="Create_Site"/>
*Sample curl request* 
```
	$ docker run --rm appropriate/curl \
	–H  'Content-Type: application/json' \
	–H 'Authorization: Basic YWRtaW46cGFzc3dvcmQ=' \
	–H 'X-SiteWhere-Tenant: sitewhere1234567890' \
	-X POST \
	–d '{
		"name":"Network1",
		"description":"smart village wifi routers ",
		"imageUrl":"http://www.smart-villages.com/cmsadmin/gallery-photogallery_pics-pic_154.jpg",
		"metadata":{},
		"map":{
			"type":"mapquest",
			"metadata":{
				"centerLatitude":"",
				"centerLongitude":"",
				"zoomLevel":""
			}
		}
		}' \
	 http://192.168.99.100:5000/sitewhere/api/sites 
```
