# Advanced ETL with Apache NiFi and Couchbase
This repository is companion code for a blog post on our site: ADD LINK HERE.

This project is an all in one environment that sets up Vagrant machines with Couchbase and Apache NiFi installed. It has a NiFi data flow template that will retrieve GHCN weather data from NOAA and process it into Json documents for Couchbase.

Prerequisites
-------------
1. Install Virtualbox: https://www.virtualbox.org/wiki/Downloads

2. Install Vagrant: http://www.vagrantup.com/downloads.html

3. Install necessary Vagrant plugins:

```sh
vagrant plugin install vagrant-hostmanager
vagrant plugin install vagrant-cachier
```

4. Install Ansible

```sh
brew install ansible
```

Getting Started
---------------
1. Start by bringing up the Vagrant machines, it is configured to install everything you need to run the analysis, this may take a few minutes the first time.

    ```sh
    vagrant up
    ```

2. Go to the NiFi UI at http://nifi.vagrant:8080/nifi. Import the template by clicking on the Templates icon in the top right. In the Templates menu, click Browse then select the NOAA_to_Couchbase.xml file from this project. Finally, click Import.

3. Drag a Template from the toolbar on the top left onto the canvas. Select the template you just imported. A whole template should be added to the canvas.

4. Click the Controller Settings icon in the top right, go to the Controller Services tab, then click the lightning bolt next to the CouchbaseClusterService. When prompted click Enable.

5. Finally, click the Start button at the top of the screen to start the dataflow.

6. At this point you should start to see data flowing through the system. When you see documents of the In line in the PutCouchbaseKey processor you can check Couchbase to see documents in the weather bucket.


You can access the Couchbase UI at http://couchbase.vagrant:8091 with credentials: couchbase//couchbase and the NiFi UI at http://nifi.vagrant:8080/nifi.