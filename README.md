Network in VMware Workstation 
======
- [Mục lục ](#user-content-network-in-vmware-workstation-)
	- [1. Network mặc định khi mới cài đặt VMware](#user-content-1-network-m%E1%BA%B7c-%C4%91%E1%BB%8Bnh-khi-m%E1%BB%9Bi-c%C3%A0i-%C4%91%E1%BA%B7t-vmware)
	- [2. Các thao tác với một card mạng ảo trong VMware Workstation](#user-content-2-c%C3%A1c-thao-t%C3%A1c-v%E1%BB%9Bi-m%E1%BB%99t-card-m%E1%BA%A1ng-%E1%BA%A3o-trong-vmware-workstation)
		- [2.1. Thêm, xóa một vmnet](#user-content-21-th%C3%AAm-x%C3%B3a-m%E1%BB%99t-vmnet)
				- [Thêm một vmnet](#user-content-th%C3%AAm-m%E1%BB%99t-vmnet)
				- [Xóa một vmnet](#user-content-x%C3%B3a-m%E1%BB%99t-vmnet)
		- [2.2. Sửa dải IP của một vmnet](#user-content-22-s%E1%BB%ADa-d%E1%BA%A3i-ip-c%E1%BB%A7a-m%E1%BB%99t-vmnet)
		- [2.3. Cấu hình DHCP](#user-content-23-c%E1%BA%A5u-h%C3%ACnh-dhcp)
		- [2.4. Cách thêm một card mạng vào máy ảo](#user-content-24-c%C3%A1ch-th%C3%AAm-m%E1%BB%99t-card-m%E1%BA%A1ng-v%C3%A0o-m%C3%A1y-%E1%BA%A3o)
	- [3. Kinh nghiệm bản thân](#user-content-3-kinh-nghi%E1%BB%87m-b%E1%BA%A3n-th%C3%A2n)
		- [3.1. Đặt thứ tự và cấu hình trước địa chỉ IP các vmnet trước khi lab](#user-content-31-%C4%90%E1%BA%B7t-th%E1%BB%A9-t%E1%BB%B1-v%C3%A0-c%E1%BA%A5u-h%C3%ACnh-tr%C6%B0%E1%BB%9Bc-%C4%91%E1%BB%8Ba-ch%E1%BB%89-ip-c%C3%A1c-vmnet-tr%C6%B0%E1%BB%9Bc-khi-lab)
		- [3.2. Xây dựng mô hình lab hoàn chỉnh trên giấy rồi mới thực hiện trên VMware](#user-content-32-x%C3%A2y-d%E1%BB%B1ng-m%C3%B4-h%C3%ACnh-lab-ho%C3%A0n-ch%E1%BB%89nh-tr%C3%AAn-gi%E1%BA%A5y-r%E1%BB%93i-m%E1%BB%9Bi-th%E1%BB%B1c-hi%E1%BB%87n-tr%C3%AAn-vmware)
		- [3.3. Cách lab kết hợp giữa GNS3 và VMware Workstation](#user-content-33-c%C3%A1ch-lab-k%E1%BA%BFt-h%E1%BB%A3p-gi%E1%BB%AFa-gns3-v%C3%A0-vmware-workstation)
				- [Lưu ý:](#user-content-l%C6%B0u-%C3%BD)
		- [3.4. Cách thêm nhiều card mạng cho máy ảo](#user-content-34-c%C3%A1ch-th%C3%AAm-nhi%E1%BB%81u-card-m%E1%BA%A1ng-cho-m%C3%A1y-%E1%BA%A3o)
		- [3.5. Cách thay đổi địa chỉ Gateway cho card mạng NAT](#user-content-35-c%C3%A1ch-thay-%C4%91%E1%BB%95i-%C4%91%E1%BB%8Ba-ch%E1%BB%89-gateway-cho-card-m%E1%BA%A1ng-nat)
	- [4. Lời cảm ơn](#user-content-4-l%E1%BB%9Di-c%E1%BA%A3m-%C6%A1n)

VMware Workstation là một phần mềm ảo hóa dùng cho desktop mạnh và rất phổ biến. 

Ta có thể download và cài đặt một cách rất dễ dàng. [Link download] (https://my.vmware.com/web/vmware/info/slug/desktop_end_user_computing/vmware_workstation/10_0?rct=j&q=&esrc=s&source=web&cd=1&sqi=2&ved=0CBsQFjAA&url=http://www.vmware.com/go/downloadworkstation&ei=ZCscVKLEO5S68gXy2oHAAg&usg=AFQjCNEVKbKEcEsfY7NjAaBQZbrtZtXttg&sig2=UxGNBi9DyNElS6RlUrRrTw&bvm=bv.75774317,d.dGc)

Tính năng của nó thì không cần giới thiệu nhiều, chắc hẳn ai trong chúng ta cũng đều biết cách tạo một máy ảo trong VMware. Tuy nhiên trong quá trình lab nhiều bài lab với VMware Workstation đôi khi tôi gặp trường hợp mạng giữa các máy ảo không thông, địa chỉ IP của máy ảo tự nhiên bị thay đổi,..vv.

Trong bài viết này tôi sẽ trình bày cho các bạn một số kinh nghiệm về network trong VMware tôi rút ra được trong thời gian lab với nó. Hi vọng nó sẽ giúp ích cho các bạn.

# Chú ý:
- Phiên bản VMware tôi sử dụng là VMware Workstation 10
- Host cài đặt VMware Workstation: Windows 7 Pro 64bit
- Quy ước: các card mạng ảo trong VMware sẽ được gọi là vmnetx (với x là số thứ tự của card mạng)

## 1. Network mặc định khi mới cài đặt VMware

Khi mới cài đặt VMware Workstation, mặc định phần mềm sẽ cài cho chúng ta 2 card mạng: 

- Một card bridge, card này sử dụng chính card mạng thật của chúng ta để kết nối ra ngoài Internet (card ethernet hoặc wireless). Do đó khi sử dụng card mạng này IP của máy ảo sẽ cùng với dải IP của máy thật.

Ưu điểm: đơn giản, ra được internet và cùng dải máy thật nên cấu hình gì cũng dễ dàng.

Nhược điểm: tôi đã gặp nhiều trường hợp dùng card bridge cấu hình bình thường và đến khi nơi nào không có mạng (lên lớp chẳng hạn) thì hỏi " hôm qua làm bình thường, sao nay lại không kết nối được?"

=> mất mạng là mất hết!!!!

- Một card Nat, card này sẽ Nat địa chỉ IP của máy thật ra một địa chỉ khác cho máy ảo sử dụng. Card này cũng có thể kết nối ra bên ngoài Internet.

Cá nhân tôi ít khi dùng card này.

Để xem các card mạng đã có trong VMware Workstation ta chỉ cần bật VMware lên, chọn Edit => Virtual Network Editor 

<img src=http://i.imgur.com/HQ6C3Np.png>

Ta có thể thấy trong hình card bridge có tên là VMnet0, card Nat có tên là VMnet8

Card bridge không có địa chỉ IP do nó sẽ sử dụng dải IP của máy thật. VMware sẽ tự sinh một dải IP và gán cho VMnet8. Trong trường hợp của tôi là dải 192.168.238.0/24.

## 2. Các thao tác với một card mạng ảo trong VMware Workstation

### 2.1. Thêm, xóa một vmnet

##### Thêm một vmnet

Cũng trong Virtual Network Editor ta chọn như sau:

<img src=http://i.imgur.com/c5H2lOL.png>

- Bước 1: chọn Add Network
- Bước 2: chọn card cần add thêm (ở đây là VMnet1) 
- Bước 3: ấn OK

Lúc này trên cửa sổ Virtual Network Editor sẽ xuất hiện thêm card VMnet1 và được gắn tự động một dải IP, như hình dưới đây:

<img src=http://i.imgur.com/K6DCSG8.png>

Làm tương tự để add thêm các vmnet tiếp theo.

##### Xóa một vmnet

Trong Virtual Network Editor chọn một vmnet và ấn Remove Network (button cạnh Add Network)

### 2.2. Sửa dải IP của một vmnet

Có thể thấy các dải IP mà VMware tự sinh ra và gắn cho các card mạng rất khó nhớ. Ta có thể thay đổi dải IP này bằng cách ấn vào vmnet muốn đổi địa chỉ.

Trong dòng Subnet IP chọn dải IP và subnet muốn thay đổi.

<img src=http://i.imgur.com/8a9PjoC.png>

Click Apply và OK

### 2.3. Cấu hình DHCP

Các card mạng này có thể cấp DHCP cho các máy ảo sử dụng nó.

để làm việc này ta ấn vào DHCP Settings, sau đó chọn dải IP dùng để cấp DHCP

<img src=http://i.imgur.com/RbgHKPE.png>

### 2.4. Cách thêm một card mạng vào máy ảo

Ví dụ ở đây tôi có một máy ảo Ubuntu Server gắn sẵn một card bridge khi tạo máy ảo.

Show IP trên máy ảo:

<img src=http://i.imgur.com/aTMWiUE.png>

Thêm card mạng thứ 2 vào máy ảo bằng cách vào Edit Virtual Machine Settings, chọn Add => Network và làm theo hình dưới:

<img src=http://i.imgur.com/Tx3Cfd2.png>

Xin cấp IP cho card mạng mới trên máy ảo bằng lệnh ***dhclient eth1***

IP của máy ảo sau khi thực hiện xong (đã có thêm card eth1):

<img src=http://i.imgur.com/qfLEEfc.png>

Đối với trường hợp muốn thay đổi từ card bridge (hoặc nat hoặc vmnet) sang card khác thì chỉ cần chọn vào card cần đổi và làm như bước 3 bên trên (không add thêm card mới)

## 3. Kinh nghiệm bản thân

### 3.1. Đặt thứ tự và cấu hình trước địa chỉ IP các vmnet trước khi lab

Trước đây khi làm một bài lab, tôi thường lao thẳng vào cài máy ảo luôn, sau đó mới xem địa chỉ IP cửa mỗi vmnet rồi đặt IP tĩnh hoặc xin cấp IP bằng cho máy ảo.

Nhưng với một bài lab lớn, sử dụng khoảng 3,4 máy ảo (ví dụ như bài lab firewall, định tuyến, cloud coputing,...) thì việc làm như trên là một sai lầm.

Các địa chỉ IP của tôi rối loạn hết lên, topo lằng nhằng, không thể thông nổi mạng chứ đừng nói đến chuyện cấu hình các thứ khác.

Sau một thời gian tôi đã tự quy hoạch lại các vmnet mình sử dụng, như add thêm các vmnet, đặt lại dải IP cho các vmnet cho dễ nhớ (vmnet1 dải 10.10.10.0/24, vmnet2 dải 10.10.20.0/24,...)

Việc làm này chỉ mất công có một lần, từ các lần sau khi tạo máy ảo bằng VMware tôi chỉ cần add các vmnet mong muốn theo đúng topo là xong

Việc cấu hình và sửa lỗi cũng trở nên dễ dàng hơn do tôi đã thuộc luôn các địa chỉ IP

Các bạn có thể tham khảo cấu hình các vmnet của tôi như hình dưới đây:

<img src=http://i.imgur.com/sfJvoFk.png>

Các card vmnet1, vmnet2, vmnet3 là các card tôi thêm vào.

Các card vmnet0, vmnet8 là các card mặc định đã trình bày ở trên.

### 3.2. Xây dựng mô hình lab hoàn chỉnh trên giấy rồi mới thực hiện trên VMware

Như ví dụ tôi đã trình bày ở phần 3.1, việc lập một topo lab là một việc cực quan trọng.

Trong topo cần chỉ rõ card vmnet nào nối với máy ảo nào, các IP của các interface máy ảo.

##### *Chú ý*: các máy ảo sử dụng chung một vmnet thì cần cùng dải IP với vmnet đó. Ví dụ hai máy ảo của tôi là Win XP và CentOS cùng sử dụng vmnet1 thì 2 máy ảo này phải có IP cùng dải 10.10.10.0. Nếu không đúng như thế thì mạng sẽ không thông.

Ví dụ mô hình Lab OpenStack All in one:

<img src=http://i.imgur.com/YcxaRhP.png>

### 3.3. Cách lab kết hợp giữa GNS3 và VMware Workstation

GNS3 thì chắc hẳn ai cũng biết. Một trong những cái hay của GNS3 mà tôi thấy đó là nó có thể kết nối với các card mạng có trong máy (vmnet, ethernet, wireless)

Thông qua các card mạng này ta có thể kết nối trức tiếp các máy ảo trong VMware Workstation hoặc chính máy thật với các thiết bị mạng (Router, SW,...) trong GNS3

Trong mục này tôi sẽ lấy một ví dụ sử dụng GNS3 giả lập một Switch và kết Switch này với một máy ảo XP chạy trên VMware Workstation.

Máy ảo XP sẽ kết nối tới Switch bằng card mạng vmnet1

Trên GNS3 ta kéo vào topo một PC và một Switch

<img src=http://i.imgur.com/v3X5SJA.png>

Click vào biểu tượng kết nối (hình RJ45 bên góc trái) và ấn vào PC. Sau đó chọn đến card VMnet1

<img src=http://i.imgur.com/5gIlKrn.png>

Đầu dây còn lại nối vào cổng bất kỳ trên Switch.

<img src=http://i.imgur.com/YxeqcIN.png>

Trên VMware Workstation chọn máy ảo XP => Edit Virtual Machine Settings và chọn card mạng là vmnet1 như hình sau:

<img src=http://i.imgur.com/gShCPQt.png>

Sau đó bật máy ảo. Lúc này máy ảo XP đã kết nối đến Switch.

##### Lưu ý:

- Nhiều trường hợp cần chạy GNS3 với quyền Admin thì nó mới nhận được các card vmnet
- Đây chỉ là một ví dụ đơn giản, với các bài lab kết hợp phức tạp hơn cần phải xây dựng mô hình trước.

### 3.4. Cách thêm nhiều card mạng cho máy ảo 

Trong nhiều trường hợp một máy ảo cần phải add nhiều card mạng vmnet.

Nếu các card vmnet này được add cùng một lúc khi khởi tạo máy ảo thì sau này khi đặt IP cho các interface của máy ảo có thể xảy ra hiện tượng ** đảo IP hai interface** rất khó chịu và khó khăn trong việc sửa lỗi.

#### *GIẢI PHÁP*: add từng card mạng cho máy ảo, ví dụ add xong card vmnet1 ta phải click "Finish" rồi "OK" để thoát hẳn ra ngoài. Sau đó "Edit Virtual Machine Settings" rồi add thêm card vmnet2 => Finish => OK. Lặp lại như vậy để add các card mạng tiếp theo.

### 3.5. Cách thay đổi địa chỉ Gateway cho card mạng NAT

Giả sử ta cần làm một bài lab mà sử dụng đến card bridge ở các môi trường khác nhau (ở nhà, cơ quan) có các dải IP dùng cho card bridge khác nhau mà máy ảo thì không thể thay đổi địa chỉ IP (ví dụ mạng ở nhà sử dụng dải 192.168.1.0/24, máy ảo có IP 192.168.1.10, lên công ty thì dải mạng là 10.10.10.0/24)

=> làm thế nào để lab được tại cơ quan?

Có hai cách: 

- Dùng card host only thay cho card bridge, cách này cần phải đặt lại địa chỉ IP cho card giống với IP của mạng ở nhà. để đặt lại ip xem mục 2.2

- Dùng card NAT, cách này cũng cần chỉnh dải IP như cách trên.

Lưu ý: 

- Cách thứ 1 không kết nối ra được ngoài Internet

- Cách thứ 2 cần cấu hình lại gateway của máy ảo do mặc định card NAT để gateway là .2, do đó ta cần cấu hình lại gateway cho giống với mạng bridge thật (giả sử gateway là .1). Cách làm như sau:

Vào Virtual Network Editor chọn card NAT và sửa dải IP như mục 2.2

Bỏ chọn connect a host virtual adapter to this network

<img src=http://i.imgur.com/7sPoBlJ.png>

Ấn vào mục NAT Settings đặt lại gateway cho giống với gateway của mạng ở nhà (.1)

<img src=http://i.imgur.com/dTIUQr4.png>

Apply => Ok

## 4. Lời cảm ơn

Cảm ơn các bạn đã đọc hết bài viết này. Tôi hoan nghênh mọi ý kiến đóng, góp xin hãy post lên [blog của tôi] (http://ducnc.blogspot.com/) hoặc có thể commit lên github này.

Liên hệ:
- Skype: khong_giong_ai
- Facebook: https://www.facebook.com/nguyencongduc
