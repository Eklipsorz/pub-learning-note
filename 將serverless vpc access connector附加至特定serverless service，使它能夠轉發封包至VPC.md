1.  Add the Serverless VPC Access field to your `app.yaml` file:
    
    vpc_access_connector:
     name: projects/PROJECT_ID/locations/REGION/connectors/CONNECTOR_NAME
    
    Replace the following:
    
    -   `PROJECT_ID` with your Cloud project ID. If your connector is in the host project of a Shared VPC, this must be the ID of the host project.
    -   `REGION` with the region that your connector is in.
    -   `CONNECTOR_NAME` with the name of your connector.



記得賦予cloud build 一個能夠存取serverless vpc 的權限
Serverless VPC Access Admin