### 1. 说一说你对泛型的理解和看法
1. 一些函数的作用相同，处理逻辑也相同，只是入参或者返回值类型不同可以考虑使用泛型
2. 对于 slice、map、channel 等类型，如果它们的元素类型是不确定的，操作这类类型的函数可以考虑用泛型

泛型会使代码可能性变差，增加了维护成本，谨慎使用。

### 2. 适合泛型的demo
```go
package main

 
import "fmt"
 
type Number interface {
    int64 | float64
}

func sum[T constraints.Ordered](x, y T) T {
	return x + y
}

func sumInt(x, y int64) int64 {
	return x + y
}

func sumFloat(x, y float64) float64 {
	return x + y
}

func SumIntsOrFloats[K comparable, V int64 | float64](m map[K]V) V {
    var s V
    for _, v := range m {
        s += v
    }
    return s
}

func main() {
    x1 := 1
	y1 := 2
	x2 := 1.1
	y2 := 2.1

	fmt.Println(sumInt(x1, y1))
	fmt.Println(sumFloat(x2, y2))
	fmt.Println(sum[int](x1, y1))
	fmt.Println(sum[float64](x2, y2))


	ints := map[string]int64{
        "first":  34,
        "second": 12,
    }
    floats := map[string]float64{
        "first":  35.98,
        "second": 26.99,
    }
	fmt.Printf("Generic Sums: %v and %v\n",
    SumIntsOrFloats[string, int64](ints),
    SumIntsOrFloats[string, float64](floats))
}
```
