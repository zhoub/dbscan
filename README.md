# DBSCAN in Go

[![Go Report Card](https://goreportcard.com/badge/github.com/kelindar/dbscan)](https://goreportcard.com/report/github.com/kelindar/dbscan)
[![GoDoc](https://godoc.org/github.com/kelindar/dbscan?status.svg)](https://godoc.org/github.com/kelindar/dbscan)

This package implements density-based spatial clustering of applications with noise [DBSCAN](https://en.wikipedia.org/wiki/DBSCAN) in Golang. It is a data clustering algorithm proposed by Martin Ester, Hans-Peter Kriegel, Jörg Sander and Xiaowei Xu in 1996 which clusters densely packed points. This particular implementation is a fork of [sohlich/go-dbscan](https://github.com/sohlich/go-dbscan) with few optimizations and some clean up to make it a bit more idiomatic.


# Usage
In order to use it, a point needs to implement `DistanceTo` and `Name` functions.

```
type Value float64

func (v Value) DistanceTo(other dbscan.Point) float64 {
	return math.Abs(float64(other.(Value)) - v)
}

func (v Value) Name() string {
	return fmt.Sprint(v)
}

```

After this, `dbscan.Cluster` function can be called with a list of points, desired minimum density and epsilon value.

```
clusters := dbscan.Cluster(2,  1.0,
    Value(1),
    Value(0.5),
    Value(0),
    Value(5),
    Value(4.5),
    Value(4),
)
```