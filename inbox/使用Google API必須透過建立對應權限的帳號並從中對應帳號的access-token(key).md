使用Google API必須透過建立對應權限的帳號並從中對應帳號的access-token(key)



Create a service account:

1.  In the Cloud console, go to the **Create service account** page.
    
    [Go to Create service account](https://console.cloud.google.com/projectselector/iam-admin/serviceaccounts/create?supportedpurview=project&_ga=2.195391724.1532012106.1653075287-1061095323.1651492866&_gac=1.250609140.1653101683.Cj0KCQjw-JyUBhCuARIsANUqQ_KGPwgT76S49-UR_g1OggGZhVMqQ3ZB3UIpkbue7nYf0-24rNhzrxAaAjIhEALw_wcB)
2.  Select your project.
3.  In the **Service account name** field, enter a name. The Cloud console fills in the **Service account ID** field based on this name.
    
    In the **Service account description** field, enter a description. For example, `Service account for quickstart`.
    
4.  Click **Create and continue**.
5.  To provide access to your project, grant the following role(s) to your service account: **Project > Owner**.
    
    In the **Select a role** list, select a role.
    
    For additional roles, click add **Add another role** and add each additional role.
    
    **Note**: The **Role** field affects which resources your service account can access in your project. You can revoke these roles or grant additional roles later. In production environments, do not grant the Owner, Editor, or Viewer roles. Instead, grant a [predefined role](https://cloud.google.com/iam/docs/understanding-roles#predefined_roles) or [custom role](https://cloud.google.com/iam/docs/understanding-custom-roles) that meets your needs.
    
6.  Click **Continue**.
7.  Click **Done** to finish creating the service account.
    
    Do not close your browser window. You will use it in the next step.
    

Create a service account key:

1.  In the Cloud console, click the email address for the service account that you created.
2.  Click **Keys**.
3.  Click **Add key**, and then click **Create new key**.
4.  Click **Create**. A JSON key file is downloaded to your computer.
5.  Click **Close**.