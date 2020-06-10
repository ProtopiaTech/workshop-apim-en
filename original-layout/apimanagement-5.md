# API Management - Hands-on Lab Script - part 5

Mark Harrison : checked & updated 12 March 2020 - original 1 Nov 2017

![](../Images/APIM.png)

- [Part 1 - Create an API Management instance](apimanagement-1.md)
- [Part 2 - Developer Portal](apimanagement-2.md)
- [Part 3 - Administration](apimanagement-3.md)
- [Part 4 - Policy Expressions](apimanagement-4.md)
- [Part 5 - API Proxy to other Azure services](apimanagement-5.md) ... this document

## API Proxy to other Azure services

### Azure Functions

- Create a simple function that is Triggered by an HTTP Request

Example:

![](../Images/APIMFunctionExample.png)

```c#
    string[] strColors = { "blue", "lightblue", "darkblue" };
//  string[] strColors = { "green", "lightgreen", "darkgreen" };

    Random r = new Random();
    int rInt = r.Next(strColors.Length);

    return req.CreateResponse(HttpStatusCode.OK, strColors[rInt]);
```

Lets add the function to API Managament.   In the API blade select [+Add API] and the [Function App] tile

![](../Images/APIMFunctionAddAPI.png)

- Select the [Browse] button to get a list of Functions in the subscription

![](../Images/APIMFunctionAddBrowse.png)

- Select the function

![](../Images/APIFunctionSelect.png)

- Amend the Names / Descriptions, URL suffix and select the Products

![](../Images/APIMFunctionCreate.png)

- As previously add CORS policy

- Validate the function works - either from the Azure management portal or the developer portal

![](../Images/APIMFunctionTest1.png)

![](../Images/APIMFunctionTest2.png)

### Azure Logic Apps

- Create a simple logic app that is Triggered by an HTTP Request

Example:

![](../Images/APIMLogicAppExample1.png)

![](../Images/APIMLogicAppExample2.png)

Use the following sample message to generate the schema of the Request body payload.  By specifying the schema, the individual fields (in this case `msg`) can be extracted and referred to in the subsequent logic

```json
{
  "msg": "text"
}
```

Lets add the function to API Managament. In the API blade select [+Add API] and the [Logic App] tile

![](../Images/APIMLogicAppAddAPI.png)

- Select the [Browse] button to get a list of Logic Apps in the subscription

![](../Images/APIMLogicAppAddBrowse.png)

- Select the Logic App

![](../Images/APILogicAppSelect%20.png)

- Amend the Names / Descriptions, URL suffix  and select the Products

![](../Images/APIMLogicAppCreate.png)

 As previously add CORS policy

- Validate the Logic App works - either from the Azure management portal or the developer poral

![](../Images/APIMLogicAppTest1.png)

![](../Images/APIMLogicAppTest2.png)

- Check the Logic App audit

![](../Images/APIMLogicAppTest3.png)

- Check the email was sent

![](../Images/APIMLogicAppTest4.png)

---
[Home](apimanagement-0.md) | [Prev](apimanagement-4.md)
