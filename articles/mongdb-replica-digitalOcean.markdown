Title: MongoDB on Digital Ocean, installation and replica
Author: Matthieu Croquelois
Date: 10/28/2013 20:37
Categories: mongodb,replica,digitalOcean

## Choose the droplet

First step create a droplet, choose a **64bit** version of ubuntu, and a decent amount of memory.

## Prepare the droplet

- apt-get update
- apt-get upgrade

To have the last version of mongodb, you need to get it from 10gen directly.

10gen was the company which is behind MongoDB, they have now rename the company just MongoDB but I suppose the repository will stay 10gen for sometime.

- apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10
- echo 'deb http://downloads-distro.mongodb.org/repo/ubuntu-upstart dist 10gen' | tee /etc/apt/sources.list.d/mongodb.list
- apt-get update

Clean previous mess

- apt-get remove mongodb
- apt-get remove mongodb-clients
- apt-get remove mongodb-server
- apt-get remove mongodb-dev

## FTP

To ease the deployement, a ftp can be useful, so let's add a new user and install ftpd:

- useradd -m ftpUser
- passwd ftpUser 
- apt-get install ftpd

## Mongodb installation

- apt-get install mongodb-10gen

Then launch mongo

- start mongodb
- mongo

Add an admin: 

- db = db.getSiblingDB('admin')
- db.addUser( { user: "dbAdmin",  pwd: "yourPassword", roles:[ "userAdminAnyDatabase","clusterAdmin",""readAnyDatabase"","dbAdminAnyDatabase"  ] } )

And some users:

- db = db.getSiblingDB('mydb')
- db.addUser( { user: "vinck",  pwd: "passOfVinck", roles: [ "readWrite", "dbAdmin" ] } )
- db.addUser( { user: "croq",  pwd: "passOfCroq", roles: [ "readWrite", "dbAdmin" ] } )

In the mongodb.cfg file in your /etc directory, put 'auth' to true 

## MMS

### Prepare Python environment

install python 2.7 and gcc

- apt-get install gcc
- apt-get install python
- apt-get install python-dev

install easy_install and pip

- wget https://bitbucket.org/pypa/setuptools/raw/bootstrap/ez_setup.py -O - | python
- easy_install pip

uninstall & install driver

- pip uninstall pymongo
- pip install pymongo

### Create an account on MMS

- go to [mms.mongodb.com](http://mms.mongodb.com "mms.mongodb.com")
- create your account
- download the agent
- transfer it to your server (it's where ftp can be useful)

### Launch the agent

- change settings.py to add you admin login and password
- nohup python agent.py >> /home/croq/agent.log 2>&1 &

## Create replica

### Create a keyFile

Your different replica will have to communicate securely.

So you need to give them a unique random key to share information.

- openssl rand -base64 741 > /etc/mongo.keyfile
- chown mongodb:mongodb /etc/mongo.keyfile
- chmod 0600 /etc/mongo.keyfile

in mongodb.cfg put 'keyFile' to '/etc/mongo.keyfile'
 
- copy this key to the replica (once again the ftp can be useful)
- redo chown & chmod and the modification in mongodb.cfg

### DNS setup

You will have to make sure your database can communicate between them, so either you have a properly configured dns server. 

Or you add your replica ip and host name in /etc/hosts on all machine.

### Setup each replica

On each server:

- stop mongodb
- in mongodb.cfg put 'replSet' to 'RS0'
- start mongodb

### Connect replica together

Go to the primary server (or a random one if all database are empty)

Add each replica by doing: rs.add("host:port") for each secondary server

## Enjoy

you can now connect to your database with [http://www.mongovue.com/](http://www.mongovue.com/ "mongoVue") to check if everything is ok

you can also check on MMS if everything work fine
