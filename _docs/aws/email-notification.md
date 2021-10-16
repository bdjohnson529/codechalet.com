---
title:  "Serverless email notifications"
layout: blog
order: 0
topic: AWS
topic_path: /docs/aws/index.html
---
Email notifications are great. Using [Lambda](https://aws.amazon.com/lambda/) functions, [API Gateway](https://aws.amazon.com/api-gateway/) and [Simple Email Service](https://aws.amazon.com/ses/), you can collect information in an HTML form and send that information to your email. This guide will explain how to send data in client-side Javascript via an AJAX request, and receive the data in a Lambda function. The Lambda function can be used to send the email.

Let's take a moment to think about the architecture. There are at least two concerns, which we can define as
* Constructing an email
* Transmitting an email

Also consider that you will need both client-side AJAX function, and a Lambda function to receive the request. I found it helpful to separate the two concerns into two different functions. More on design later, for now, let's get to work!

In this example, let's pretend we are building a site for Phil the Painter. Phil wants new customers to be able to request a quote through the website. He even created an HTML form we can use. Go Phil!

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

Let's take care of the first task, and write a function to send an email via SES. I am going to demonstrate the function in Node.js but it could easily be programmed in Python as well.

```javascript
// index.js

var aws = require("aws-sdk");
var ses = new aws.SES({ region: "us-west-2" });

exports.handler = async function (event) {
  var params = {
    Destination: {
      ToAddresses: ["phil@fake.com"],
    },
    Message: {
      Body: {
        Text: { Data: "A customer requested a quote!" },
      },

      Subject: { Data: "Customer Reuest for Quote" },
    },
    Source: "phil@fake.com",
  };
 
  return ses.sendEmail(params).promise()
};
```

Our Lambda function is now capable of transmitting an email message to the `phil@fake.com`. Of course you may want to replace Phil's email address with your own. Once you have done this, let's test the function. You can do this by clicking the Test button in the AWS web editor.

You should receive an email. It may be in your Spam folder, because the email sender was listed as your account, but the message was delivered by SES. We will work to clear this up later.



# HTML Form
This is an HTML form you can use to collect information from the user.

<button onClick="ToggleElement('show-code-1')" class="btn btn-info">
  Show HTML Form
</button>


<div markdown="1" id="show-code-1" class="d-none">

```html
<form id="target">
  <label for="inputName"">Name</label>
  <input type="text" id="inputName" placeholder="Enter your name." required>

  <label for="inputEmail">Email</label>
  <input type="email" id="inputEmail" placeholder="Enter your email." required>

  <label for="inputDescription">Email</label>
  <textarea rows="5" id="inputDescription" placeholder="How can I help?" required>
  </textarea>

  <input type="submit" value="Request Quote" class="btn btn-primary">
</form>
```
</div>
