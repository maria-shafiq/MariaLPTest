---
title: Unmarshal JSON arrays

---
<!--Unmarshal JSON arrays-->

Assume you have a JSON array that looks like this:

```JSON
[
  {
    "category": "midsized",
    "color": "white"
  },
  {
    "category":"small",
    "color":"yellow"
  }
]
```

From the JSON data above, we can tell that the elements of the array have the same structure.

We can therefore create a struct and unmarshal the data into a slice.

Add the code below to implement that:

```go
package main

import (
	"encoding/json"
	"fmt"
)

type Tent struct {
	Category string
	Color    string
}

func main() {
	tentJson := `[
		{
			"category":"midsized",
			"color":"white"
		},
		{
			"category":"small",
			"color":"yellow"
		}
		]`
	var tent []Tent
	json.Unmarshal([]byte(tentJson), &tent)
	fmt.Printf("Tents : %+v", tent)
}

{{copy filename='code.go'}}
```

Here we created a slice variable variable `tent` to store all the elements in from the JSON data.

Run the application using the command below:

```
go run code.go
{{execute}}
```

Next, we’ll look at how to unmarshal nested objects.