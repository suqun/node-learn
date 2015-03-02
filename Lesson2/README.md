# Ubuntu中安装mongodb

------
##Control Scripts
The package configures MongoDB using the `/etc/mongod.conf` file in conjunction with the control scripts.
##Install MongoDB
1. Import the public key used by the package management system.
  >**sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10 **
2. Create a list file for MongoDB.
  >**echo 'deb http://downloads-distro.mongodb.org/repo/ubuntu-upstart dist 10gen' | sudo tee /etc/apt/sources.list.d/mongodb.list**
 3. Reload local package database.
 >**sudo apt-get update**
 4. Install the MongoDB packages.
     * Install the latest stable version of MongoDB.
     >**sudo apt-get install -y mongodb-org**
     * install a specific release of MongoDB
     >**sudo apt-get install -y mongodb-org=2.6.1 mongodb-org-server=2.6.1 mongodb-org-shell=2.6.1 mongodb-org-mongos=2.6.1 mongodb-org-tools=2.6.1
**
##Run MongoDB
The MongoDB instance stores its data files in `/var/lib/mongodb` and its log files in `/var/log/mongodb` by default, and runs using the mongodb user account. You can specify alternate log and data file directories in `/etc/mongod.conf`.

1. Start MongoDB.
>**sudo service mongod start**
2. Verify that MongoDB has started successfully

     Verify that the mongod process has started successfully by checking the contents of the log file at `/var/log/mongodb/mongod.log` for a line reading

     >**[initandlisten] waiting for connections on port <port>**

     where <port> is the port configured `/etc/mongod.conf`,`27017` by default.

3. Stop MongoDB.

    As needed,you can stop the `mongod` process by issuing the following command:
    >**sudo service mongod stop**
    
4. Restart MongoDB.
    
    Issue the following command to restart`mongod`:
    >**sudo service mongod restart**

 
 

[参考docs.mongodb.org](http://docs.mongodb.org/manual/tutorial/install-mongodb-on-ubuntu/)
