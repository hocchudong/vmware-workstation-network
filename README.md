Network in VMware Workstation 
======

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

### 2.1. Sửa dải IP của một vmnet

Có thể thấy các dải IP mà VMware tự sinh ra và gắn cho các card mạng rất khó nhớ. Ta có thể thay đổi dải IP này bằng cách ấn vào vmnet muốn đổi địa chỉ.

Trong dòng Subnet IP chọn dải IP và subnet muốn thay đổi.

Click Apply và OK

### 2.3. Cấu hình DHCP

Các card mạng này có thể cấp DHCP cho các máy ảo sử dụng nó.

để làm việc này ta ấn vào DHCP Settings, sau đó chọn dải IP dùng để cấp DHCP

<img src=http://i.imgur.com/RbgHKPE.png>

## 3. Kinh nghiệm bản thân

### 3.1. Đặt thứ tự và cấu hình trước địa chỉ IP các vmnet trước khi lab

### 3.2. Xây dựng mô hình lab hoàn chỉnh trên giấy rồi mới thực hiện trên VMware

### 3.3. Cách lab kết hợp giữa GNS3 và VMware Workstation

### 3.4. Cách thêm nhiều card mạng cho máy ảo 

## 4. Lời cảm ơn

Cảm ơn các bạn đã đọc hết bài viết này. Tôi hoan nghênh mọi ý kiến đóng, góp xin hãy post lên [blog của tôi] (http://ducnc.blogspot.com/) hoặc có thể commit lên github này.

Liên hệ:
- Skype: khong_giong_ai
- Facebook: https://www.facebook.com/nguyencongduc


