## K-Means
k-means聚类将多维数据集划分为k个聚类，每个数据点属于均值最近的聚类，作为聚类的原型。

> * 当你有数值的、多维的数据集时
> * 数据没有标签
> * 您确切地知道需要将数据划分到多少聚类中

### Example
```go
import (
	"github.com/geoos/clusters/kmeans"
	"github.com/geoos/clusters"
)

// 设置一个随机的二维数据集(float64类型的值介于0.0和1.0之间)
var d clusters.PointList
for x := 0; x < 1024; x++ {
	d = append(d, clusters.Coordinates{
		rand.Float64(),
		rand.Float64(),
	})
}

// 将数据点划分为16个聚类
km := kmeans.New()
clusters, err := km.Partition(d, 16)

for _, c := range clusters {
	fmt.Printf("Centered at x: %.2f y: %.2f\n", c.Center[0], c.Center[1])
	fmt.Printf("Matching data points: %+v\n\n", c.Observations)
}
```

## DBScan

(Lat, lon) 在Go中使用DBScan算法快速聚类,
给定一组地理点，这个库可以根据指定的参数找到簇。有几个优化应用:

> * 距离计算使用了sine/cosine的“快速”实现，删除了sqrt
> * 为了在eps距离内找到点，我们使用k-d树
> * 在集合中存在相同点的边缘情况处理

### Example
构建Point集合:
```go
points := cluster.PointList{{30.258387, 59.951557}, {30.434124, 60.029499}, ...}
```
设定DBScan参数:

> * eps 聚合半件 (单位 kilometers)
> * minPoints 聚类最小点的数量

eps 和 minPoints 共同定义了聚类的最小密度

Run DBScan:
```go
clusters, noise := cluster.DBScan(points, 0.8, 10) // eps is 800m, 10 points minimum in eps-neighborhood

```
DBScan 方法返回clusters集合 (每个聚类都是元数据点的结合)