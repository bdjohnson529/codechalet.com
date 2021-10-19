---
title:  "Lambda Functions"
layout: blog
order: 0
topic: AWS
topic_path: /docs/aws/index.html
---
Using [Lambda](https://aws.amazon.com/lambda/) functions, [API Gateway](https://aws.amazon.com/api-gateway/) and [Simple Email Service](https://aws.amazon.com/ses/), you can send data from a static site to your email. This first chapter will explain how to send an email using Lambda and SES.

Let's take a moment to think about the generic problem of sending an email. The solution architecture will involve at least two concerns, which we can define as
* Constructing an email
* Transmitting an email

I found it helpful to separate the two concerns entirely by using the frontend to construct the email, and the API to transmit the message. The advantage to this architecture is the flexibility of our API - since we are not using the API to format the message, we can use it to send emails with different types of formatting.

<img src="{{ site.baseurl }}/assets/img/docs/aws/serverless-email-architecture.png"
     alt="Serverless Email Architecture">

In this example, let's pretend we are building a site for Phil the Painter. Phil wants new customers to be able to request a quote through his website. In a good month, Phil *might* have 100 customers contacting him through the site. Clearly, Phil's site does not have any major performance considerations (yet!) and we can take advantage of a serverless architecture.

# SES
AWS Simple Email Service can send emails to your personal or business email account. The first thing you will need to do is verify your email address. In the AWS console, navigate to SES. There, you can initiate a verification of an email account. SES will send an email as part of the verification process, follow the instructions to verify your email.

<br>

<div class="container">
  <button onClick="PlayGif('gif-1')" class="btn-lg btn-secondary">
    <i class="fa fa-play"></i>
  </button>
  <img id="gif-1" src="{{ site.baseurl }}/assets/img/docs/aws/ses-verify-email.gif" alt="SES Verify Email">
</div>

<br>

# Lambda
Now that you have verified your email address, let's construct a Lambda function to send an email. First, navigate to Lambda in the AWS Management Console. Create a new Lambda function, and name it something like `sendEmail`.

<br>

<div class="container">
  <button onClick="PlayGif('gif-1')" class="btn-lg btn-secondary">
    <i class="fa fa-play"></i>
  </button>
  <img src="{{ site.baseurl }}/assets/img/docs/aws/lambda-create-function.gif" alt="SES Verify Email">
</div>

The `sendEmail` function will be the sole executor of our API. This function will be invoked by API Gateway. The function has several resposibilities:

* Transmit email to email account via SES
* Receive data from AJAX request

Let's take care of the first responsibility, and write a function to send an email via SES. I am going to demonstrate the function in Node.js but it could easily be programmed in Python as well.

When a Lambda function is invoked, the runtime passes three arguments to the [handler method](https://docs.aws.amazon.com/lambda/latest/dg/nodejs-handler.html): an `event` object, a `context` object, and  a `callback` function. Right now we aren't going to concern ourselves with any of these arguments, and we will simply use the function invocation to trigger a boilerplate email notification. Later on, we will use data from the `event` object to construct the email.

We will use the [`sendEmail`](https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS/SES.html#sendEmail-property) function from the AWS Javascript SDK to compose an email and push it to the queue. Note that `sendEmail` inherits from [`AWS.Request`](https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS/Request.html), which is an asynchronous callback function. Since `sendEmail` executes asynchronously, we need to wait for it to return before we return from the Lambda function; otherwise, the Lambda function will terminate prematurely. The [`await`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/await) operator will pause the execution of our Lambda function until the `sendEmail` function settles its promise.

```javascript
// index.js

var aws = require("aws-sdk");
var ses = new aws.SES({ region: "us-west-2" });

exports.handler = async function (event) {
  var source = "bdjohnson529@gmail.com";
  var destination = "bdjohnson529@gmail.com";
  var subject = "Test email from AWS";
  var body = "This email was sent by AWS Lambda";

  var params = constructEmailParams(source, destination, subject, body);
 
  await ses.sendEmail(params).promise()
  return 0;
};

function constructEmailParams(source, destination, subject, body) {
  var params = {
    Destination: {
      ToAddresses: [destination],
    },
    Message: {
      Body: {
        Text: { Data: body },
      },

      Subject: { Data: subject },
    },
    Source: source,
  };
  
  return params;
}
```

Our Lambda function is now capable of transmitting an email message to the `phil@fake.com`. The email will tell Phil that a customer requested a quote. Our next step is to test this function. First, you will need to manually deploy your code within the Lambda editor, by clicking the Deploy button. After you have done this, click the Test button.

You should receive an email. It may be in your Spam folder, because the email sender was listed as your account, but the message was delivered by SES. We will work to clear this up later.

<br>
<a href="/docs/aws/tutorials/api-gateway.html"
   class="btn-lg btn-primary">Next</a>