---
title:  "Serverless Javascript"
layout: blog
order: 1
topic: Javascript
topic_path: /docs/javascript/index.html
---
Javascript enjoys a number of frontend frameworks which have become extremely popular among web developers. React, Vue, Angular, Ember are just some of the Javascript frameworks that can be used to design Single Page Applications (SPAs). SPAs are pages which use Javascript to update the page, rather than performing a HTTP request to the server and reloading the page on receipt of data.

SPAs are great. They can be used to build impressive frontends. The UX feels more immersive, since you are not reloading the entire page each time you toggle the view. In theory, views load faster than they would if you had to wait for a request to make a trip to the server and back.

However, SPAs also require a server. What if you wanted to build a static website?

### Static Websites
Static websites are also great. They are easy to maintain, and dirt cheap to host. You can host a static website on AWS for less than $1 per month (S3 + CloudFront).

Let's say you have a blog which does not need to store any user data, but you want the user to be able to filter the blog posts. Enter serverless Javascript!

### Render everything
Let's say you have a page which displays a set of travel destinations. The user needs to filter the destinations by country. For our purposes, we can say that the HTML page will look approximately like this:
```html
<div id="Denver" class="destination">
  <img src="img/Denver">
</div>
<div id="Chicago" class="destination">
  <img src="img/Chicago">
</div>
<div id="London">
  <img src="img/London" class="destination">
</div>
```

### Filtering in Javascript
Our filtering function will add the HTML `hidden` attribute to the `divs` which need to be hidden. We can retrieve a `HTMLCollection` with the containing `divs` by selecting all elements with the class name `destination`. The `getElementsByClassName` API does this quite nicely.

Using another web API, `element.classList.add`, we can add the `hidden` attribute to the `divs` which we don't want to display to the user. We are rendering everything, and then hiding the `divs` which we don't want to see. Of course we could approach this problem the other way round and hide all the divs when the page first loads, and use our Javascript function to show the divs which we want the user to see.
```javascript
function FilterDestinations(filter) {
  // get list of destinations
  var destinations = document.getElementsByClassName("destination");

  // iterate through destinations
  if (filter == "UK") {
    for (let destination of destinations) {
      if (destination.id != "London") {
        destination.classList.add("hidden");
      }
    }
  } else if (filter == "US") {
    for (let destination of destinations) {
      if (destination.id == "London") {
        destination.classList.add("hidden");
      }
  }
}
```

### Adding Buttons
We can now add two buttons which launch the `FilterDestinations()` function. The two buttons will pass different parameters to the Javascript function: one to filter to the US, and the other to filter to the UK.
```html
<button onclick="FilterDestinations('UK')">Filter to UK</buton>
<button onclick="FilterDestinations('US')">Filter to US</buton>
```

In this way, the user can filter the results displayed on a page, and we do not need to deploy a server! This concept can be applied to images, or even tabular results.

## Limitations
This method will have limited effectiveness when the data on the page grows in size. For a few dozen entries, the serverless option will do just fine. However, if you were filtering thousands of destinations, it would not make sense to render all of them and then hide the ones which are not selected. Load times would be slow, and there is a more efficient way to solve that problem.

For blogs or other small websites, this technique works great!