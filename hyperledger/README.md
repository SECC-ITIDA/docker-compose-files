# HyperLedger

HyperLedger project provides a blockchain technologies for open source community. In this file we are going to introduce two main HyperLedger components (Fabric and Composer) in order to orchestrate business network services on top of blockchain networks.

# HyperLedger Fabric

* Download the following images
```
	$ sudo docker pull hyperledger/fabric-couchdb:x86_64-1.0.0-beta
	$ sudo docker pull hyperledger/fabric-orderer:x86_64-1.0.0-beta
	$ sudo docker pull hyperledger/fabric-peer:x86_64-1.0.0-beta
	$ sudo docker pull hyperledger/fabric-ccenv:x86_64-1.0.0-beta
	$ sudo docker pull hyperledger/fabric-ca:x86_64-1.0.0-beta
```

* Install Nodejs and nvm 

```
  	$ sudo apt-get install nodejs
	$ sudo apt-get install npm
	$ sudo apt-get update
	$ sudo apt-get install build-essential libssl-dev
	$ curl https://raw.githubusercontent.com/creationix/nvm/v0.16.1/install.sh | sh
	$ source ~/.profile
	$ nvm install v6.9.0
	$ nvm use v6.9.0
```

*  Download composer example

```
	$  npm install -g digitalproperty-network
```


# HyperLedger Composer

* Install composer tools

```
	$ npm install -g composer-cli
	$ npm install -g composer-rest-server
	$ npm install -g yo
```
