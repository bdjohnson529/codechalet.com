---
title:  "AJAX Requests"
layout: blog
order: 4
topic: AWS
topic_path: /docs/aws/index.html
---
This is the third part of the guide explaining how to build a serverless notification system using AWS. In the first chapter, we built a Lambda function which is capable of sending an email via SES. In the second chapter, we created an API Gateway to invoke the Lambda function. In this chapter we will learn how to transmit data in AJAX requests from the client to API Gateway.

## HTML Form
Phil has specified the HTML form which he wants to use on his website. Go Phil! Take this form and add it to your static site. The form will collect data from the user.

```html
<form id="target">
  <label for="inputName"">Name</label>
  <input type="text" id="inputName" placeholder="Enter your name." required>

  <label for="inputEmail">Email</label>
  <input type="email" id="inputEmail" placeholder="Enter your email." required>

  <label for="inputDescription">Description</label>
  <textarea rows="5" id="inputDescription" placeholder="How can I help?" required>
  </textarea>

  <input type="submit" value="Request Quote" class="btn btn-primary">
</form>
```

## Prevent Form Submission
We can use a little client-side Javascript (Jquery, specifically) to intercept the form submission. Notice how the `<form>` above has the `id` attribute set to `target`. We can locate the form using this ID. The standard Javascript function [`Event.preventDefault()`](https://developer.mozilla.org/en-US/docs/Web/API/Event/preventDefault) is used to prevent the submission of the form.
```javascript
// form.js

$(document).ready(function(){
  $( "#target" ).submit(function( event ) {
    event.preventDefault();
  });
});
```

## Collect Form Inputs
Our Javascript functions can access the values of the form inputs by using `event.target`, since the function is triggered by the form element. Let's store the values of the form elements as variables scoped within our function. If you want to test that values are being collected within your function, you can output them to the console using `console.log()`.
```javascript
// form.js

$(document).ready(function(){
  $( "#target" ).submit(function( event ) {
    var inputName = event.target.inputName.value;
    var inputEmail = event.target.inputEmail.value;
    var inputPhone = event.target.inputPhone.value;
    var inputDescription = event.target.inputDescription.value;
    
    ...
```

## AJAX Request
Now that we have collected the form values, we need to package them into a request.


<br>
<a href="/docs/aws/api-gateway.html"
   class="btn-lg btn-secondary">Previous</a>