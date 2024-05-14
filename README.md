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
Kiểu số nguyên:
```
var a int = 10
var b uint = 20
```
Kiểu số thực:
```
var c float32 = 1.2
var d float64 = 3.4
```
Kiểu số phức:
```
var e complex64 = 1 + 2i
var f complex128 = 3 + 4i
```
Kiểu boolean:
```
var g bool = true
var h bool = false
```
Kiểu chuỗi: (Nhớ để trong dấu nháy kép "")
```
var i string = "hello"
```
Kiểu byte:
```
var a byte = 'A'
fmt.Println(a)  //In ra giá trị ASCII của 'A' (65)
```
Kiểu rune: Kiểu rune trong Go là một ref kiểu int32. Nó được sử dụng để đại diện cho một ký tự Unicode.(Thao tác với chuỗi chính xác hơn với hỗ trợ những ký tự Unicode)
```
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
Errors: error được định nghĩa sẵn, mà bất kỳ kiểu nào triển khai phương thức Error() string đều được coi là một kiểu error
```
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
```
Panic: panic là một hàm tích hợp trong Go, khi được gọi, sẽ dừng thực thi chương trình và in ra một thông điệp lỗi.
```
func main() {
    panic("something bad happened")
}
```
Recover: recover cho phép kiểm soát lại sau khi panic. recover chỉ có thể được gọi trong hàm defer. Nếu không có panic nào xảy ra, recover sẽ trả về nil
```
func main() {
    defer func() {
        if r := recover(); r != nil {
            fmt.Println("Recovered from", r)
        }
    }()
    panic("something bad happened")
}
```
### Starting Todo list project
- Dùng Gin để tạo http server
- Tải image mysql lên docker
- Dùng GROM để kết nối mysql

## 13/05/2024
### Defer
Defer được sử dụng để hoãn việc thực thi một hàm cho đến khi hàm chứa nó kết thúc
```
func printCountdown() {
    for i := 5; i > 0; i-- {
        defer fmt.Println(i)  // Các lệnh defer sẽ được thực thi theo thứ tự ngược lại (1,2,3,4,5)
    }
    fmt.Println("Start!")
}
```
### Silde
Slide nó giống như array nhưng có kích thước linh động hơn
```
func main() {
	primes := [6]int{2, 3, 5, 7, 11, 13}

	var s []int = primes[1:4]
	fmt.Println(s)
}
```
### Tham chiếu và tham trị
- Tham trị (Pass by Value): Khi truyền một biến vào hàm theo kiểu tham trị, mình sẽ truyền giá trị của biến đó. Nếu giá trị được thay đổi bên trong hàm, nó không ảnh hưởng đến biến ban đầu.
- Tham chiếu (Pass by Reference): Khi truyền một biến vào hàm theo kiểu tham chiếu, mình sẽ truyền địa chỉ của biến đó. Do đó, bất cứ thay đổi nào xảy ra với biến bên trong hàm sẽ ảnh hưởng đến biến ban đầu.
```
// Pass By Value
func Add(x int) {
    fmt.Printf("Before Add, Memory Location: %p, Value: %d\n", &x, x)
    x++
    fmt.Printf("After Add, Memory Location: %p, Value: %d\n", &x, x)
}

// Pass By Reference
func AddPtr(x *int) {
    fmt.Printf("Before AddPtr, Memory Location: %p, Value: %d\n", x, *x)
    *x++
    fmt.Printf("After AddPtr, Memory Location: %p, Value: %d\n", x, *x)
}

func main() {
    a, b := 0, 0
    fmt.Printf("Memory Location a: %p, b: %p\n", &a, &b)
    fmt.Printf("Value a: %d, b: %d\n", a, b)

    Add(a)
    AddPtr(&b)

    fmt.Printf("Memory Location a: %p, b: %p\n", &a, &b)
    fmt.Printf("Value a: %d, b: %d\n", a, b)
}
```
### Stack and Heap
- Stack là bộ nhớ lưu các biến cục bộ hoặc là hàm và nó sẽ giải phóng khi hàm đó chạy xong
- Heap để lưu những biến toàn cục có thời gian tồn tại hoặc là độ dài ko xác định và nó sẽ giải phóng bộ nhớ khi mình giải phóng nó hoặc chương trình kết thúc
- Việc giải phóng bộ nhớ cho heap được thực hiện tự động thông qua bộ thu gom rác (Garbage Collection)
### Continute Todolist Project
- Tách các thư mục ra để dể quản lý
- Dùng packet "github.com/joho/godotenv" để load .env
- Hoàn tất CRUD
### Pointer
- Tiết kiệm dữ liệu hơn về việc thao tác trên 1 biến
- Hạn chế con trỏ: khó dùng và phải handle nil
### Concurrency and Parallelism
Concurrency (Đồng thời):

* Liên quan đến việc một ứng dụng xử lý nhiều tác vụ cùng một lúc.
* Concurrency được thực hiện thông qua việc xen kẽ các hoạt động của các tiến trình trên CPU (Central Processing Unit) hoặc nói cách khác là thông qua việc chuyển đổi ngữ cảnh.

Parallelism (Song song):

* Parallelism liên quan đến việc một ứng dụng chia các tác vụ thành các tác vụ con nhỏ hơn được xử lý cùng một lúc hoặc song song.
* Nó được sử dụng để tăng throughput và tốc độ tính toán của hệ thống bằng cách sử dụng nhiều bộ xử lý.

So sánh:

* Concurrency là giải quyết nhiều vấn đề cùng một lúc (không nhất thiết phải là đồng thời), còn Parallelism là giải quyết một vấn đề duy nhất nhanh hơn bằng cách chia nó thành các phần nhỏ hơn và giải quyết chúng đồng thời.
* Concurrency thường chia nhỏ một tác vụ thành nhiều phần nhỏ hơn và xử lý chúng một cách xen kẻ độc lập. Trong khi đó, Parallelism thường liên quan đến việc chia nhỏ một tác vụ thành nhiều phần nhỏ hơn và xử lý chúng cùng một lúc.
* Concurrency có thể được thực hiện trên một bộ xử lý duy nhất hoặc nhiều hơn. Trong khi đó, Parallelism yêu cầu nhiều bộ xử lý để thực hiện các tác vụ cùng một lúc.
### Download go by WSL
- Dowload go mở terminal và nhập lệnh:
```
curl -OL https://golang.org/dl/go1.22.3.linux-amd64.tar.gz
```
- Giải nén file
```
sudo tar -C /usr/local -xzf go1.22.3.linux-amd64.tar.gz
```
- Vào mở file .bashrc và bấm 'i' để edit. Sau đó thêm dòng này ở cuối 
```
export PATH=$PATH:/usr/local/go/bin
```
- Sau đó nhấn Esc để thoát trình edit và nhập `:wq` để đóng file
- Cập nhật lại file .bashrc
```
source .bashrc
```
- Kiểm tra phiên bản
```
go version
```

