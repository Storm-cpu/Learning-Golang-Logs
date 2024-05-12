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

// Kiểu rune: Kiểu rune trong Go là một ref kiểu int32. Nó được sử dụng để đại diện cho một ký tự Unicode.(Thao tác với chuỗi chính xác hơn với hỗ trợ những ký tự Unicode)
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
## 12/05/2024
### For Loop và Range
```
//Range để lặp qua các phần tử của một slice, map hoặc chuỗi
nums := []int{1, 2, 3, 4, 5}
for i, num := range nums {
    fmt.Printf("Index: %d, Value: %d\n", i, num)
}
```
### If, Switch statements
```
x := 10
if x > 5 {
    fmt.Println("x lớn hơn 5")
} else {
    fmt.Println("x không lớn hơn 5")
}

day := "Friday"
switch day {
case "Monday":
    fmt.Println("Today is Monday")
case "Friday":
    fmt.Println("Today is Friday")
default:
    fmt.Println("Today is another day")
}
```
### Errors, Panic, Recover
```
//Errors: error được định nghĩa sẵn, mà bất kỳ kiểu nào triển khai phương thức Error() string đều được coi là một kiểu error
func divide(x, y int) (int, error) {
    if y == 0 {
        return 0, errors.New("cannot divide by zero")
    }
    return x / y, nil
}

result, err := divide(10, 0)
if err != nil {
    fmt.Println(err)
}

//Panic: panic là một hàm tích hợp trong Go, khi được gọi, sẽ dừng thực thi chương trình và in ra một thông điệp lỗi.
func main() {
    panic("something bad happened")
}


//Recover: recover cho phép kiểm soát lại sau khi panic. recover chỉ có thể được gọi trong hàm defer. Nếu không có panic nào xảy ra, recover sẽ trả về nil
func main() {
    defer func() {
        if r := recover(); r != nil {
            fmt.Println("Recovered from", r)
        }
    }()
    panic("something bad happened")
}

```
