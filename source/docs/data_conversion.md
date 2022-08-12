# Data type conversion

Including the conversion between wkt, geojson and geometry

## Geometry To Wkt

```go
package main

import (
	"bytes"
	"fmt"
	"log"

	"github.com/spatial-go/geoos/geoencoding"
	"github.com/spatial-go/geoos/space"
)

func main() {
	multiPoint := space.MultiPoint{{-1, 0}, {-1, 2}, {-1, 3}, {-1, 4}, {-1, 7}, {0, 1}, {0, 3}}
	buf := new(bytes.Buffer)
	err := geoencoding.Write(buf, multiPoint, geoencoding.WKT)
	if err != nil {
		log.Println(err)
	}
	fmt.Println(buf.String())
}

// MULTIPOINT((-1 0),(-1 2),(-1 3),(-1 4),(-1 7),(0 1),(0 3))
```

## Wkt To Geometry

```go
package main

import (
	"bytes"
	"log"

	"github.com/spatial-go/geoos/geoencoding"
)

func main() {
	var polygonWktStr = "POLYGON ((30 10, 10 20, 20 40, 40 40, 30 10))"
	buf := new(bytes.Buffer)
	buf.Write([]byte(polygonWktStr))
	got, err := geoencoding.Read(buf, geoencoding.WKT)
	if err != nil {
		log.Println(err)
	}
	log.Println(got)
}

// [[[30 10] [10 20] [20 40] [40 40] [30 10]]]
```

## Geometry To Geojson

```go
package main

import (
	"bytes"
	"fmt"
	"log"

	"github.com/spatial-go/geoos/geoencoding"
	"github.com/spatial-go/geoos/space"
)

func main() {
	geom := space.MultiPoint{{-1, 0}, {-1, 2}, {-1, 3}, {-1, 4}, {-1, 7}, {0, 1}, {0, 3}}
	buf := new(bytes.Buffer)
	err := geoencoding.Write(buf, geom.Geom(), geoencoding.GeoJSON)
	if err != nil {
		log.Println(err)
	}
	fmt.Println(buf.String())
}

// {"type":"MultiPoint","coordinates":[[-1,0],[-1,2],[-1,3],[-1,4],[-1,7],[0,1],[0,3]]}
```

## Geojson To Geometry

```go
package main

import (
	"bytes"
	"log"
	"reflect"

	"github.com/spatial-go/geoos/geoencoding"
)

func main() {
	var json = `{"type":"MultiPoint","coordinates":[[-1,0],[-1,2],[-1,3],[-1,4],[-1,7],[0,1],[0,3]]}`
	buf := new(bytes.Buffer)
	buf.Write([]byte(json))
	got, err := geoencoding.Read(buf, geoencoding.GeoJSON)
	if err != nil {
		log.Println(err)
	}
	log.Println(reflect.TypeOf(got))
}

// space.MultiPoint
```
## WkbHex To Geometry

```go
package main

import (
	"bytes"
	"log"

	"github.com/spatial-go/geoos/geoencoding"
)

func main() {
	var wkbHex = `0101000020E610000000000020D8135D400000004072054440`
	buf := new(bytes.Buffer)
	buf.Write([]byte(wkbHex))
	got, err := geoencoding.Read(buf, geoencoding.WKB)
	if err != nil {
		log.Println(err)
	}
	log.Println(got.Geom())
}

//[116.31006622314453 40.04254913330078]
```