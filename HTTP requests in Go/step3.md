---
title: Format response

---
<!--Format response-->

To make sense of the response that was returned by the GET function we need to access the response struct’s Body property and read it. We achieve this by using `ioutil.ReadMe` function that takes the response body as the argument and returns a body and an error.

After getting the body, we then convert it from bytes to a string before printing it out.

Add the code below to implement it:

```go
package main

import (
	"fmt"
	"io/ioutil"
	"net/http"
)

func main() {
	resp, err := http.Get("https://api.coinbase.com/v2/prices/spot?currency=USD")
	if err != nil {
		fmt.Printf("Failed with an error %s\n", err)
	} else {
***
		//Reading the response
		data, _ := ioutil.ReadAll(resp.Body)
		//Converting the body to type string
		fmt.Println(string(data))
***        
	}
}

{{copy filename='code.go'}}
```

From the code above, we’ve converted the Body returned by the function to a string using a `string()` function.

Run the application to see the formatted output:

```
go run code.go 
{{execute}}
```

Next, we’ll look at how to handle POST requests.