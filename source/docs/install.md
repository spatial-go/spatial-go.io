## Installation

Install GeoOS
```sh
$ go get github.com/spatial-go/geoos
```

## Documentation
How to use `GeoOS`:
Example: Calculating `area` via `GeoOS`
```
package main

import (
	"bytes"
	"fmt"

	"github.com/spatial-go/geoos/geoencoding"
	"github.com/spatial-go/geoos/planar"
)

func main() {
	// First, choose the default algorithm.
	strategy := planar.NormalStrategy()
	// Secondly, manufacturing test data and convert it to geometry
	const polygon = `POLYGON((-1 -1, 1 -1, 1 1, -1 1, -1 -1))`
	// geometry, _ := wkt.UnmarshalString(polygon)

	buf0 := new(bytes.Buffer)
	buf0.Write([]byte(polygon))
	geometry, _ := geoencoding.Read(buf0, geoencoding.WKT)

	// Last， call the Area () method and get result.
	area, e := strategy.Area(geometry)
	if e != nil {
		fmt.Printf(e.Error())
	}
	fmt.Printf("%f", area)
	// get result 4.0
}
```