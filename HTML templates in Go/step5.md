---
title: Create a view handler

---
<!--Create a view handler-->

In this step, we’ll create a handler that will allow us to view the HTML file created in the previous step. To do this we need to add the **html/template** package that is part of the Go standard library. This is what allows us to have the HTML content file in a different file.

Add the code below to implement this:

```go
package main
 
import (
***    
    "html/template"
***    
    "io/ioutil"
    "log"
    "net/http"
)
 
type Page struct {
    Title string
    Body  []byte
}
 
func (p *Page) save() error {
    filename := p.Title + ".txt"
    return ioutil.WriteFile(filename, p.Body, 0600)
}
 
func loadPage(title string) (*Page, error) {
    filename := title + ".txt"
    body, err := ioutil.ReadFile(filename)
    if err != nil {
        return nil, err
    }
    return &Page{Title: title, Body: body}, nil
}
 
***
func renderTemplate(w http.ResponseWriter, tmpl string, p *Page) {
    t, _ := template.ParseFiles(tmpl + ".html")
    t.Execute(w, p)
}
 
func viewHandler(w http.ResponseWriter, r *http.Request) {
    title := r.URL.Path[len("/view/"):]
    p, _ := loadPage(title)
    renderTemplate(w, "view", p)
}
***
func main() {
***
    http.HandleFunc("/view/", viewHandler)
***    
    log.Fatal(http.ListenAndServe(":5000", nil))
}
{{copy filename='code.go'}}
```

From the code above, "Title" is extracted from `r.URL.Path`, the path component of the request URL. 

"Path" is re-sliced with `[len("/view/"):]` to drop the leading `/view/` component of the request path. This is because the path will invariably begin with `/view/`, which is not part of the Page's title. The separate `.html` is handled by the `renderTemplate()` function.

The function takes three arguments: 
- The `http.ResponseWriter`, 
- data as string, 
- and the Page struct pointer. 

The function `template.ParseFiles()` will read the contents of view.html and return a `template.Template`.

The method `t.Execute()` executes the template, writing the generated HTML to the `http.ResponseWriter`.

Let's initialize the application if it's not already done:

```
go mod init my_mod
{{ execute }}
```

Start the server using gin and send it to the background:

```
nohup gin --immediate &
{{ execute }}
```

The server is running on port 5000.

View the page associated to the text file "learner.txt" here:

```
[]('{{webUrl}}' "5000")/view/learner
```

If you look at the source page of this web page:

```
curl http://0.0.0.0:5000/view/learner
{{ execute }}
```

You should see:

```html
<h1> learner</h1>
<label for="message">Message:</label><br><br>
<div>Welcome to Brainarator&#39;s server. Feel free to edit me...
</div>
<p><a href="/edit/learner">Edit Message</a></p>
```

Which is generated from this template:

```html
<h1> {{.Title}}</h1>
<label for="message">Message:</label><br><br>
<div>{{printf "%s" .Body}}</div>
<p><a href="/edit/{{.Title}}">Edit Message</a></p>
```


Next, we’ll look at how we can edit the page.