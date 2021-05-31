# Data type conversion

Including the conversion between wkt, geojson and geometry

## Wkt To Geometry

```go
package main

import (
	"fmt"

	"github.com/spatial-go/geoos/encoding/wkt"
)

func main() {
	var polygonWktStr = "POLYGON ((30 10, 10 20, 20 40, 40 40, 30 10))"
	getGeom, err := wkt.UnmarshalString(polygonWktStr)
	if err != nil {
		fmt.Println(err)
	}
	fmt.Println(getGeom)
}

// [[[30 10] [10 20] [20 40] [40 40] [30 10]]]
```

## Geometry To Wkt

```go
package main

import (
	"fmt"

	"github.com/spatial-go/geoos"
	"github.com/spatial-go/geoos/encoding/wkt"
)

func main() {
	multiPoint := geoos.MultiPoint{{-1, 0}, {-1, 2}, {-1, 3}, {-1, 4}, {-1, 7}, {0, 1}, {0, 3}}
	getWkt := wkt.MarshalString(multiPoint)
	fmt.Println(getWkt)
}

// MULTIPOINT((-1 0),(-1 2),(-1 3),(-1 4),(-1 7),(0 1),(0 3))
```

## Wkt To Geojson

```go
package main

import (
	"fmt"

	"github.com/spatial-go/geoos/encoding/wkt"
	"github.com/spatial-go/geoos/geojson"
)

func main() {
	var polygonWktStr = "POLYGON ((30 10, 10 20, 20 40, 40 40, 30 10))"
	geoosGeometry, err := wkt.UnmarshalString(polygonWktStr)
	if err != nil {
		fmt.Println(err)
	}
	point := geojson.NewGeometry(geoosGeometry)
	value := *point
	bytes, err := value.MarshalJSON()
	fmt.Println(string(bytes))
}

// {"type":"Polygon","coordinates":[[[30,10],[10,20],[20,40],[40,40],[30,10]]]}
```

## Geometry To Geojson

```go
package main

import (
	"fmt"

	"github.com/spatial-go/geoos"
	"github.com/spatial-go/geoos/geojson"
)

func main() {
	var geom = geojson.Geometry{
		Type:        "MultiPoint",
		Coordinates: geoos.MultiPoint{{-1, 0}, {-1, 2}, {-1, 3}, {-1, 4}, {-1, 7}, {0, 1}, {0, 3}},
	}
	bytes, err := geom.MarshalJSON()
	if err != nil {
		fmt.Println(err)
	}
	fmt.Println(string(bytes))
}

// {"type":"MultiPoint","coordinates":[[-1,0],[-1,2],[-1,3],[-1,4],[-1,7],[0,1],[0,3]]}
```

## Geojson To Geometry

```go
package main

import (
	"fmt"
	"reflect"

	"github.com/spatial-go/geoos/geojson"
)

func main() {
	var json = `{"type":"MultiPoint","coordinates":[[-1,0],[-1,2],[-1,3],[-1,4],[-1,7],[0,1],[0,3]]}`
	geom, err := geojson.UnmarshalGeometry([]byte(json))
	if err != nil {
		fmt.Println(err)
	}
	geoosGeometry := geom.Geometry()

	fmt.Println(reflect.TypeOf(geoosGeometry))
}

// geoos.MultiPoint

```

