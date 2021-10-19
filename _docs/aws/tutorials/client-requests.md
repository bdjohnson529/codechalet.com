---
title:  "Client Requests"
layout: blog
order: 4
topic: AWS
topic_path: /docs/aws/index.html
---
This is the fourth chapter of the guide explaining how to build a serverless notification system using AWS. Here is a review of the first three chapters.
1. We built a Lambda function which is capable of sending an email via SES.
2. We created an API Gateway to invoke the Lambda function.
3. We created an authorization function for API Gateway.

In this chapter we will learn how to make a request from the client browser to the API.

## Fetch API
We will be using Javascript in the client browser to make the request to our API Gateway. Specifically, we will use the [`Fetch`](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) API to make an HTTP request. Let's start by constructing an asynchronous function to make a POST request. Notice that we are once again making use of the `await` operator. Fetch is asynchronous, so we need to block the execution of the `postRequest` function until our `fetch` request is completed.
```javascript
async function postRequest(url = '', data = {}) {
  const response = await fetch(url, {
    method: 'POST',
    mode: 'cors',
    headers: {
      'Content-Type': 'application/json',
      'authtoken': 'supersecretvalue'
    },
    body: JSON.stringify(data)
  });

  return response;
}
```



We probably want to encapsulate the `postRequest` function in another function, which will be called directly by the button which the user clicks to submit the form. That way, we can interpret the response and add logic which notifies the user that the form has been submitted. Let's create an addition function, `triggerAPI`, which calls `postRequest`.
```javascript
function triggerAPI() {
  var url = "https://api-gateway-prod-stage-url";

  postRequest(url, { answer: 42 })
    .then(data => {
      console.log(data);
    });
}
```

## HTML Button
Somewhere on our site, we can add an HTML button which triggers our Javascript function. Create a simple button with an `onClick` attribute.
```html
<button onclick="triggerAPI()">Send Email</button>
```

Now, you can use the button to trigger the API! When you click the button, you should receive an email in your inbox. Voila!

<br>
<a href="/docs/aws/tutorials/api-gateway-authorization.html"
   class="btn-lg btn-secondary">Previous</a>