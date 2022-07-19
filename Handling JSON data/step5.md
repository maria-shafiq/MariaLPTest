---
title: Unmarshal unstructured JSON data

---
<!--Unmarshal unstructured JSON data-->

In cases where you do not know the structure of the data beforehand, we cannot use structs. Instead, we use maps.

Assume you want to unmarshal the data below:

```JSON
{
  "cars": {
    "Honda CRV": "30000",
    "Mercedes C200": "41000"
  },
  "motocycles": "none"
}
```

It is not possible to create a struct that captures all the data above. This is because the keys are not well aligned to be represented as a struct.

To handle this case, we’ll create a map of strings to empty interfaces.

Add this code:

```go
package main

import (
	"encoding/json"
	"fmt"
)

type Cars struct {
	Type  string `json:" carType"`
	Price string `json:"How much it costs"`
}

func main() {
	vehicleJson := `{"cars":{"Honda CRV": "30000","Mercedes C200": "41000"},"motocycles": "none"}`
	var stock map[string]interface{}
	json.Unmarshal([]byte(vehicleJson), &stock)
	cars := stock["cars"].(map[string]interface{})

	for key, value := range cars {

		fmt.Println(key, value.(string))
	}
}

{{copy filename='code.go'}}
```

From the code above, each string corresponds to a JSON property, and its mapped `interface{}` type corresponds to the value, which can be of any type. We then use type assertions to convert this interface{} type into its actual type.

These maps can be iterated over, so an unknown number of keys can be handled by a simple for loop.

Run the code above using this command:

```
go run code.go
{{execute}}
```

Next, we’ll look at how to marshall JSON data.