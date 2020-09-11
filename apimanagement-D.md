# API Management - Hands-on Lab Script

[Home](README.md)

## Additional Topics - Azure Active Directory Integration

## AAD Create a new tenant

1. Sign in to your organization's [Azure portal](https://portal.azure.com/).

1. From the Azure portal menu, select **Create a resource**.  

    ![Azure Active Directory Create resoure page](Images/azure-ad-portal.png)

1. Select **Identity**, and then select **Azure Active Directory**.

    The **Create directory** page appears.

    ![Azure Active Directory Create page](Images/azure-ad-create-new-tenant.png)

1.  On the **Create directory** page, enter the following information:
    
    - Type _Contoso_ into the **Organization name** box.

    - Type _Contoso_ into the **Initial domain name** box.

    - Leave the _United States_ option in the **Country or region** box.

1. Select **Create**.

Your new tenant is created with the domain labapimtenant.onmicrosoft.com.



## AAD Create a new user, group - 
    Create user1, user2, user3
    Group blue
        Add user1
    Group green
        Add user1
        Add user2
        Add user3
    Group red
        Add user3
        

## AAD Register apps 
    Register Frontend - msal authenticate the user , obtain user group claim 
    Register api management , validate jwt 
    Register el backend legacy SOAP - certificate auth, networking firewall ///

## Modify Frontend with AAD login 
    Add a view to asp.net core frontend with msal authentication

## APIM configure OAUTH2 server
    Add oauth2 server
    Add oauth2 server to webservice
    Add jwt-validate policy 
    Transform, get user group claim and pass to legacy backend

## Legacy Backend,
    Secure using networking 

## Add legacy backend to apim

## Cofigure legacy webservice to apim





---
[Home](README.md)  
