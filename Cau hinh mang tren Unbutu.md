
**Ubuntu cũng như các hệ điều hành linux khác coi card mạng là một devicce và lưu cấu hình trong file text, sau đó tải lên mỗi khi khởi động máy.**

###Thông tin cơ bản

Mỗi máy tính cần có một card mạng Ethernet có dây hoặc không dây, được liệt kê trong thư mục /dev với tên gọi bắt đầu bằng 3 chữ cái eth. Ví dụ

* eth0 cho card mạng thứ nhất
* eth1 cho card mạng thứ 2, ....

Để xem máy có bao nhiêu card mạng, gõ lệnh sau:
                **# ifconfig -a | grep eth**
                
Để kiểm tra xem các card mạng đã được cấu hình hay chưa gõ các lệnh sau
               **# ifconfig**  
               
Lệnh này cung cấp thông tin về địa chỉ MAC, địa chỉ IP, gateway... của tất cả các card mạng. Nếu muốn xem thông tin từng card mạng gõ lệnh này cộng với tên card mạng được list ở bước trên 
ví dụ **# ifconfìg eth0**

Để xem các định tuyến đi qua các mạng như thế nào gõ lệnh sau:
               **# route -n**

###Gán địa chỉ IP tức thời cho card mạng
Để gán ip, cấu hình cho card mạng và kiểm tra chúng ta dùng lệnh sau. Lệnh này sẽ có tác dụng ngay tức thì tuy nhiên cấu hình này không ghi vào file config nên sẽ mất khi khởi động lại máy tính

**# ifconfig ethX IP-address netmask subnet-mask**

Ví dụ
>**# ifconfig eth0 192.168.1.2 netmask 255.255.255.0**

###Gán địa chỉ IP cố định cho card mạng và lưu cấu hình trong file
Muốn card mạng được khai báo IP cố định, chúng ta đặt các lệnh cấu hình card mạng trong file cấu hình có đường dẫn là /etc/network/interface. Có thể dùng lệnh vi hoặc gedit để tạo file cấu hình card mạng này và chỉnh sửa nó

**#sudo gedit /etc/network/interfaces**

Nội dung file như sau:

* auto lo
* iface lo inet loopback
* auto eth0
* iface eth0 inet static
* address 192.168.1.2
* netmask 255.255.255.1.0
* gateway 192.168.1.1
Sau khi khai báo cấu hình trong file interfaces nói trên, cần khởi động lại máy hoặc dùng lệnh sau để khởi động lại dịch vụ mạng để lấy cấu hình mới. Lưu ý 2 dòng đầu tiên là dành cho card loopback, không nên thay đổi.

**# sudo reboot
**# sudo /etc/init.d/networking restart**

###Cấu hình card mạng nhận IP động từ DHCP server
Nếu muốn cấu hình card mạng nhận IP từ DHCP server chúng ta khai báo các dòng lệnh sau trong file /etc/network/interfaces thay cho 5 dòng lệnh cấu hình card mạng ở bước trên

*auto eth0
*iface eth0 inet dhcp

Sau đó reboot hoặc restart dịch vụ mạng như ở bước trên

###Đặt địa chỉ DNS server
Sau khi có địa chỉ mạng, nếu muốn hệ thống có thể truy cập internet, vào các website và chạy các lệnh get app, chúng ta cần chỉ ra một DNS server để hệ thống biết cách phân giải tên miền. Khai báo DNS trong file /etc/resolv với lệnh gedit như sau

**#sudo gedit /etc/resolv**

Và sửa nội dung file này như sau:

**nameserver 8.8.8.8**
**nameserver 8.8.8.4**

Trong đó 8.8.8.8 là DNS chính của google, còn 8.8.8.4 là DNS phụ của google. Bạn có thể thay thế hai địa chỉ DNS này bằng địa chỉ DNS riêng của bạn hoặc của nhà cung cấp dịch vụ nào gần nhất.

###Các lệnh khác với routing và card mạng
Để đặt một card mạng nào đó làm default gateway chúng ta gõ dòng lệnh sau

**# route add default gw ip-getway**  hoặc
**# route add -net 0.0.0.0 mask 0.0.0.0 dev {interface-name}**

Ví dụ  
>**# route add default gw 192.168.1.1**
>**# route add -net 0.0.0.0 mask 0.0.0.0 dev eth0**

Để add một routing tĩnh đến một mạng nào đó ta dùng lệnh

**# route add -net x.x.x.x mask y.y.y.y  dev {interface-name}**

Trong đó x.x.x.x là địa chỉ mạng, còn y.y.y.y là subnet-mask. Ví dụ:

**# route add -net 192.168.5.0 mask 255.255.255.0 dev eth0**

Để gỡ bỏ một route tĩnh hay một default gateway chúng ta thay lệnh route add ở trên bằng lệnh route delete như ví dụ sau

**# route delete -net 192.168.5.0 mask 255.255.255.0 dev eth0**
**# route delete default gw 192.168.1.1**

Để tạm ngừng (disable) một card mạng chúng ta dùng lệnh

**# sudo ifconfig eth0 down**

Để bật lại một card mạng ta dùng lệnh

**# sudo ifconfig eth0 up**

Lưu ý. Tất cả các lệnh trên đều phải dùng với ****sudo** ở đằng trước để đảm bảo có quyền cao nhất
