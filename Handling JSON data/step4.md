---
title: Unmarshal nested objects

---
<!--Unmarshal nested objects-->

Assume that we have another property that measures the height and capacity of the tent. Below is an example of the data.

```json
{
	"category": "midsized",
 	"color": "white",
	"space":
        {
            "seat capacity": 40,
            "height": 4
        }
}
```

To handle this we would need to create a second struct `Space` that would handle the extra property object.

Add the code below to implement this:

```go
package main

import (
	"encoding/json"
	"fmt"
)

type Space struct {
	Capacity int
	Height int
}

type Tent struct {
	Category string
	Color string
	Space Space
}

func main() {
	tentJson := `{"category":"midsized","color":"white", "space":{"capacity":40 , "height":4}}`
	var tent Tent	
	json.Unmarshal([]byte(tentJson), &tent)
	fmt.Println(tent)
}
{{copy filename='code.go'}}
```

From the code above, we added a struct Space to handle the extra dimensions describing the tent. We then added that struct to the Tent struct.

Use this command to run the application:

```
go run code.go
{{execute}}
```

Next, we’ll look at how to unmarshal unstructured data.