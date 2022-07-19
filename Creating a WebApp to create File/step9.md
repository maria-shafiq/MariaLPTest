---
title: Key Takeaways

---
<!--Key Takeaways-->
- We used the net/http package to create a simple webserver that shows files from the filesystem.
- We used the `http.ResponseWriter` to show contents on a web page (a text file content, or form ..etc).
- In the main function, we used `http.HandleFunc()` to link a route to a function. Example: `http.HandleFunc("/view/", viewHandler)`.