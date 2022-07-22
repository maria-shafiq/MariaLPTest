---
title: How to define a package?

---
<!--

-->

Go is an open source strong statically typed language initially developed by a small team at Google. 

It's described as strong typed because the type of variable cannot be changed over time after it has been declared and statically typed because, at compile-time, all the variables have to be defined. 

Although there are ways to get around this, you’ll in most cases not be able to escape these two properties.

Let us now write our first Go application. We’ll call this application “Hello World”.

All Go applications are structured into packages and in our case, the package is `main`. This will serve as an entry point to the application. Add the package by entering the code below.

{{copy filename='code.go'}}
```go
package main
```
{{ /copy }}

Next, we will import the necessary libraries.
