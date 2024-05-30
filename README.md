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

### Regions
- Có 25 regions
- Mỗi regions có ít nhất 3 AZs (Availability Zones) riêng.
- Mỗi AZ là một hoặc nhiều trung tâm dữ liệu. Nên triễn khai tài nguyên lên 2 AZs
- Points of Presence (PoP) nó là một end point của AWS được dùng để lưu trữ nội dung tạm thời và hoạt động như CDN (Content Delivery Network)
- PoP này chủ yếu chứa các dịch vụ như:
	- Amazon CloudFront, CDN (Content Delivery Netork).
	- Amazon Route 53, DNS (Domain Name System).
	- AWS Global Accelerator (AGA).

### Public and Private network
- VPC dùng để tạo các môi trường riêng độc lập dưới dạng network
- VPC có tính năng VPC end poin ví dụ: tạo end poin của DynamoDB hoặc S3 để kết nối vào VPC mà không cần đi ra ngoài internet
- Khai báo một dãy địa chỉ ip base khi tạo VPC. Phía dưới VPC sẽ có các subnet. Mỗi tier sẽ nằm trong một subnet. Mỗi subnet sẽ nằm trong một AZ
- VPC có tính năng Route Table
- Default Route Tables để truy cập local trong VPC
- Để truy cập internet thì phải có internet gateway, gán vào VPC và cấu hình route table 0.0.0.0/0 và đặt target là id của internet gateway
	- Sau đó gán custom route table vào một subnet trong VPC
	- Cấp EC2 instance địa chỉ public ip address
- Khi tạo ra mỗi subnet thì mất 5 địa chỉ IP:
	- *.*.*.0: Network
	- *.*.*.1: Router
	- *.*.*.2: DNS
	- *.*.*.3:
	- *.*.*.255: Broadcast
- Để Private instance truy cập ra ngoài internet
	- Tạo public ip tĩnh
  	- Tạo NAT gateway (ip pub với pri) và gán public ip tĩnh vào 
  	- Add Route entry vào id của NAT gateway (0.0.0.0/0)

### Security Group
- Nó như một tường lửa
- Mặc định nó sẽ chặn các kết nối từ bên ngoài vào và cho phép truy cập từ trong ra ngoài
- Bản chất của nó là bảo vệ card mạng. Có thể tạo ra nhiều SG lên một card mạng
- Scope của nó bao quanh một EC2
- Phải cấu hình inbound rule để có thể remote từ máy bàn đến server
- Statefull firewall
- Allow only
- Tính năng reference other group thay vì gõ ip vào inbound rule thì mình chỉ cần id của security group

### Network Access Control Lists (NACLs)
- Nó là một tính năng tường lửa thứ 2
- Mặc định không cấm gì
- Scope của nó bao quanh một subnet

### VPC Peering
- Peering connection dùng để kết nối 2 VPC
- Muốn kết nối 2 VPC thì cả 2 route table cúa 2 bên phải có ip base của cả 2 VPC và target đặt là id của peering connection
- Peering connection là một cái relationship 1:1
- 2 ip base của VPC phải khác nhau

### AWS Site-to-site VPN
- Dùng để tạo kết nối an toàn giữa trung tâm dữ liệu hoặc văn phòng với các tài nguyên của AWS
- Virtual Private Gateway: Virtual Private Gateway là end point VPN ở phía Amazon của kết nối VPN Site-to-Site của mình.
- Customer Gateway: Một tài nguyên AWS cung cấp thông tin cho AWS về thiết bị cổng mạng của khách hàng.
- IPSec Tunnel là một liên kết mã hóa nơi để truyền dữ liệu giữa client và AWS

### Cost Optimization
- Rightsize your resourse 
- Increase elasticity
- Pick the right pricing model
- Optimize storage
- Meansure, monitor and improve

### Amazon Elastic Block Store (EBS)
- Amazon EBS Volumes: Là các volume lưu trữ gắn vào các EC2 instance và có thể điều chỉnh để phù hợp với nhu cầu.
- Amazon EBS Snapshots: Là các bản sao lưu của Amazon EBS volumes.
- Volume Type Amazon EBS cung cấp nhiều loại volume giúp tối ưu hóa hiệu suất và lưu trữ, volume bao gồm SSD và HDD.
- Sử dụng mã hóa Amazon EBS để mã hóa các volume EBS và các snapshots EBS.
- EBS tách rời với server

### Amazon Elastic Compute Cloud (EC2)
- EC2 Instances là một máy chủ có thể thuê vận hành qua internet
- Có thể tùy chỉnh lưu trữ, CPU, RAM và hệ điều hành khi tạo một instance
- Có nhiều loại instance có các cấu hình CPU, RAM, đồ họa,... khác nhau
- Có 2 loại lưu trữ trong EC2 instance store (tạm thời) và Amazon EBS volumes (lâu dài)
- Hỗ trợ 3 dòng hệ điều hành chính: Linux, Win, Mac

## 21/05/2024
### Amazon S3
- Là một dịch vụ lưu trữ đối tượng
- Có khả năng mở rộng, bảo mật và hiệu suất cao

Options for data transfer
- AWS Direct Connect
- Amazon Kinesis Firehose
- Amazon Kinesis Data Streams
- Amazon Kinesis Video Streams
- Amazon S3 Transfer Acceleration
- AWS Storage Gateway
- AWS Snowball
- AWS Snowball Edge
- AWS Snowmobile
- AWS DataSync
- AWS Transfer for SFTP

Cấu trúc
- Bucket là root level của các thư mục được tạo ra trong S3. Mỗi bucket tương ứng với một đơn vị lưu trữ logical trên S3.
- Các thư mục con nằm trong một bucket gọi là Folder.
- OObjects là các files được upload và lưu trữ dưới dạng các object. Mỗi object bao gồm dữ liệu, khóa và siêu dữ liệu (metadata).
- Keys là unique name được gán cho mỗi object trong bucket.
- Regions là vị trí địa lý của data center nơi mà dữ liệu được lưu trữ

S3 Block Public Access
- Là một tính năng của S3 giúp ngăn chặn các truy cập public đến tài nguyên S3
- Mặc định là S3 sẽ không cho truy cập tài nguyên từ bên ngoài nên cần phải cấu hình lại

S3 Access Points
- Là các Sub của Bucket
- Là một tính năng quản lý quyền truy cập tài nguyên của S3

S3 Storage Classes
- Amazon S3 Standard (S3 Standard): Dành cho dữ liệu được truy cập thường xuyên.
- Amazon S3 Intelligent-Tiering (S3 Intelligent-Tiering): Tự động di chuyển dữ liệu giữa các lớp dựa trên mẫu truy cập.
- Amazon S3 Standard-Infrequent Access (S3 Standard-IA): Dành cho dữ liệu ít truy cập.
- Amazon S3 One Zone-Infrequent Access (S3 One Zone-IA): Dữ liệu ít truy cập và được lưu trữ chỉ trong một Zone.
- Amazon S3 Glacier (S3 Glacier): Dành cho lưu trữ dữ liệu lâu dài, hiếm khi truy cập mà không yêu cầu quyền truy cập tức thì.
- Amazon S3 Glacier Deep Archive (S3 Glacier Deep Archive): Dành cho lưu trữ lâu dài và bảo quản kỹ thuật số với khả năng truy xuất trong vài giờ với chi phí lưu trữ thấp nhất trên đám mây

### AWS Storage Gateway
- Là một dịch vụ kết nối một thiết bị phần mềm tại chỗ với lưu trữ đám mây để cung cấp tích hợp liền mạch và an toàn giữa môi trường IT tại chỗ của mình và cơ sở hạ tầng lưu trữ AWS trong đám mây
- Deloyment Options: VMware, Hyper-V, KVM, Amazon EC2, Hardware appliance,...
- Hỗ trợ bốn loại cổng: Tape, S3 File, FSx File, và Volume
- Các loại công chính:
	- Amazon S3 File Gateway: Cung cấp truy cập dựa trên Server Message Block (SMB) hoặc Network File System (NFS) đến dữ liệu trong Amazon S3.
	- Tape Gateway: Cung cấp các băng từ ảo cho các ứng dụng sao lưu hàng đầu mà có thể lưu trữ trong Amazon S3 hoặc Amazon S3 Glacier.
	- Volume Gateway: Cung cấp các tập lưu trữ block iSCSI cho các ứng dụng tại chỗ của mình mà mình có thể lưu trữ trong Amazon S3 hoặc di chuyển đến Amazon EBS.

File Gateway
- Tạo folder và share cho server của mình ở môi trường của mình (on-premises) thông qua NSF/SMB protocol
- Sau đó các dữ liệu trong folder đó sẽ được sync lên tới endpoint của Storage Gateway của AWS rồi sau đó nó sẽ được chuyển vào S3
- Trong S3 có thể cấu hình lifecycle để chuyển sang class lưu trữ thấp hơn
- Công dụng: Backup dữ liệu lên cloud

Volume Gateway
- Tạo ra một volume ảo và share thông qua iSCSI protocol
- Khi dữ liệu volume đó sẽ được sync lên tới endpoint của Storage Gateway của AWS rồi sau đó nó sẽ được chuyển vào S3
- Sau đó nó có thể được chuyển thành Amazon EBS
- Công dụng: Backup, Disaster Recovery, Migration (Lưu ý nó chỉ là một dịch vụ hỗ trợ DR)

Tape Gateway
- Tạo một Tape Lib ảo và share lên backup server thôg qua iSCSI VTL protocol
- Tape Lib sẽ được sync lên tới endpoint của Storage Gateway của AWS rồi sau đó nó sẽ được vào S3
- Sau đó Tape Lib có thể được eject vào ngược lại Tape Archive  

## 22/05 - 28/05/2024
### Social Blog Project
- Dùng thư viện GORM để thao tác với db
- Dùng thư viện Echo để xây dựng ứng dụng web
- Cơ sở dữ liệu dùng Postgres
- Migration data
- Login, Register, CRUD User và Blog
- Sử dụng JWT
- Config Logger
- Forgot Password bằng cách gữi mail và xác thực bằng token
- Sử dụng dockerfile và docker-compose
- Thực hiện phân quyền theo mô hình RBAC
```
Roles:
- ADMIN
- AUTHOR
- USER
Permissions:
- ADMIN: CRUD (Create, Read, Update, Delete)
- AUTHOR: RUD (Read, Update, Delete)
- USER: CR (Create, Read)
Scopes:
- ADMIN:
  + ALL USERS
  + ALL BLOGS
- AUTHOR:
  + OWNED USER
  + OWNED BLOGS
USER:
  + ALL USERS
  + ALL BLOGS
```

### Docker

Docker Engine
- Là phần core của Docker, dùng để tạo, vận chuyển và chạy Docker Container
- Cung cấp kiến trúc ứng dụng client-server

Docker Images
- Docker Images như là source code cho Docker Containers
- Được sử dụng để xây dựng các Docker Containers
- Có thể tạo ra Docker Images của riêng mình hoặc sử dụng các Docker Images hiện có

Docker Containers
- Docker Containers là các instance của Docker Images.
- Docker Container chứa tất cả các thành phần của phần mềm để chạy một ứng dụng.

## 29/05/2024
### Refesh token
- Máy khách sử dụng tên người dùng và mật khẩu để xác thực.
- Máy chủ tạo token JWT với thời gian hiệu lực ngắn hơn (ví dụ: 10 phút) và Refresh Token với thời gian hiệu lực dài hơn (ví dụ: 7 ngày).
- Khi máy khách truy cập vào giao diện yêu cầu xác thực, nó sẽ mang Token theo.
- Nếu Token chưa hết hạn, máy chủ sẽ trả về dữ liệu mà khách hàng cần sau khi xác thực.
- Nếu xác thực thất bại khi truy cập vào giao diện yêu cầu xác thực bằng Token (ví dụ: trả về lỗi 401), khách hàng sử dụng Refresh Token để áp dụng cho Token mới từ giao diện làm mới.
- Nếu Refresh Token chưa hết hạn, máy chủ sẽ cấp Token mới cho máy khách.
- Máy khách sử dụng Token mới để truy cập vào giao diện yêu cầu xác thực.
- Nếu Refesh token hết hạn thì phải đăng nhập lại để lấy Access tokem và Refesh token mới
