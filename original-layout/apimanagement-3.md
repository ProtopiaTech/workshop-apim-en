# API Management - Hands-on Lab Script - part 3

Mark Harrison : checked & updated 12 March 2020 - original 1 Nov 2017

![](../Images/APIM.png)

- [Part 1 - Create an API Management instance](apimanagement-1.md)
- [Part 2 - Developer Portal](apimanagement-2.md)
- [Part 3 - Administration](apimanagement-3.md)  ... this document
- [Part 4 - Policy Expressions](apimanagement-4.md)
- [Part 5 - API Proxy to other Azure services](apimanagement-5.md)

## Administration

API Management administration is done using the Azure management portal.

### Identity

#### Users / Groups

- Look at users and groups

![](../Images/APIMGroupsBlade.png)

![](../Images/APIMUsersBlade.png)

- Approve the developers request (from earlier) for a "Unlimited" subscription

![](../Images/APIMUserActivateSub.png)

![](../Images/APIMUserActivateSub2.png)

#### Federation

User identity can federate with Azure AD and social identity providers.

![](../Images/APIMIdentitiesBlade.png)

Set up federation - optional (needs access to an identity provider / approprate permissions).

Example, for Azure AD

![](../Images/APIMFederationAzureAD.png)

- Config API Management to federate with Azure AD
Redirect  
  - Make note of the Redirect URL

- Switch to the Azure AD blade to config an app
  - Create a new registration
  - Configure the App - specify the Redirect URL ... and Register

![](../Images/APIMFederationCreateApp.png)

![](../Images/APIMFederationCreateApp2.png)

- Get App registration information
  - Make note of Application Id
  - Create a Key - make a note of it

![](../Images/APIMFederatationGetAppID.png)

![](../Images/APIMFederationCreateKey.png)

![](../Images/APIMFederationCreateKey2.png)

- Select Authentication and then select [ID tokens] under Implicit Grant ... Save

![](../Images/APIMFederationAuthentication.png)

- Return to the APIM Configuration | Add Identity Provider blade
  - Enter the Application Id and Key
  - Enter the AD tenants that you want to federate with

![](../Images/APIMFederationAzureAD2.png)

![](../Images/APIMFederationAzureAD3.png)

- As administrator return to Developer portal and republish the portal website

- As an unauthenticated user - return to the Developer portal | Sign In Page - and notice the Azure AD federation option now appears at the bottom
  - Create an account with a user from Azure AD
  - Sign in with an Azure AD account

![](../Images/APIMFederationSignup.png)

![](../Images/APIMFederationSignup2.png)

![](../Images/APIMFederationSignup3.png)

![](../Images/APIMFederationSignup4.png)

#### API authentication

Developers need a key to successfully invoke the API

- The keys for the subscribed products can be seen in the Profile screen
- The Unlimited subscription is now active (we approved the request)

![](../Images/APIMDevKeys2.png)

There is also support for OAuth2 & OpenId Connect to enable user authentication.

![](../Images/APIMOAuthBlade.png)

Support for JSON Web Token (JWT) and to ensure it is valid and to make decisions based on the claims in the token ... this is addressed later

Client certificates can be uploaded, and used to authenticate API Management with the backend API infrastructure

![](../Images/APIMCertBlade.png)

### Service Management

Each API Management service instance maintains a configuration database that contains information about the configuration and metadata for the service instance.

#### Scripting

Changes can be made to the service instance by changing a setting in the publisher portal, using a PowerShell cmdlet, or making a REST API call.

- Look at the management REST API.  This is off by default and needs to be enabled, if required.

![](../Images/APIMManagementAPIBlade.png)

#### Global deployment

Premium tier supports multi-region deployment which enables API publishers to distribute a single API Management service across any number of desired Azure regions.

Uses Traffic Manager 'performance routing' methods.

- This is not available in the Developer tier.

<https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-deploy-multi-region>

#### Lifecycle

Changes can be made to the service instance by changing a setting in the publisher portal, using a PowerShell cmdlet, or making a REST API call.

Can also manage your service instance configuration using Git, enabling service management scenarios such as configuration versioning, bulk configuration changes and familiar Git toolchain and workflow.

- Look at Git configuration
  - Generate password
  - Save to Repository

![](../Images/APIMRepositoryPWBlade.png)

![](../Images/APIMRepositoryBlade.png)

- Pull to local machine ... will need to enter credentials

![](../Images/APIMGitClone.png)

![](../Images/APIMGitClone2.png)

![](../Images/APIMGitClone3.png)

- Make change to a Product description

![](../Images/APIMGitEditContent.png)

- Push back to the API Management repository

![](../Images/APIMGitPush.png)

- Select [Deploy to API Management] in the Repository blade - specify master branch

![](../Images/APIMGitDeploy.png)

- See update in Developer portal

![](../Images/APIMGitProductUpdates.png)

#### Networking

Azure API Management can be deployed inside the virtual network (VNET), so it can access backend services within the network. The developer portal and API gateway, can be configured to be accessible either from the Internet or only within the virtual network.

<https://docs.microsoft.com/en-us/azure/api-management/api-management-using-with-vnet>

VNET connectivity is available in the Premium and Developer tiers only.

![](../Images/APIMVNet.png)

#### Scale

Customers can scale an API Management instance by adding and removing units. A unit has a certain load-bearing capacity expressed as a number of API calls per month and volume of data transfer.  Capacity and price of each unit depends on a tier in which the unit exists. You can choose between three tiers: Developer, Standard, Premium.

The price of each unit, the ability to add/remove units, whether or not you have certain features (for example, multi-region deployment) depends on the tier that you chose for your API Management instance.  Standard and Premium are production tiers have SLA and can be scaled. The Standard tier can be scaled to up to four units. You can add any number of units to the Premium tier.

<https://azure.microsoft.com/en-gb/pricing/details/api-management/>

![](../Images/APIMScale.png)

### Product Management

A product contains one or more APIs as well as a usage quota and the terms of use. Once a product is published, developers can subscribe to the product and begin to use the product's APIs.

#### Product definition

- Look at existing products

![](../Images/APIMProducts.png)

- Add new product - for example a Gold tier
  - Assign APIs | set Visibility | Create

![](../Images/APIMAddProduct.png)

![](../Images/APIMAddProduct2.png)

- Set Access Controls to allow developer access

![](../Images/APIMAddProductsAccess.png)

- See the new Gold Tier product in the Developer portal

![](../Images/APIMAddProductsDevPortal.png)

#### Policies

- Look at policy for Starter product
- Notice the rate limits / quota constraints
- Policies can be at the Product level, API level or Operation Level
  - We will later drill deeper into API policy expressions

![](../Images/APIMProductStarter.png)

![](../Images/APIMProductStarterPolicy.png)

### API Management

An API represents a set of operations that can be invoked. New APIs are defined and then the desired operations are added. An API is added to a product and can be published; it may then be subscribed to and used by developers.

#### APIs

- Look at the API blade
  - List of APIs under management
  - Options for adding new APIs

![](../Images/APIMListAPIs.png)

![](../Images/APIMAddAPIs.png)

#### Add API from scratch

This will use the Start Wars API <https://swapi.dev>

- Select [Add Blank API]
  - Select the [Full] option at the top of the dialog
  - Enter Display name, name and description
  - Enter back end Web Service - this is <https://swapi.dev/api>
  - Set API URL suffice to sw
  - Assign Products - Starter and Unlimited
  - Create

![](../Images/APIMAddBlankAPI.png)

- Select [Start Wars API]

![](../Images/APIMAddStarWars.png)

- Add Operation
  - GET /people/  ... use lowercase
  - GET /people/{id}/  ... use lowercase

![](../Images/APIMAddSWGetPeople.png)

![](../Images/APIMAddSWGetPeopleById.png)

![](../Images/APIMAddSWOperations.png)

To get this to work from the Developer portal - we must overcome the CORS.  Cross-origin resource sharing (CORS) is a mechanism that allows restricted resources on a web page to be requested from another domain outside the domain from which the first resource was served.   This involves setting up a Policy - a topic that we explain in more depth in the next section.

- Select the Star Wars API | All Operations ... and in the Inbound processing select [Add policy]

![](../Images/APIMSWCORS1.png)

- Select [CORS]

![](../Images/APIMCORS2.png)

- Define the Policy as in the screenshot - this config is suitable for demo purposes only and ensures we are not hampered by CORS

![](../Images/APIMCORS3.png)

- Once the policy had been Saved, we can inspect it in [Code View]

![](../Images/APIMCORS4.png)

- Switch now to the Developer Portal
  - Signin as a developer with a subscription
  - Select [Start Wars API]

![](../Images/APIMSWTryIt1.png)

- Try the "GetPeople" operation
- Try the "GetPeopleById" operation ... with id = 2

![](../Images/APIMSWTryIt2.png)

- Examine Response and more detailed Trace information
  - Response 200 successful
  - Information about C-3PO in the Response body payload.

![](../Images/APIMSWTryIt3.png)

#### Import API using swagger

The OpenAPI specification (aka Swagger) is a definition format to describe RESTful APIs. The specification creates a RESTful interface for easily developing and consuming an API by effectively mapping all the resources and operations associated with it.

<https://www.openapis.org/>

<https://swagger.io>

As a demo we shall use an API that offers a simple calculator service

- Calc API
  - <http://calcapi.cloudapp.net/>

![](../Images/APIMCalcAPI.png)

- Goto API blade and select [Add OpenAPI Specification]
- Specify swagger URL <http://calcapi.cloudapp.net/calcapi.json>
  - Some of the fields will be populated from the swagger definition
  - Use "calc" in URL for API
  - Add products Starter and Unlimited

![](../Images/APIMAddCalcAPI1.png)

![](../Images/APIMAddCalcAPI2.png)

- As above set a CORS policy to allow access from the Developer portal

- Look at Calculator API in Developer portal
  - Try the Add Two Integers operation
- Look at Response / Trace

![](../Images/APIMCalcTryIt1.png)

![](../Images/APIMCalcTryIt2.png)

We can inspect / edit the Open API definition by selecting Edit icon from the Frontend block:

![](../Images/APIMCalcSwagger.png)

![](../Images/APIMCalcSwagger2.png)

Another example - the Colors API

- Colors API
  - <https://markcolorapi.azurewebsites.net/swagger/>

![](../Images/APIMColorAPI.png)

- Import swagger from > <https://markcolorapi.azurewebsites.net/swagger/v1/swagger.json>
  - Use "color" in URL for API

![](../Images/APIMAddColorAPI1.png)

![](../Images/APIMAddColorAPI2.png)

Remember to set a CORS policy.

The swagger file did not contain the name of the host so need to update

- Select [Settings]
- Amend Web Service URL to <https://markcolorapi.azurewebsites.net>

![](../Images/APIMAddColorAPI3.png)

We can test this from the [Test] tab

![](../Images/APIMAddColorAPI.png)

- Switch to the Developer portal and look at Color API
  - Try the RandomColor operation
- Look at Response / Trace ... see the random color returned

![](../Images/APIMColorTryIt1.png)

![](../Images/APIMColorTryIt2.png)

#### Rate limit

Use website <https://markcolorweb.azurewebsites.net> - this displays 500 lights.  Each light will at random intervals make a call to the RandomColor API - and then display the color returned.

![](../Images/APIMColorWeb.png)

Via the menu - there is a configution page to specify the API endpoint

![](../Images/APIMColorWebConfig.png)

- Open Developer portal and get API keys for Starter and Unlimited products
- Open Notepad - make note of URLs
  - <https://markharrison.azure-api.net/color/api/RandomColor?key=> *Starter-Key*
  - <https://markharrison.azure-api.net/color/api/RandomColor?key=> *Unlimited-Key*

![](../Images/APIMColorWebKeys.png)

- To see that Unlimited product has no rate limits
  - Configure Color Website to use Unlimited URL
  - Select [Start]
  - Notice there is no Rate Limit - every light is randomly updated

![](../Images/APIMColorWebUnlimited.png)

- To see that Starter product is limited to 5 calls per minute
  - Configure Color Website to use Starter URL
  - Select [Start]
  - Notice that only 5 lights get coloured
- Try URL with the Starter key, directly in the web browser address bar
  - Notice the error status / message returned
  - Example: *{ "statusCode": 429, "message": "Rate limit is exceeded. Try again in 54 seconds." }*

![](../Images/APIMColorWebStarter.png)

#### Caching

API Management can be configured for response caching - this can significantly reduce API latency, bandwidth consumption, and web service load for data that does not change frequently.

- Using the original Azure Management portal - set a caching Policy on the RandomColor API call
  - Set a caching duraction of 15 seconds
  - Simple caching configuration is not yet implemented in the Azure Management portal - we see shall see later how it can be done using policy expressions

![](../Images/APIMEnableCaching.png)

![](../Images/APIMEnableCaching2.png)

![](../Images/APIMEnableCaching3.png)

- Configure Color Website to use Unlimited URL
- Select [Start]
- Notice that for each 15 seconds period - the same color is set

![](../Images/APIMColorWebCaching.png)

#### Analytics

Analytics is available in the Azure management portal from the Analyics blade.

- Look at dashboard and detailed :  Timeline | Geography | APIs | Operations | Products | Subscriptions | Users | Requests

![](../Images/APIMAnalytics.png)

![](../Images/APIMAnalytics2.png)

---
[Home](apimanagement-0.md) | [Prev](apimanagement-2.md) | [Next](apimanagement-4.md)
