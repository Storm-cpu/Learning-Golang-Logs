# LEARNING-GOLANG-LOGS
## 10/05/2024
### Khai báo biến
```
var a = 10
var a int
var a,b = 10,"Hello"
a := 10
...
```
## 11/05/2024
### Kiểu dữ liệu
```
//Kiểu số nguyên:
var a int = 10
var b uint = 20

//Kiểu số thực:
var c float32 = 1.2
var d float64 = 3.4

//Kiểu số phức:
var e complex64 = 1 + 2i
var f complex128 = 3 + 4i

//Kiểu boolean:
var g bool = true
var h bool = false

//Kiểu chuỗi:
var i string = "hello"

//Kiểu mảng:
var j [5]int = [5]int{1, 2, 3, 4, 5}

//Kiểu slice:
k := []int{1, 2, 3, 4, 5}

//Con trỏ:
m := 10
var n *int = &m

//Kiểu struct:
type Person struct {
    Name string
    Age  int
}
p := Person{Name: "Alice", Age: 20}
```
