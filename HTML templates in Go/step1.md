---
title: 'Introduction '

---
<!--Introduction -->

In Go, **html/template** package is used to generate HTML outputs by implementing data-driven templates. 

Some of the syntax used by the package to render HTML pages include:

- **{{.}}**: This is a root element render
- **{{.Title}}**: This renders the "Title"-field
- **{{if .Done}} {{else}} {{end}}**: Is used to define the if-Statement
- **{{range .Items}} {{.}} {{end}}**: Is used to loop over "Items"
- **{{/* a comment */}}**: Is used to define a comment

In this scenario, we’ll use this package to create a simple web application that reads data from a txt file and displays it on a HTML form. The application will also have the capability to edit and save the data displayed.


Let’s start!