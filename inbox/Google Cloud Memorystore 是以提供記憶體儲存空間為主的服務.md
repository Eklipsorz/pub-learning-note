
Google Cloud Memorystore 是以提供記憶體儲存空間為主的服務
其中有分redis和memcached
- Google Cloud Memorystore for Redis API
- Google Cloud Memorystore for Memcached API


https://github.com/googleapis/nodejs-redis/issues/386


# Serverless VPC Access API
To access the Redis instance, the App Engine app must be configured to use your Serverless VPC Access connector, and you must provide your Redis instance's connection details.

1.  If you don't already have one, create an [App Engine application](https://console.cloud.google.com/projectselector/appengine/create).
    
2.  Update the app's configuration to specify your Serverless VPC Access connector and the IP address and port of your Redis instance:
## Create a Serverless VPC Access connector

To send requests to your VPC network and receive the corresponding responses without using the public internet, you must use a Serverless VPC Access connector.

You can create a connector by using the Google Cloud console, Google Cloud CLI, or Terraform: