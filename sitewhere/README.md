# SiteWhere Platform

This project provides docker compose scripts which enable starting up [SiteWhere]() cluster on the fly. Also It is useful for testing and automatic deployment for SiteWhere components (SiteWhere, MongoDB, and MQTT (mosquito)).

Currently we support SiteWhere 1.9.0

If you are not familiar with Docker, please find the below link

* [Play with Docker](http://training.play-with-docker.com/)
* [Docker Orchestration](http://jpetazzo.github.io/orchestration-workshop/#1)

## Table of Contents

* [Start SiteWhere Cluster](#Start_SiteWhere_Cluster)
* [SiteWhere REST APIs](#SiteWhere_APIs)
  * [Create devices specifications](#Create_devices_specifications)
  * [Create site](#Create_site)
  * [Create device](#Create_device)
  * [Create assignment for devices](#Create_assignment_for_devices)
  * [Get sites](#Get_site)
  * [List device assignments for site](#List_device_assignments_for_site)
  * [Get device by hardware id](#Get_device_by_hardware_id)
  * [Get commands of device specification](#Get_commands_of_device_specification)
  * [Send command to a device assignment](#Send_command_to_a_device_assignment)
* [SiteWhere Common Scenarios](#SiteWhere_Common_Scenarios)
  * [Create the devices network](#create_the_devices_network)
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

**Create devices specifications**
<a name="Create_devices_specifications"

*Sample curl request* 
```
	docker run --rm appropriate/curl \
	–H  'Content-Type: application/json' \
	–H 'Authorization: Basic YWRtaW46cGFzc3dvcmQ=' \
	–H 'X-SiteWhere-Tenant: sitewhere1234567890' \
	-X POST \
	–d '{
		"name":"WiFi-Node",
		"containerPolicy":"Standalone",
		"assetModuleId":"fs-devices",
		"assetId":"174",
		"metadata":{
		"Cotract":"sample"}}' \
	http://192.168.99.100:5000/sitewhere/api/specifications
```
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
**Create device**
<a name="Create_device"/>

*Sample curl request* 
```
	docker run --rm appropriate/curl \
	–H  'Content-Type: application/json' \
	–H 'Authorization: Basic YWRtaW46cGFzc3dvcmQ=' \
	–H 'X-SiteWhere-Tenant: sitewhere1234567890' \
	-X POST \
	–d '{
		"hardwareId":"WiFi-Node 2",
		"siteToken":"bfd6c191-194e-401f-be93-6fa4db920968",
		"comments":"wifi node at smart village ",
		"specificationToken":"311cdf0d-0dec-4db5-8163-3b93ad4b2c2b",
		"metadata":{}}' \
	http://192.168.99.100:5000/sitewhere/api/devices
```
**Create assignment for devices**
<a name="Create_assignment_for_devices"/>

*Sample curl request* 
```
	docker run --rm appropriate/curl \
	–H  'Content-Type: application/json' \
	–H 'Authorization: Basic YWRtaW46cGFzc3dvcmQ=' \
	–H 'X-SiteWhere-Tenant: sitewhere1234567890' \
	-X POST \
	–d ' {
		"deviceHardwareId":"WiFi-Node 2",
		"metadata":{},
		"assignmentType":"Associated",
		"assetModuleId":"fs-devices",
		"assetId":"174"}' \
	http://192.168.99.100:5000/sitewhere/api/assignments
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

**Get device by hardware id**
<a name="Get_device_by_hardware_id"/>

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
	http://192.168.99.100:5000/sitewhere/api/devices/2fa14cfd-525f-4beb-bedd-dc296ff7ace7?tenantAuthToken=sitewhere1234567890
```

**Get commands of device specification**
<a name="Get_commands_of_device_specification"/>

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
	http://192.168.99.100:5000/sitewhere/api/specifications/82043707-9e3d-441f-bdcc-33cf0f4f7260/commands?tenantAuthToken=sitewhere1234567890
```
**Send command to a device assignment**
<a name="Send_command_to_a_device_assignment"/>

*Sample curl request* 
```
	docker run --rm appropriate/curl \
	–H  'Content-Type: application/json' \
	–H 'Authorization: Basic YWRtaW46cGFzc3dvcmQ=' \
	–H 'X-SiteWhere-Tenant: sitewhere1234567890' \
	-X POST \
	–d '{"initiator":"REST",
	"initiatorId":"admin",
	"target":"Assignment",
	"commandToken":"b5268517-4f31-48f3-a5bf-bbb1c99f8467",
	"status":"Pending",
	"metadata":{},
	"parameterValues":{"message":"$$testing command$$"}}' \
	http://192.168.99.100:5000/sitewhere/api/assignments/09ff7368-3ce0-4d26-bc40-d7c775c1b305/invocations?tenantAuthToken=sitewhere1234567890
```


## SiteWhere Common Scenarios
<a name="SiteWhere_Common_Scenarios"/>

**Create the devices network**
<a name="create_the_devices_network"/>

1.Create Devices Specifications for each device category to hold the characteristics of a given hardware configuration

2.Create site to hold a related devices 

3.Create devices that represent a connected physical hardware, which must be configured with certain device specification and site

4.Create new assignment for devices

**Send command to a device assignment**
<a name="Send_command_to_a_device_assignment"/>

1- get the assignments in the site

2- parse the return json using the "assetName" to get the "deviceHardwareId"

3- get the device details to get the specification token

4- parse the return json using "specification" to get the "token"

5- get the commands using the specification token

6- parse the return json using "name" to get the "token"

7- send the command using assignment token id and commandToken

