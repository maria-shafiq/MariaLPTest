---
title: Auto reloading the server

---
<!--Auto reloading the server-->
<!--Please install go get github.com/codegangsta/gin -->

Before we move to code, we need to understand that by running `go run code.go`, our web server will not take code changes into consideration.
We should always kill the server and restart it again.

To avoid this, we are going to use [gin](https://github.com/codegangsta/gin).

gin is a simple command line utility for live-reloading Go web applications. gin runs as a proxy, it automatically recompiles code when it detects a change.

Let's run gin in the background for now. To do this, we need to create a module:

```
go mod init webserver
{{ execute }}
```

Then launch gin:

```
nohup gin --immediate &
{{ execute }}
```