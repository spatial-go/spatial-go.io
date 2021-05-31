# Space calculation

**Support basic GIS operations of spatial data. You can perform intersections, create buffers, calculate statistics, perform neighborhood analysis, and more.**

## Intersect

If the intersection of two geometric objects does not generate an empty set, return true, otherwise return false

**parameter:**

Input parameters: geom1, geom2 (determine whether the geometric objects intersect)

Output parameters: bool (judgment result), error (corresponding error message)

**Example:**

```go
package main

import (
	"fmt"

	"github.com/spatial-go/geoos"
	"github.com/spatial-go/geoos/planar"
)

func main() {
	G := planar.GEOAlgorithm{}
	polygon := geoos.Polygon{{{116.39439582824706, 39.93284110825641},
		{116.38675689697266, 39.92494288320867}, {116.40563964843749, 39.93020846782819},
		{116.39439582824706, 39.93284110825641}}}
	line0 := geoos.LineString{{116.40495300292967, 39.926785883895654}, {116.3975715637207, 39.9295502919}}
	line1 := geoos.LineString{{116.37310981750488, 39.92099342895789}, {116.39928817749023, 39.9174387253541}}
	b1, _ := G.Intersects(polygon, line0)
	b2, _ := G.Intersects(polygon, line1)
	fmt.Println(b1, b2)
}

//output
//true false
```

## Buffer

Get the geometric object and distance, and then return the geometric object representing the buffer surrounding the original source image.

**parameter:**

Input parameter: geom (geometric object that needs to be buffer)

Output parameters: width (buffer distance), quadsegs (number of sides in 1/4 circle)

**Example:**

```go
package main

import (
	"fmt"

	"github.com/spatial-go/geoos"
	"github.com/spatial-go/geoos/planar"
)

func main() {
	G := planar.GEOAlgorithm{}
	point := geoos.Point{1, 1}
	buffered := G.Buffer(point, 1, 4)
	fmt.Println(buffered)
}

// output
//[[[2 1] [1.923879532511287 0.6173165676349106] [1.7071067811865481 0.292893218813453] [1.382683432365091 0.0761204674887137] [1.0000000000000016 0] [0.6173165676349122 0.0761204674887125] [0.2928932188134541 0.2928932188134508] [0.0761204674887143 0.6173165676349077] [0 0.9999999999999968] [0.0761204674887118 1.3826834323650865] [0.2928932188134495 1.7071067811865446] [0.6173165676349064 1.9238795325112852] [0.9999999999999953 2] [1.3826834323650852 1.9238795325112887] [1.7071067811865435 1.7071067811865515] [1.9238795325112845 1.3826834323650954] [2 1]]]
```

## Length

Used to return the length of a line string or multi-line string.

**parameter:**

Input parameter: geom (geometric object whose length needs to be calculated)

Output parameters: float64 (corresponding length), error (corresponding error message)

**Example:**

```go
package main

import (
	"fmt"

	"github.com/spatial-go/geoos"
	"github.com/spatial-go/geoos/planar"
)

func main() {
	G := planar.GEOAlgorithm{}
	line := geoos.LineString{{0, 0}, {1, 1}}
	length, _ := G.Length(line)
	fmt.Println(length)
}

// output
//1.4142135623730951
```

## Equals

Compare two geometric objects, if the two geometric objects are exactly the same, return true, otherwise return false.

**parameter:**

Input parameters: geom1, geom2 (determine whether to intersect geometric objects)

Output parameters: bool (judgment result), error (corresponding error message)

**Example:**

```go
package main

import (
	"fmt"

	"github.com/spatial-go/geoos"
	"github.com/spatial-go/geoos/planar"
)

func main() {
	G := planar.GEOAlgorithm{}
	polygon0 := geoos.Polygon{{{116.39439582824706, 39.93284110825641},
		{116.38675689697266, 39.92494288320867}, {116.40563964843749, 39.93020846782819},
		{116.39439582824706, 39.93284110825641}}}
	polygon1 := geoos.Polygon{{{116.39439582824706, 39.93284110825641},
		{116.38675689697266, 39.92494288320867}, {116.40563964843749, 39.93020846782819},
		{116.39439582824706, 39.93284110825641}}}
	b, _ := G.Equals(polygon0, polygon1)
	fmt.Println(b)
}

// output
// true
```



## Union

Returns the geometric object formed by combining two source objects.

**parameter:**

Input parameters: geom1, geom2 (two geometric objects that need to be intersected)

Output parameters: geometry (the final geometric object), error (corresponding error message)

**Example:**

```go
package main

import (
	"fmt"

	"github.com/spatial-go/geoos"
	"github.com/spatial-go/geoos/planar"
)

func main() {
	G := planar.GEOAlgorithm{}
	polygon0 := geoos.Polygon{{{116.38564109802246, 39.938829988015556},
		{116.38177871704102, 39.9282339210584}, {116.4052963256836, 39.93382832231185},
		{116.38564109802246, 39.938829988015556}}}
	polygon1 := geoos.Polygon{{{116.38924598693846, 39.94146229682228},
		{116.39036178588867, 39.93514458556912}, {116.40392303466797, 39.93942226632577},
		{116.38924598693846, 39.94146229682228}}}
	b, _ := G.Union(polygon0, polygon1)
	fmt.Println(b)
}

// output
//[[[116.4052963256836 39.93382832231185] [116.38177871704102 39.9282339210584] [116.38564109802246 39.938829988015556] [116.38990240696533 39.93774561274604] [116.38924598693846 39.94146229682228] [116.40392303466797 39.93942226632577] [116.39472064011711 39.93651951697532] [116.4052963256836 39.93382832231185]]]
```