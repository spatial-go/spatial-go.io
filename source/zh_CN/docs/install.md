## 安装使用

此项目需要依赖 [geos](https://github.com/libgeos/geos) (GEOS 是一个 C++库，是​JTS的拓展), 首先你需要安装 `geos` . 然后在安装 `geoos`:

1. Mac OS X(用 brew)
```sh
$ brew install geos
```
2. Ubuntu or Debian
```sh
$ apt-get install libgeos-dev
```
3. 通过源代码安转
```sh
$ wget http://download.osgeo.org/geos/geos-3.9.0.tar.bz2
$ tar xvfj geos-3.9.0.tar.bz2
$ cd geos-3.9.0
$ ./configure
$ make
$ sudo make install
```
4. 安装 geoos
```sh
$ go get github.com/spatial-go/geoos
```

## 快速入门
怎样使用 `Geoos`:
示例: 用`Geoos`计算`area`
```
package main

import (
	"encoding/json"
	"fmt"
	"github.com/spatial-go/geoos"
	"github.com/spatial-go/geoos/encoding/wkt"
	"github.com/spatial-go/geoos/geojson"
	"github.com/spatial-go/geoos/planar"
)

func main() {
	// First, choose the default algorithm.
	strategy := planar.NormalStrategy()
	// Secondly, manufacturing test data and convert it to geometry
	const polygon = `POLYGON((-1 -1, 1 -1, 1 1, -1 1, -1 -1))`
	geometry, _ := wkt.UnmarshalString(polygon)
	// Last， call the Area () method and get result.
	area, e := strategy.Area(geometry)
	if e != nil {
		fmt.Printf(e.Error())
	}
	fmt.Printf("%f", area)
	// get result 4.0

	rawJSON := []byte(`
  { "type": "FeatureCollection",
	"features": [
	  { "type": "Feature",
		"geometry": {"type": "Point", "coordinates": [102.0, 0.5]},
		"properties": {"prop0": "value0"}
	  }
	]
  }`)

	fc := geojson.NewFeatureCollection()
	_ = json.Unmarshal(rawJSON, &fc)
	println("%p", fc)

	// Geometry will be unmarshalled into the correct geo.Geometry type.
	point := fc.Features[0].Geometry.(geoos.Point)
	println("%p", &point)

}

```