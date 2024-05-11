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

//Kiểu chuỗi: (Nhớ để trong dấu nháy kép "")
var i string = "hello"

//Kiểu mảng:
var j [5]int = [5]int{1, 2, 3, 4, 5}

//Kiểu struct:
type Person struct {
    Name string
    Age  int
}
p := Person{Name: "Alice", Age: 20}

//Kiểu byte:
var a byte = 'A'
fmt.Println(a)  //In ra giá trị ASCII của 'A' (65)

// Kiểu rune: (Thao tác với chuỗi chính xác hơn với hỗ trợ những ký tự Unicode)
var a rune = 'あ'
fmt.Printf("%c\n", a) //'あ'
fmt.Println(a) // In ra giá trị Unicode của'あ' (12354)
```
