# API Management - Hands-on Lab Script - part 9

- [Part 1 - Create an API Management instance](apimanagement-1.md) 
- [Part 2 - Developer Portal and Product Management](apimanagement-2.md) 
- [Part 3 - Adding API's](apimanagement-3.md) 
- [Part 4 - Caching and Policy Expressions](apimanagement-4.md) 
- [Part 5 - Versioning and Revisions](apimanagement-5.md) 
- [Part 6 - Analytics and Monitoring](apimanagement-6.md) 
- [Part 7 - Security](apimanagement-7.md) 
- Part 8 - DevOps... this document

Please see [aka.ms/apimdevops](http://aka.ms/apimdevops) for (work in progress) guidance and tools around automating deployment across multiple API Management environments.

## CI/CD with API Management

The proposed approach is illustrated in the below picture. You can also [watch this video](https://www.youtube.com/watch?v=4Sp2Qvmg6j8) which explains the approach as well as demonstrates a sample implementation. 

![alt](Images/APIM-DevOps.png)

In this example, there are two deployment environments: Development and Production, each has its own API Management instance. API developers have access to the Development instance and can use it for developing and testing their APIs. The Production instance is managed by a designated team called the API publishers.

The key in this proposed approach is to keep all API Management configurations in Azure [Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates). These templates should be kept in a source control system. We will use GIT throughout this example. As illustrated in the picture, there is a Publisher repository that contains all configurations of the Production API Management instance in a collection of templates.

* **Service template**: contains all the service-level configurations of the API Management instance (e.g., pricing tier and custom domains). 
* **Shared templates**: contain shared resources throughout an API Management instance (e.g., groups, products, loggers). 
* **API templates**: include configurations of APIs and their sub-resources (e.g., operations, policies, diagnostics settings). 
* **Master template**: ties everything together by [linking](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-linked-templates) to all templates and deploy them in order. If we want to deploy all configurations to an API Management instance, we can just deploy the master template. Meanwhile, each template can also be deployed individually.

API developers will fork the publisher repository to a developer repository and work on the changes for their APIs. In most cases, they will focus on the API templates for their APIs and do not need to change the shared or service templates.

We realize there are two challenges for API developers when working with Resource Manager templates:

* First, API developers often work with [OpenAPI Specification](https://github.com/OAI/OpenAPI-Specification) and may not be familiar with Resource Manager schemas. Authoring templates manually might be an error-prone task. Therefore, we created a utility tool called [**Creator**](https://github.com/Azure/azure-api-management-devops-resource-kit/blob/master/src/APIM_ARMTemplate/README.md#Creator) to automate the creation of API templates based on an Open API Specification file. Optionally, developers can supply API Management policies for an API in XML format. Basically, the tool inserts the Open API specification and policies into a Resource Manager template in the proper format. With this tool, API developers can continue focusing on the formats and artifacts they are familiar with.

* Second, for customers who have already been using API Management, another challenge is how to extract existing configurations into Resource Manager templates. For those customers, We have created another tool called [**Extractor**]([./src/APIM_ARMTemplate/README.md#extractor](https://github.com/Azure/azure-api-management-devops-resource-kit/blob/master/src/APIM_ARMTemplate/README.md#extractor)) to help them generate templates by extracting configurations from their exisitng API Management instances.  

Once API developers have finished developing and testing an API, and have generated the API template, they can submit a pull request to merge the changes to the publisher repository. API publishers can validate the pull request and make sure the changes are safe and compliant. For example, they can check if only HTTPS is allowed to communicate with the API. Most of these validations can be automated as a step in the CI/CD pipeline. Once the changes are approved and merged successfully, API publishers can choose to deploy them to the Production instance either on schedule or on demand. The deployment of the templates can be automated using [Github Actions](https://github.com/Azure/apimanagement-devops-samples), [Azure Pipeline](https://docs.microsoft.com/en-us/azure/devops/pipelines/?view=azure-devops), [PowerShell](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-template-deploy), [Azure CLI](Azure-cli-example.md) or other tools.

With this approach, the deployment of API changes into API Management instances can be automated and it is easy to promote changes from one environment to another. Since different API development teams will be working on different sets of API templates and files, it prevents interference between different teams.

We realize our customers bring a wide range of engineering cultures and existing automation solutions. The approach and tools provided here are not meant to be a one-size-fits-all solution. That's why we created this repository and open-sourced everything, so that you can extend and customize the solution.


## Alternatives

* For customers who are just starting out or have simple scenarios, they may not necessarily need to use the tools we provided and may find it easier to begin with the boilerplate templates we provided in the [example]([./example/](https://github.com/Azure/azure-api-management-devops-resource-kit/tree/master/example)) folder.
* Customers can also run [PowerShell](https://docs.microsoft.com/powershell/module/azurerm.apimanagement/?view=azurermps-6.13.0) scripts as part of their release process to deploy APIs to API Management.
* There is also a **non-official** Azure DevOps [extension](https://marketplace.visualstudio.com/items?itemName=stephane-eyskens.apim) created by [Stephane Eyskens](https://stephaneeyskens.wordpress.com/)

---
[Home](README.md) | [Prev](apimanagement-7.md) 