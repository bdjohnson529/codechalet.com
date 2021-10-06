---
title:  "HTML Over the Wire"
layout: blog
order: 2
topic: Javascript
topic_path: /docs/javascript/index.html
---
The guys at Basecamp have developed an interesting perspective to approach building modern web applications. The popular SPA approach often sends JSON from the server to the client browser, and Javascript running in the client browser filters the JSON and arranges it into a meaningful display.

But what if we didn't send JSON over the wire? What if there was a way to send HTML over the wire, and make it look sexy? One of the advantages of SPAs is that they can update *part* of a page, rather than the entire page.

Let's consider a scenario : we have a tabular display, and the user wants to apply some filters. Using the SPA approach, we would send all the data for the display as JSON to the client browser. The JS would then apply the filters, and refresh the view.

### Server-based approach
Instead, if we are using the server to apply the filter, the client would make a request to the server with the filter parameters. The server would fulfill this request by sending an HTML response to the client browser. The client browser would refresh the page, and the user would see the filtered table.

There are a couple disadvantages to this approach. First, the page refresh is not ideal. It adds loading time to the UX, and can cause the user to lose their place if the entire page is reloaded. And if we only want to change one part of the page, it does not make sense to reload the entire page if we can avoid it.

So, how can we reload part of a page while still using the server to apply our filter?

### Turbo Frames
Turbo is one of the frontend frameworks supplied as part of the Hotwired kit. Per [their website](https://turbo.hotwired.dev/handbook/frames) - Turbo Frames allow predefined parts of a page to be updated on request. So if you want to apply a filter and update a table, you can define the table within a Turbo Frame. When the user applies a filter by clicking a button, the browser makes a request to the server. The response is used to populate the HTML within the Turbo Frame. Nothing changes outside the Turbo Frame.

In the example below, I use ERB to iterate through the instance variable `@users`. The example will look familiar if you use Rails, however, this example applies to any backend framework.
```html
<turbo-frame id="users">
  <table>
    <thead>
      <tr>
        <th>Name</th>
        <th>Email</th>
      </tr>
    </thead>

    <tbody>
      <% @users.each do |user| %>
        <tr>
          <td>
            <p>
              <%= user.name %>
            </p>
          </td>
          <td>
            <p>
              <%= user.email %>
            </p>
          </td>
        </tr>
      <% end %>
    </tbody>
  </table>
</turbo-frame>
```

Now, let's say we want to add a text search. We can add a form with an `input` element, which submits a request to the appropriate HTTP method. We want to add this form within the existing `turbo-frame` so that the results of the request will be used to replace the contents of that frame.
```html
<turbo-frame id="users">
  <form action="/sort_users" data-turbo-frame="users">
    <input name="query">
    <button>Search</button>
  </form>

  ...

</turbo-frame>
```

When the user types a name in the input and clicks Search, a request will be submitted to the path `sort_users`. The server will handle the request, parse the parameters and respond with HTML. Turbo will intercept this HTML and use it to populate the `turbo-frame` element with the `users` ID.

### Limitations
Using the server to perform operations on the data can be advantageous, but there are also times when it would make more sense to use the client browser to perform the operation. In the above example, depending on the size of the dataset, it may make more sense to send all the data to the client browser and use Javascript in the browser to perform the filtering. It really comes down to the specifics of your situation.

### Advantages
In the case that you can live with the server/client latency, this method provides an alternative way to modify the display without using the client browser to generate HTML. In some cases, this will be cleaner and easier to implement than implementing a SPA framework in the browser.