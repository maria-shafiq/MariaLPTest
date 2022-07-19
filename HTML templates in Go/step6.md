---
title: 'Editing the displayed page '

---
<!-- Editing the displayed page -->

In the previous step, we displayed the content of `learner.txt` using the template in `view.html`. 
The displayed page has an "edit" hyperlink which we shall now handle its function. To achieve this, we’ll create an "edit.html" template from which we’ll edit all files.

Create the file by adding the code below:

```html
<h1>Editing {{.Title}}</h1>
<form action="/save/{{.Title}}" method="POST">
<div><textarea name="body" rows="5" cols="40">{{printf "%s" .Body}}</textarea></div><br>
<div><input type="submit" value="Save"></div>
</form>
{{copy filename='edit.html'}}
```

The code above allows us to edit the file content and save it.

Now, let’s see how the edit is handled by Go.