# LEARNING-GOLANG-LOGS
## 10/05/2024
### Variable and declaration
```
var a = 10
var a int
var a,b = 10,"Hello"
a := 10
...
```
## 11/05/2024
### Data type
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

//Kiểu chuỗi: (Nhớ để trong dấu nháy kép "")
var i string = "hello"

//Kiểu byte:
var a byte = 'A'
fmt.Println(a)  //In ra giá trị ASCII của 'A' (65)

// Kiểu rune: (Thao tác với chuỗi chính xác hơn với hỗ trợ những ký tự Unicode)
var a rune = 'あ'
fmt.Printf("%c\n", a) //'あ'
fmt.Println(a) // In ra giá trị Unicode của'あ' (12354)
```
### Functions, multiple/named returns
```
func swap(x, y int) (int, int) {
    return y, x
}
a, b := swap(1, 2)
fmt.Println(a, b) // In ra "2 1"
```
### Arrays, Slices, Maps
```
arr := [3]int{1, 2, 3}
sli := []int{1, 2, 3}
m := map[string]int{
    "one": 1,
    "two": 2,
}
```
### Structs
```
type Person struct {
    Name string
    Age  int
}

// Khởi tạo một đối tượng Person
p := Person{Name: "Alice", Age: 20}

// Truy cập vào các trường của struct
fmt.Println(p.Name) // In ra "Alice"
fmt.Println(p.Age)  // In ra "20"

// Thay đổi giá trị của trường trong struct
p.Age = 21
fmt.Println(p.Age)  // In ra "21"
```
