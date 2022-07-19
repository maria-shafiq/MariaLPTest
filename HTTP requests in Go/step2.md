---
title: GET requests

---
<!--GET requests-->
In the following example, we are going to request Coinbase API to get the actua price of a currency of Bitcoin in USD.

If we run curl on:

```
curl https://api.coinbase.com/v2/prices/spot?currency=USD
{{ execute }}
```

We should be able to get a JSON that looks like the following one:

```JSON
{
    "data": {
        "base": "BTC",
        "currency": "USD",
        "amount": "57479.22"
    }
}
```

This means that BTC price reflected in USD is "57479.22".

Let's start with code:

```go
package main

import (
	"fmt"
	"net/http"
)

func main() {
	resp, err := http.Get("https://api.coinbase.com/v2/prices/spot?currency=USD")
	if err != nil {
		fmt.Printf("Failed with an error %s\n", err)
	} else {
		fmt.Println(resp)
	}
}

{{copy filename='code.go'}}
```

From the code above, the `GET()` takes one parameter, a URL string, and it returns a response of type pointer to a struct and an error. It will return a response containing the body if the error returned is nil.

Let us now run the application using the command below:

```
go run code.go
{{execute}}
```

You’ll note that the response given contains data that seems meaningless. Let’s handle this incoherent data to get what we are looking for.