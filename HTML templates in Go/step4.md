---
title: Create HTML template file

---
<!--Create HTML template file-->

Let’s now create a template that will define how the loaded data will be displayed.

Create the file "view.html" by adding the code below:

```html
<h1> {{.Title}}</h1>
<label for="message">Message:</label><br><br>
<div>{{printf "%s" .Body}}</div>
<p><a href="/edit/{{.Title}}">Edit Message</a></p>
{{copy filename='view.html'}}
```

From the code above, the title is displayed in `<h1>` format. There is also an edit hyperlink defined by the tag `<a>` that sends the user to the `‘’/edit/’` page.

The `printf "%s" .Body` is a function that will output the`.Body` as a string.

Next, we’ll create a view handler.