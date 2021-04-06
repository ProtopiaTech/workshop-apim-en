# API Management - Hands-on Lab Script - part 2

- [Lab Prerrequisites](apimanagement-prerrequisites.md)
- [Part 1 - Create an API Management instance](apimanagement-1.md) 
- Part 2 - Developer Portal and Product Management (You are here)
- [Part 3 - Adding API's](apimanagement-3.md)
- [Part 4 - Policy Expressions](apimanagement-4.md)
- [Part 5 - Versioning and Revisions](apimanagement-5.md)
- [Part 6 - Analytics and Monitoring](apimanagement-6.md)
- [Part 7 - Security](apimanagement-7.md)
- [Part 8 - DevOps](apimanagement-8.md)

## Developer Portal

The developer portal is an automatically generated, fully customizable website with the documentation of your APIs. It is where API consumers can discover your APIs, learn how to use them, request access, and try them out. 

### Publishing the developer portal

Accessing from the link in the Overview blade of the Azure Management Portal, will display the developer portal in admin / edit mode and you can customize it.
Using the left-side menu `Portal Overview` Icon - select the `Publish` button.  It will then be available for users to access.

![](Images/apim-developerportal-publish.png)

### Enabling CORS for the developer portal

Cross-origin resource sharing is a mechanism that allows resources on a web page to be requested from another domain, outside the domain from which the first resource was served. CORS is required to let portal visitors use the interactive console in the API reference pages and should be enabled for domains, including custom domains.

CORS is enabled by using policies, we will go deep on this topic in part 4. For now we will enable this using a builtin UI. To do this, using the left-side menu `Portal Overview` Icon - select the `Enable CORS` button.

![](Images/apim-developerportal-CORS.png)

After publishing the portal and enabling CORS, we should access the developer portal located at: {apim-service-name}.developer.azure-api.net

![](Images/APIMDeveloperPortal.png)


### User Experience

Let's experience how your users will navigate through your portal

#### Anonymous User

As an unauthenticated user (=open URL in a new browser), look around the developer portal, and check the Products.

> Notice the difference between the Starter & Unlimited products

![](Images/APIMDevPortalProducts.png)

You can also check the APIs. As you can see, all operations exposed are described and can also be tested directly within the portal.

![](Images/APIMDevPortalAPIs.png)

#### Register for an account

Let's sign up for an account (If logged in as Administrator - log out)

![](Images/APIMDevSignup.png)

Check acceptance email and confirm to activate account

![](Images/APIMDevSignupEmail.png)

Sign into account

![](Images/APIMDevSignin.png)


Select Starter Product and subscribe to a "Starter" subscription
  - Check email - subscription has been accepted and some key information are provided

Select Unlimited Product and subscribe to an "Unlimited" subscription
  - Check email - the subscription requires approval 

![](Images/APIMDevSubscribe.png)

Check the user profile page - see products and keys
  - Note that the Unlimited subscription is not yet *Active* as this request has not yet been approved (status=submitted)

![](Images/APIMDevSubscribe2.png)

The "Unlimited" being in "submitted" state (=needs approval), you can, in Azure Portal, go in the `subcriptions` blade to approve it.

#### Try an API

It's now time to test one of the published APIs. Open the APIs page and look at the Echo API
  - Notice the developer information
  - Test the Echo API using the GET verb 

![](Images/APIMDevTryAPI.png)

![](Images/APIMDevTryAPI2.png)

### Customising the Developer Portal

#### Site Configuration

The developer portal is based on a fork of the Paperbits Web framework <https://paperbits.io/>, and is enriched with API Management-specific features.  The fork resides at <https://github.com/Azure/api-management-developer-portal>.

It is possible to self-host, and manage your own developer portal outside of an API Management instance. It's an advanced option, which allows you to edit the portal's codebase and extend the provided core functionality. This is documented at <https://github.com/Azure/api-management-developer-portal/wiki>/ and <https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-developer-portal>.

Before you make your portal available to the visitors, you should personalize the automatically generated content. Recommended changes include the layouts, styles, and the content of the home page. This is documented at <https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-developer-portal-customize>

Video on customization is available at <https://www.youtube.com/watch?v=5mMtUSmfUlw>

![](Images/APIMDevConfig.png)

![](Images/APIDevConfig2.png)

![](Images/APIMDevStyles.png)

#### Email Configuration

The templates for the email notifications are managed from the Azure Management Portal, directly on the blade's side menu.
Look at the available notifications and notifications templates which are customizable

![](Images/APIMNotifications.png)

![](Images/APIMNotificationTemplates.png)

![](Images/APIMNotificationEdit.png)


### Product Management

A product contains one or more APIs as well as a usage quota and the terms of use. Once a product is published, developers can subscribe to the product and begin to use the product's APIs.

#### Product definition

Again in the Azure Management portal, open the left menu `Products `

![](Images/APIMProducts.png)

Add a new product - for example a Gold tier - change its visibility (Published) and click on the [Create] button

![](Images/APIMAddProduct.png)

![](Images/APIMAddProduct2.png)

Set Access Controls to allow access to developers and guests

![](Images/APIMAddProductsAccess.png)

Once saved, see the new Gold Tier product in the Developer portal

![](Images/APIMAddProductsDevPortal.png)

---
[Home](README.md) | [Prev](apimanagement-1.md) | [Next](apimanagement-3.md)
