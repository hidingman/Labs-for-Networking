# Lab Tổng Hợp

### Mô tả:
Hệ thống mạng được xây dựng như sơ đồ.

![lab](https://github.com/nhuhp/Labs-for-Networking/blob/master/Lab_Tong_Hop_1/img/lab.png)

- ISP rót về một IP tĩnh `100.0.0.6/32`

### Yêu cầu:
#### 1.	Cấu hình đặt địa chỉ IP cho các cổng của các Router theo quy hoạch IP trên sơ đồ.
#### 2.	Thiết lập IP tĩnh cho các thiết bị Host 1, Host2, Host3.
#### 3.	Xây dựng mạng chuyển mạch lớp 2:

##### a. Cấu hình để tất cả các đường link đấu nối giữa các Switch trở thành các đường trunking Dot1q.
##### b. Xây dựng cấu hình VLAN theo mô tả sau:
* Khai báo các VLAN 10, 20 và 30 trên SW1.
* Các VLAN trên SW1 phải được tự đồng bộ đến SW2 và SW3.
* Các thao tác can thiệp vào cấu hình VLAN trên SW2 và SW3 bị cấm.
#### 4.	Hiệu chỉnh đường đi Layer 2:
##### a. Cấu hình hiệu chỉnh STP đảm bảo trên VLAN 10 cổng E0/2 của SW1 bị khóa.
##### b. Cấu hình hiệu chỉnh STP đảm bảo trên VLAN 20 cổng E0/1 của SW1 bị khóa.
#### 5. Định tuyến VLAN:
Trên R1 thực hiện cấu hình định tuyến giữa các VLAN 10, 20 và 30 với các thông số như sau:

| Cổng | Kết nối đến | Địa chỉ IP |
|---|---|---|
| e0/0.10 | VLAN 10 | 172.16.10.1/24 |
| e0/0.20 | VLAN 20 | 172.16.20.1/24 |
| e0/0.30 | VLAN 30 | 172.16.30.1/24 |

#### 6. Cấu hình định tuyến:
Cấu hình định tuyến OSPF trên các Router R1, R2 và R3 đảm bảo tất cả các subnet thuộc dải IP 172.16.0.0/16 có thể đi đến được với nhau.
**Lưu ý:** R3 không được cho cổng nối đến ISP tham gia OSPF.
#### 7. Hiệu chỉnh định tuyến:
##### a. Cấu hình hiệu chỉnh đảm bảo router-id của các router đạt giá trị như sau:
R1: 1.1.1.1 ; R2: 2.2.2.2 ; R3: 3.3.3.3
##### b. Hiệu chỉnh OSPF đảm bảo R1 và R3 đi đến các loopback 0 của nhau thông qua đường trung chuyển qua R2, đường link đấu nối trực tiếp chỉ để dự phòng.
##### c. HIệu chuyển OSPF đảm bảo trên R1 các đường đấu nối với VLAN 10, 20 và 30 tham gia vào OSPF nhưng không nhận các gói tin hello OSPF
#### 8. Cấu hình DHCP:
Cấu hình DHCP trên R2 cấp IP tự động cho VLAN 30.
#### 9. ACL:
##### a. Sử dụng Standard ACL trên R2 cấm IP VLAN10 telnet đến R2 nhưng cho phép các VLAN khác.
##### b. Sử dụng Extended ACL trên R2 chỉ cho phép các user thuộc VLAN20 được truy cập web đến server 172.16.22.2, ngoài ra các lưu lượng khác bị cấm.
##### c. Tiếp tục bổ sung Extended ACL đã cấu hình cho phép server 172.16.22.2 có thể traceroute ra bên ngoài nhưng bên ngoài không thể traceroute đến server này.
#### 10. Internet:
##### a. Cho phép mọi IP VLAN 10, VLAN 20 và VLAN 30 đi internet bằng IP đấu nối 100.0.0.6 trên cổng e0/2 của R3
##### b.	Host 1 hiện đang sử dụng địa chỉ IP private 172.16.10.2. Thực hiện public host này lên Internet bằng địa chỉ 100.0.0.6 được cấp phát bởi ISP.
##### c. Thực cấu hình cho phép mọi user VLAN 2o có thể đi được Internet bằng đầu nối 200.0.0.6 trên cổng E0/2 của R3.
**Lưu ý:** Chỉ được phép cấu hình một và chỉ một static default  - route trên R3 cho hoạt động đi Internet. 
#### 11. Yêu cầu khác:
##### a. Trên các router, thực hiện cấu hình thích hợp để xây dựng sơ đồ như hình dưới:

![de_morong1](https://github.com/nhuhp/Labs-for-Networking/blob/master/Lab_Tong_Hop_1/img/de_morong.png)

b.	Cấu hình định tuyến RIP version 2 trên sơ đồ hình 2 đảm bảo kết quả show trên R1 như sau:

```
R1#show ip route rip
[..]

	10.0.0.0/8 is variably subnetted, 6 subnets, 3 masks
R		10.0.0.0/8		[120/1]		via 192.168.13.3, 00:00:07, Ethernet0/2.13
R		10.1.2.0/24		[120/1]		via 192.168.12.2, 00:00:11, Ethernet0/1.12
R		10.1.3.0/24		[120/1]		via 192.168.12.2, 00:00:11, Ethernet0/1.12
R		10.1.23.0/24		[120/1]		via 192.168.12.2, 00:00:11, Ethernet0/1.12
```

c.	Thực hiện thiết lập sơ đồ Ipv6 giữa R1 và R3 như hình sau. Sử dụng một hình thức định tuyến IPv6 bất kỳ đảm bảo mọi địa chỉ IPv6 trên sơ đồ thấy nhau.

![de_morong2](https://github.com/nhuhp/Labs-for-Networking/blob/master/Lab_Tong_Hop_1/img/de_morong2.png)

