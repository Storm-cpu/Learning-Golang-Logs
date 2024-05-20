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

## 14/05/2024
### Goroutine and Channel
Goroutine:
- Goroutine là một luồng nhẹ trong Go, cho phép chúng ta thực hiện các tác vụ song song.
- Mỗi goroutine chạy độc lập và song song với các goroutine khác.
- Từ khóa `go` được sử dụng để khởi tạo một goroutine mới.
```
func say(s string) {
	for i := 0; i < 5; i++ {
		time.Sleep(100 * time.Millisecond)
		fmt.Println(s)
	}
}

func main() {
	go say("world")
	say("hello")
}
```

Channel:
- Channel là một cơ chế cho phép hai hoặc nhiều goroutine trao đổi dữ liệu và đồng bộ hóa việc thực thi chúng.
- Dữ liệu được gửi vào channel bằng toán tử `<-`.
- Dữ liệu được nhận từ channel cũng bằng toán tử `<-`.
- Khi tạo một channel không đệm (unbuffered channel) bằng cách sử dụng `make(chan Type)` nó có nghĩa là mỗi lần gửi (send) trên channel sẽ bị chặn cho đến khi có một lần nhận (receive) tương ứng.
- Tạo một channel với dung lượng (capacity), có thể sử dụng `make(chan Type, capacity)`. Trong trường hợp này, các lần gửi vào channel sẽ không bị chặn cho đến khi channel đầy.
```
func sum(s []int, c chan int) {
	sum := 0
	for _, v := range s {
		sum += v
	}
	c <- sum // send sum to c
}

func main() {
	s := []int{7, 2, 8, -9, 4, 0}

	c := make(chan int)
	go sum(s[:len(s)/2], c)
	go sum(s[len(s)/2:], c)
	x, y := <-c, <-c // receive from c

	fmt.Println(x, y, x+y)
}
```

### Select
- Câu lệnh `select` trong Go cho phép chờ đồng thời nhiều hoạt động trên các channel. Nó giống như một câu lệnh `switch`, nhưng dành cho các hoạt động trên channel.
- `select` sẽ kiểm tra tất cả các `case` của nó để xem có `case` nào sẵn sàng thực thi hay không.
- Nếu có nhiều hơn một `case` sẵn sàng thực thi, `select` sẽ chọn một cách ngẫu nhiên. Nếu chỉ có một `case` sẵn sàng, `select` sẽ chọn `case` đó. Nếu không có `case` nào sẵn sàng và không có `default`, `select` sẽ chặn cho đến khi có `case` sẵn sàng. Nếu có khối default, `select` sẽ thực thi khối `default`.
- `select` sẽ thực hiện hoạt động trên channel tương ứng với `case` đã chọn (nhận hoặc gửi dữ liệu), sau đó thực thi khối mã trong `case` đó.
```
select {
case msg := <-ch1:
    fmt.Println("Received message from ch1:", msg)
case ch2 <- "Hello":
    fmt.Println("Sent message to ch2")
default:
    fmt.Println("No message received or sent")
}
```

### Docker
- Dowload docker trên WSL
- Setup docker vô group có thể sử dụng mà không cần cần sudo
```
sudo usermod -aG docker $USER
exec su -l $USER
```
- Build a Go image
```
#Dockerfile
#Xây dựng dựa trên Docker image golang phiên bản mới nhất.
FROM golang:latest
# Đặt thư mục làm việc trong docker container
WORKDIR /app
# Sao chép các tệp go.mod và go.sum từ host vào /app 
COPY go.mod go.sum ./
# Tải về các module go cần thiết
RUN go mod download
# Sao chép tất cả file go vào /app
COPY *.go ./
# Biên dịch và tạo file thực thi có tên là /docker-gs-ping
RUN CGO_ENABLED=0 GOOS=linux go build -o /docker-gs-ping
# Docker container sẽ lắng nghe trên cổng 8080
EXPOSE 8080
# Đặt lệnh mặc định khi docker được chạy
CMD ["/docker-gs-ping"]
```
- Run a Go image `docker run --publish 8080:8080 docker-gs-ping`

### Mutex and RWMutex
- Mutex: giúp đảm bảo chỉ có một goroutine có thể truy cập vào dữ liệu được chia sẻ tại một thời điểm để tránh race conditions
- RNMutex: nó là biến thể khác của mute. Nhiều goroutine có thể read dữ liệu mà không cần khóa nhau nhưng chỉ có 1 goroutine có thể ghi dữ liệu

### Dowload Portgres in docker
```
docker run --name postgres -p 5432:5432 -e POSTGRES_PASSWORD=mysecretpassword -d postgres
```
## 15/05/2024
### Create three todo porject with mux, gin anh echo
## 16/05/2024
### Gin
- Gin là một framework HTTP router và middleware nó làm đơn giản hóa việc phát triển web với Golang. 
- Hỗ trợ các middleware ghi log, xử lý lỗi, xác thực
- Binding JSON, XML, HTML
- Group các đường dẫn
- Hiệu suất cao do sử dụng thư viện httprouter để xử lý yêu cầu http
- API đơn giản
- Hỗ trợ xây dựng module handle request có thể tái sử dụng
- Gin có bộ tính năng giới hạn so với các framework lớn hơn
- Không hỗ trợ ORM
- Hỗ trợ HTTP/2, TSL

### Echo
- Echo là một framework mạnh mẽ và linh hoạt
- Hỗ trợ các middleware ghi log, xử lý lỗi, xác thực
- Router được tối ưu hóa cao
- Có khả năng mở rộng
- Group các đường dẫn
- Hỗ trợ xây dựng module handle request có thể tái sử dụng
- Binding JSON, XML
- Template engines
- Hỗ trợ HTTP/2, TSL
- Tối ưu hóa framework khiến cho ứng dụng nhẹ hơn
- Hỗ trợ Websocket

### Compare Gin and Echo
Router
 - Cả 2 đếu được tối ưu hóa về hiệu xuất nhưng Gin thì tốt hơn một chút về mặt hiệu xuất, nhưng echo thì cung cấp được sự tùy chỉnh và linh hoạt. 

Xử lý lỗi
 - Trong gin có thẻ tạo một middleware có thể được đặt trước hoặc sau các handler trong chuỗi middleware để xử lý các lỗi và trả về phản hồi HTTP, nó cho phép lỗi nên được xử lý trước hay sau khi các handler khác được thực thi. Nếu một lỗi xảy ra thì có thể gọi ra một hàm AbortWithError để ngăn chặn các middleware tiếp theo thực thi.
 - Trong echo, lỗi từ các handler hoặc middleware và được gom lại HTTPErrorHandler. Có nghĩa là thay vì xử lý lỗi ngay tại nơi nó xảy ra, minhd có thể trả lỗi về và để HTTPErrorHandler quyết định cách xử lý nó. Điều này giúp tập trung việc xử lý lỗi vào một nơi, giúp code dễ đọc và bảo dưỡng hơn.
 - Gin xử lý lỗi ngay tại chỗ nó xảy ra, trong khi Echo trả lỗi về và xử lý tập trung.

Khả năng mở rộng
- Echo được cho là tốt hơn vì nó có khả năng tùy chỉnh, cấu hình và mở rộng cao. Gin không tập trung nhiều vào việc hỗ trợ đa dạng các loại file như Echo. Echo hỗ trợ xử lý đa dạng các file và engine template.

Bảo mật
- Gin và Echo đều được hỗ trợ xử lý lỗi và phục hồi từ Panic để tránh crash ứng dụng, hỗ trợ TSL và HTTP/2

### Microservices
Microservices là một kiến trúc ứng dụng mà ở đó, ứng dụng được chia thành nhiều dịch vụ nhỏ, mỗi dịch vụ hoạt động độc lập và thực hiện một nhiệm vụ cụ thể. Mỗi microservice có thể được phát triển, triển khai và mở rộng độc lập với nhau.

### ORM
ORM, viết tắt của Object-Relational Mapping, là một kỹ thuật lập trình cho phép ánh xạ cơ sở dữ liệu đến các đối tượng thuộc ngôn ngữ lập trình hướng đối tượng.

## 17/05/2024
### Tokens
Các loại token
- Access Tokens
- Refesh Tokens
- CRSF Tokens: là token được sử dụng để ngăn chặn các cuộc tấn công CSRF. Khi một form được tạo, một CSRF token cũng được tạo và lưu trữ trong session. Khi form được gửi, token này cũng được gửi theo và sau đó được kiểm tra với token trong session. Nếu hai token này khớp, thì yêu cầu được coi là hợp lệ.
- Session Tokens
- OAuth Tokens: là token được sử dụng trong quy trình xác thực OAuth. OAuth là một giao thức cho phép người dùng chia sẻ tài nguyên của họ mà không cần chia sẻ mật khẩu. Thay vào đó, họ cung cấp một OAuth Token cho ứng dụng, và ứng dụng này sử dụng token để truy cập vào tài nguyên thay cho người dùng.
- Bearer Tokens
- API Keys
- Sender Constrained Tokens: là một loại token được thiết kế để giảm thiểu rủi ro khi token bị đánh cắp. Chỉ người gửi (sender) được ủy quyền mới có thể sử dụng token này, điều này được xác minh thông qua một cơ chế bảo mật như chứng chỉ TLS hoặc proof-of-possession(POP).
- ID Tokens: là loại token được sử dụng trong OpenID Connect để trả về thông tin về người dùng

Token Formats
- Opaque Tokens
- JSON Web Tokens

### Starting Social Blog project
- Add models
- Sửa lại hàm tạo JWT
- Cấu hình hàm get JWT để tái sử dụng và Authorization
- Tạo chức năng đăng nhập, authen
- Authorization các chức năng quản lý user dành cho admin
- Handle error record not found khi không tìm thấy dữ liệu trong database. Cụ thể trong phần kiểm tra email có tồn tại hay không. Nếu không thì sẽ tạo user mới

## 20/05/2024
### AWS
What is AWS?
- AWS (Amazon Web Service) là một service điện toán đám mây của AWS. Có khả năng mở rộng cao và chi phí thấp.

Benefit
- Tiết kiệm chi phí
- Linh hoạt
- Khả năng bảo mật caocao
- Hiệu suất cao
- Tích hợp nhiều dịch vụ và công nghệ
- Có khả năng mở rộng

Hạ tầng
- Có 25 regions
- Mỗi regions có ít nhất 3 AZs (Availability Zones) riêng.
- Mỗi AZ là một hoặc nhiều trung tâm dữ liệu
- Points of Presence (PoP) nó là một end point của AWS được dùng để lưu trữ nội dung tạm thời và hoạt động như CDN (Content Delivery Network)
- PoP này chủ yếu chứa các dịch vụ như:
 - Amazon CloudFront, CDN (Content Delivery Network).
 - Amazon Route 53, DNS (Domain Name System).
 - AWS Global Accelerator (AGA).

### CDN (Content Delivery Network) 


### DNS (Domain Name System)
