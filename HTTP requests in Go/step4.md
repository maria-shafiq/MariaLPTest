---
title: POST requests

---
<!--POST requests-->

For this example, we are going to use httpbin.org, which is a simple HTTP request & response service. This is a useful tool to test HTTP requests.

In our case, since we are going to experiment with using POST requests, we will need to use this endpoint `https://httpbin.com/post`. This will simply return the POST data to us.

We are going to code a Go application that sends the equivalent of this CURL command:

```
curl -X POST https://httpbin.org/post \
-H 'Content-Type: application/json' \
-d '{"First Name":"John","Last Name":"Doe"}'
{{ execute }}
```

Let's see how to do it. Update the code.go file:

```go
package main
 
import (
    "bytes"
    "encoding/json"
    "fmt"
    "io/ioutil"
    "net/http"
)
 
func main() {
    jsonInfo := map[string]string{
        "First Name": "John", 
        "Last Name": "Doe"
        }
    infoValue, _ := json.Marshal(jsonInfo)    
    resp, err := http.Post("https://httpbin.org/post", "application/json", bytes.NewBuffer(infoValue))
    if err != nil {
        fmt.Printf("Failed with an error %s\n", err)
    } else {
        //Reading the response body.
        data, _ := ioutil.ReadAll(resp.Body)
        //Convert the body to type string
        fmt.Println(string(data))
    }
}
{{copy filename='code.go'}}
```

From the code above, we map the data we want to send and then convert it to JSON using the `json.Marshal()` function. 

The JSON data is then converted to bytes before being sent to the server. The response is read using `ioutil.ReadAll()` before being converted to a string.

Let us now run the application using the command below:

```
go run code.go
{{execute}}
```

Next, we’ll look at the key takeaways.