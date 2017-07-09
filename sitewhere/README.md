# SiteWhere Platform

This project provides docker compose scripts which enable starting up [SiteWhere]() cluster on the fly. Also It is useful for testing and automatic deployment for SiteWhere components (SiteWhere, MongoDB, and MQTT (mosquito)).

Currently we support SiteWhere 1.9.0

If you are not familiar with Docker, please find the below link

* [Play with Docker](http://training.play-with-docker.com/)
* [Docker Orchestration](http://jpetazzo.github.io/orchestration-workshop/#1)

## Table of Contents

* [Start SiteWhere Cluster](#Start_SiteWhere_Cluster)
* [SiteWhere REST APIs](#SiteWhere_APIs)
  * [Create site](#Create_site)
  * [Get sites](#Get_site)
  * [List device assignments for site](#List_device_assignments_for_site)
  * [Get device by hardware id](#Get_device_by_hardware_id)
  * [Get commands of device specification](#Get_commands_of_device_specification)
  * [Send command to a device assignment](#Send_command_to_a_device_assignment)

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
json to access the sitWhere server through REST interface, use the following curl commands.and use http://jsonviewer.stack.hu/ to format the response.

**Create site**
<a name="Create_site"/>

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

**Get sites**
<a name="Get_site"/>


*Sample curl request* 
```
	$ docker run --rm appropriate/curl \
	–H  'Accept: application/json, text/javascript, */*; q=0.01' \
	-H 'Accept-Language: en-US,en;q=0.8' \
	-H 'X-Requested-With: XMLHttpRequest' \
	–H 'Authorization: Basic YWRtaW46cGFzc3dvcmQ=' \
	-H 'Referer: http://192.168.99.100:5000/sitewhere/admin/sites/list.html' \
	-H 'Accept-Encoding: gzip, deflate, br' \
	-X GET \
	http://192.168.99.100:5000/sitewhere/api/sites?tenantAuthToken=sitewhere1234567890&take=10&skip=0&page=1&pageSize=10
```
**List device assignments for site**
<a name="List_device_assignments_for_site"/>


*Sample curl request* 
```
	docker run --rm appropriate/curl \
	–H  'Accept: application/json, text/javascript, */*; q=0.01' \
	-H 'Accept-Language: en-US,en;q=0.8' \
	-H 'X-Requested-With: XMLHttpRequest' \
	–H 'Authorization: Basic YWRtaW46cGFzc3dvcmQ=' \
	-H 'Referer: http://192.168.99.100:5000/sitewhere/admin/sites/list.html' \
	-H 'Accept-Encoding: gzip, deflate, br' \
	-X GET \
	http://192.168.99.100:5000/sitewhere/api/sites/bb105f8d-3150-41f5-b9d1-db04965668d3/assignments?tenantAuthToken=sitewhere1234567890
```

** [Get device by hardware id](#Get_device_by_hardware_id)
**Get commands of device specification**
<a name="Get_commands_of_device_specification"/>


*Sample curl request* 
```
```
**Send command to a device assignment**
<a name="Send_command_to_a_device_assignment"/>

*Sample curl request* 
```
```


