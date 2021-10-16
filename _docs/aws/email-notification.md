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

## Collecting Form Data
In this example, let's pretend we are building a site for Phil the Painter. Phil wants new customers to be able to request a quote through the website. He even created an HTML form we can use. Go Phil!

<button onClick="ToggleElement('show-code-1')" class="btn-lg btn-light">
  Show Code
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

## SES
AWS Simple Email Service can send emails to your personal or business email account. The first thing you will need to do is verify your email address. AWS will send you a verification email.

<br>

<div class="container">
  <button class="btn-lg btn-secondary">
    <i fa fa-play></i>
  </button>
  <img src="{{ site.baseurl }}/assets/img/docs/aws/ses-verify-email.gif" alt="SES Verify Email">
</div>

## Lambda
Now that you have verified your email address, we can construct a Lambda function to send an email. First, create a new Lambda function. Let's name it `sendEmailFunction`.

<br>
<img src="{{ site.baseurl }}/assets/img/docs/aws/lambda-create-function.gif" alt="SES Verify Email">
