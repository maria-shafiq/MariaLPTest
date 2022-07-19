---
title: 'Creating the initial text file '

---
<!--Creating the initial text file -->

We’ll start by creating a txt file that will contain the body and title that we’ll use in the project.

Add the code below to create the file:

```
echo "Welcome to Brainarator's server. Feel free to edit me..." > learner.txt
{{ execute }}
```

In the next steps, we will build a web app that will do the following task: When we view a path, say `/view/<slug>`, our web app should show the <slug>.txt file content on the visited page. For example if <slug> is "learner", the web app should show `Welcome to Brainarator's server. Feel free to edit me...` on the web page (which is the content of the file learner.txt)/

In the page `/view/<slug>`, we are going to use the template generator from the standard library html/template. The page title is the filename (without the .txt extension)

According to the official documentation of Go, package template (html/template) implements data-driven templates for generating HTML output safe against code injection. It provides the same interface as package text/template and should be used instead of text/template whenever the output is HTML.

We will see how.