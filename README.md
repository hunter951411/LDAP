# LDAP
Tìm hiểu và cấu hình LDAP trên Ubuntu 14.04

###Giới thiệu

LDAP hay Lightweight Directory Access Protocol, là một giao thức cho việc quản lý thông tin liên quan từ một địa điểm trung tâm thông qua việc sử dụng một tập tin và thư mục hệ thống cấp bậc. 

Nó hoạt động theo một cách tương tự như một cơ sở dữ liệu quan hệ trong những cách nhất định, và có thể được sử dụng để tổ chức và lưu trữ bất kỳ loại thông tin. LDAP thường được sử dụng để xác thực tập trung. 

Trong hướng dẫn này, tôi sẽ giới thiệu cách cài đặt và cấu hình một máy chủ OpenLDAP trên Ubuntu 14. 04:

###Cài đặt
Các máy chủ OpenLDAP lưu trữ mặc định của Ubuntu theo gói 'slapd', vì vậy chúng ta có thể cài đặt nó một cách dễ dàng với apt-get. Tôi cũng sẽ cài đặt một số tiện ích bổ sung:
```
sudo apt-get update
sudo apt-get install slapd ldap-utils
```
Bạn sẽ được yêu cầu nhập và xác nhận mật khẩu quản trị cho các tài khoản quản trị LDAP.

###Cấu hình lại slapd
Khi cài đặt hoàn tất, chúng tôi thực sự cần phải cấu hình lại gói LDAP. Lệnh sau đây để đưa lên các công cụ cấu hình gói:
```
sudo dpkg-reconfigure slapd
```

Bạn sẽ được hỏi một loạt các câu hỏi về cách bạn muốn cấu hình phần mềm.

Omit OpenLDAP server configuration? No

Bỏ qua cấu hình máy chủ OpenLDAP? Không

DNS domain name?

Tên miền DNS?

Điều này sẽ tạo ra các cấu trúc cơ sở của đường dẫn thư mục của bạn. Đọc tin nhắn để hiểu làm thế nào nó hoạt động. 
Không có quy tắc thiết lập để làm thế nào để cấu hình này. Nếu bạn có một tên miền thực trên máy chủ này, bạn có thể sử dụng đó. Nếu không, sử dụng bất cứ điều gì bạn muốn. 

Trong bài này, chúng tôi sẽ gọi nó là test.com

Organization name?

Một lần nữa, điều này tùy thuộc vào bạn.

Chúng tôi sẽ sử dụng example trong hướng dẫn này

Administrator password?

Mật khẩu người quản trị

Sử dụng mật khẩu bạn đã cấu hình trong khi cài đặt hoặc sử dụng một mật khẩu khác.

Database backend to use? <b>HDB</b>

Cơ sở dữ liệu phụ trợ để sử dụng? <b>HDB</b>

Remove the database when slapd is purged? <b>NO</b>

Xóa cơ sở dữ liệu khi slapd bị xóa? <b>NO</b>

Move old databases? <b>YES</b>

Di chuyển dữ liệu cũ? <b>Có</b>

Allow LDAPv2 protocol?<b>NO</b>

Cho phép giao thức LDAPv2? <b>Không</b>

###Cài đặt PHPldapadmin

Chúng tôi sẽ quản trị LDAP thông qua một giao diện web được gọi là PHPldapadmin. Điều này cũng có sẵn trong kho mặc định của Ubuntu. 

Cài đặt nó bằng lệnh này: 
```
sudo apt-get install phpldapadmin 
```
Điều đó sẽ cài đặt tất cả các máy chủ web và PHP phụ thuộc yêu cầu.

###Cấu hình PHPldapadmin
Chúng ta cần phải cấu hình một số gtrị trong tập tin giao diện web trước khi chạy nó.
Mở tập tin cấu hình với quyền root:
```
sudo nano /etc/phpldapadmin/config.php

```
Tìm kiếm cho các phần sau đây và thay đổi chúng cho phù hợp.
Thay đổi các giá trị sau:
```
$servers->setValue('server','host','test.com');
```
