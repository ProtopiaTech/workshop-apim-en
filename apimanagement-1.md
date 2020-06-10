# API Management - Hands-on Lab Script - part 1

Mark Harrison : checked & updated 12 March 2020 - original 1 Nov 2017

![](Images/APIM.png)

- [Part 1 - Create an API Management instance](apimanagement-1.md) ... this document
- [Part 2 - Developer Portal](apimanagement-2.md)
- [Part 3 - Administration](apimanagement-3.md)
- [Part 4 - Policy Expressions](apimanagement-4.md)
- [Part 5 - API Proxy to other Azure services](apimanagement-5.md)

## Create an API Management instance

An instance can take sometime to provision - so have one created in advance of any demo.

[![Deploy to Azure](https://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.ApiManagement)

![](Images/APIMDeployBlade.png)

Use appropriate values and hit [Create] to provision the service.

- Service name must be unique.
- For demo purposes, use the Developer tier.

![API Management](Images/APIManagement.png)

Once the service has been provisioned, there will be:

- Publisher Administration - this is now located in the Azure Management Portal
  - ( the older Publisher portal has now been deprecated )
- Developer portal
- Gateway

The link to the developer portal is at the top of the Overview blade.

![](Images/APIMOverviewBlade.png)

---
[Home](README.md) | [Next](apimanagement-2.md)
