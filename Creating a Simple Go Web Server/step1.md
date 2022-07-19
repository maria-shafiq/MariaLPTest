---
title: Introduction

---
<!--Introduction -->
Let’s start by understanding what a web server is and what it does.


A web server is used in web hosting or the hosting of data for websites and web-based applications or web applications. It delivers content for a website to a client that requests it, like a web browser. It communicates with a web browser using HTTP.

At the most basic level, whenever a browser needs a file that is hosted on a web server, the browser requests the file via HTTP. When the request reaches the correct (hardware) web server, the (software) HTTP server accepts the request, finds the requested document, and sends it back to the browser, also through HTTP.

In Go, we can build a web server using the `net/http` package.

In this scenario, we’ll create a simple server to help us understand server handling in Go.