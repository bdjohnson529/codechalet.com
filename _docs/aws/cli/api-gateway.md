---
title:  "API Gateway"
layout: blog
order: 1
topic: AWS
topic_path: /docs/aws/index.html
---
Before we discuss API Gateway, let's take a moment to discuss REST APIs and HTTP requests. REST is an interface specification which can be applied to the architecture of [application-layer](https://osi-model.com/application-layer/) systems. In a REST API, the client sends HTTP requests, and the server replies with HTTP responses.

[HTTP requests](https://www.ibm.com/docs/en/cics-ts/5.3?topic=protocol-http-requests) have three components: a method, headers, and an optional message body. Examples of request methods include `GET`, and `POST`. Headers and the message body contain the information which is transmitted as part of the request or response.

## Configurations
API Gateway presents you with four configuration options:

* HTTP API
* WebSocket API
* REST API
* REST API (Private)

It's interesting that API Gateway makes a distinction between [HTTP APIs and REST APIs](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-vs-rest.html), because [REST](https://www.redhat.com/en/topics/api/what-is-a-rest-api) is an interface specification and [HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP) is a data transmission protocol. That is to say, all REST APIs will incorporate HTTP requests. However, all HTTP requests are not necessarily part of a RESTful interface.

Semantics aside, it seems that the HTTP option requires less setup. It also seems that the HTTP option is a more recent feature with less documentation.

## Creating a Method
Once you have created the API, you will need to create a method. Methods are associated with resoures (paths) in API Gateway. Your API might have several resources, for example, cats, dogs and mice. Each resource will have a different path - for example, the cats resource might have the path `/cats`, dogs would have the path `/dogs` and so on. In the console, you can create methods for each of your resources. In the GIF below, I create a POST method for the `root` resource, at the root path, `/`.

<div class="container">
  <button onClick="PlayGif('gif-1')" class="btn-lg btn-secondary">
    <i class="fa fa-play"></i>
  </button>
  <img src="{{ site.baseurl }}/assets/img/docs/aws/apigateway-create-action.gif" alt="SES Verify Email">
</div>


## Lambda Function Integration
Before you save your method, you'll need to associate the method with some code. One common configuration is associating a method with a Lambda function, so that the API call triggers the Lambda function. 

API Gateway offers the option of transforming the data in our request before invoking the Lambda function. In our case, we don't need to perform any transformation, and we can simply forward the request to the Lambda function. For this reason, we want to make this integration a Lambda proxy integration. [Proxy integrations](https://docs.aws.amazon.com/apigateway/latest/developerguide/set-up-lambda-proxy-integrations.html) do not transform requests or responses between the client and the Lambda function.

<img src="{{ site.baseurl }}/assets/img/docs/aws/apigateway-lambda-proxy-integration.png"
     alt="API Gateway Lambda Proxy Integration">


## CORS
[CORS]((https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)) is a protocol that governs how endpoints respond to requests from other websites. In particular, CORS is going to verify the presence of three headers in the API's response: `Access-Control-Allow-Headers`, `Access-Control-Allow-Origin`, and `Access-Control-Allow-Methods`.

Many browsers will make a [preflight request](https://developer.mozilla.org/en-US/docs/Glossary/Preflight_request) before issuing a CORS request, to ensure that the server is aware of CORS. The preflight request is an `OPTIONS` request, and the browser will verify the response before issuing the `POST` request. If the server issues an incomplete or missing response to the `OPTIONS` request, the browser will skip the `POST` request.

Use the AWS Console to enable CORS. Select the **Resources** pane. Within the **Actions** menu, select the option **Enable CORS**. You'll need to add the header `authtoken` to the list of `Access-Control-Allow-Headers`. You will also be able to see that there are two `Access-Control-Allow-Methods`: `POST`, and `OPTIONS`. The CORS wizard is going to add the `OPTIONS` resource for us, so that our API can fulfill the preflight request.

<div class="container">
  <button onClick="PlayGif('gif-1')" class="btn-lg btn-secondary">
    <i class="fa fa-play"></i>
  </button>
  <img src="{{ site.baseurl }}/assets/img/docs/aws/apigateway-cors.gif" alt="API Gateway CORS">
</div>