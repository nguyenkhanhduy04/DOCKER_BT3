Bài tập 3   : môn Phát triển ứng dụng trên nền web<br>
Giảng viên  : Đỗ Duy Cốp<br>
Lớp học phần: 58KTPM<br>
Ngày giao   : 2025-10-24 13:50<br>
Hạn nộp     : 2025-11-05 00:00<br>
--------------------------------------------------<br>
Yêu cầu     : LẬP TRÌNH ỨNG DỤNG WEB trên nền linux<br>
1. Cài đặt môi trường linux: SV chọn 1 trong các phương án<br>
 - enable wsl: cài đặt docker desktop<br>
 - enable wsl: cài đặt ubuntu<br>
 - sử dụng Hyper-V: cài đặt ubuntu<br>
 - sử dụng VMware : cài đặt ubuntu<br>
 - sử dụng Virtual Box: cài đặt ubuntu<br>
2. Cài đặt Docker (nếu dùng docker desktop trên windows thì nó có ngay)<br>
3. Sử dụng 1 file docker-compose.yml để cài đặt các docker container sau: <br>
   mariadb (3306), phpmyadmin (8080), nodered/node-red (1880), influxdb (8086), grafana/grafana (3000), nginx (80,443)<br>
4. Lập trình web frontend+backend:<br>
 SV chọn 1 trong các web sau:<br>
 4.1 Web thương mại điện tử<br>
 - Tạo web dạng Single Page Application (SPA), chỉ gồm 1 file index.html, toàn bộ giao diện do javascript sinh động.<br>
 - Có tính năng login, lưu phiên đăng nhập vào cookie và session<br>
   Thông tin login lưu trong cơ sở dữ liệu của mariadb, được dev quản trị bằng phpmyadmin, yêu cầu sử dụng mã hoá khi gửi login.<br>
   Chỉ cần login 1 lần, bao giờ logout thì mới phải login lại.<br>
 - Có tính năng liệt kê các sản phẩm bán chạy ra trang chủ<br>
 - Có tính năng liệt kê các nhóm sản phẩm<br>
 - Có tính năng liệt kê sản phẩm theo nhóm<br>
 - Có tính năng tìm kiếm sản phẩm<br>
 - Có tính năng chọn sản phẩm (đưa sản phẩm vào giỏ hàng, thay đổi số lượng sản phẩm trong giỏ, cập nhật tổng tiền)<br>
 - Có tính năng đặt hàng, nhập thông tin giao hàng => được 1 đơn hàng.<br>
 - Có tính năng dành cho admin: Thống kê xem có bao nhiêu đơn hàng, call để xác nhận và cập nhật thông tin đơn hàng. chuyển cho bộ phận <br>đóng gói, gửi bưu điện, cập nhật mã COD, tình trạng giao hàng, huỷ hàng,...<br>
 - Có tính năng dành cho admin: biểu đồ thống kê số lượng mặt hàng bán được trong từng ngày. (sử dụng grafana)<br>
 - backend: sử dụng nodered xử lý request gửi lên từ javascript, phản hồi về json.<br>
 4.2 Web IOT: Giám sát dữ liệu IOT.<br>
 - Tạo web dạng Single Page Application (SPA), chỉ gồm 1 file index.html, toàn bộ giao diện do javascript sinh động.<br>
 - Có tính năng login, lưu phiên đăng nhập vào cookie và session<br>
   Thông tin login lưu trong cơ sở dữ liệu của mariadb, được dev quản trị bằng phpmyadmin, yêu cầu sử dụng mã hoá khi gửi login.<br>
   Chỉ cần login 1 lần, bao giờ logout thì mới phải login lại.<br>
 - hiển thị giá trị mới nhất của các thông số đang giám sát, khi click vào thì hiển thị đồ thị lịch sử quá trình thay đổi (gọi grafana iframe để hiển thị)<br>
 - backend: Sử dụng nodered để đọc dữ liệu từ các cảm biến (có thể dùng api online để lấy dữ liệu theo giời gian thực), <br>
   nodered sẽ lưu dữ liệu mới nhất (dạng update) vào cơ sở dữ liệu mariadb (sử dụng phpmyadmin để tạp table và quản trị lần đầu)<br>
   nodered sẽ lưu dữ liệu (insert) vào influxdb để lưu giá trị lịch sử, để cho grafana dùng để hiển thị biểu đồ.<br>
5. Nginx làm web-server<br>
 - Cấu hình nginx để chạy được website qua url http://fullname.com  (thay fullname bằng chuỗi ko dấu viết liền tên của bạn)<br>
 - Cấu hình nginx để http://fullname.com/nodered truy cập vào nodered qua cổng 80, (dù nodered đang chạy ở port 1880)<br>
 - Cấu hình nginx để http://fullname.com/grafana truy cập vào grafana qua cổng 80, (dù grafana đang chạy ở port 3000)<br>
--------------------------------------------------------------------------------<br>
# Bài Làm:<br>
1. Cài đặt môi trường linux:<br>
- enable wsl:<br>
  <img width="662" height="492" alt="image" src="https://github.com/user-attachments/assets/38c2a272-8315-4bd0-8a6b-edb3e6f32189" /><br>
- Install Ubuntu trên Power Shell:<br>
  <img width="824" height="249" alt="image" src="https://github.com/user-attachments/assets/1966b6c8-44f9-4d8a-b4e9-79bfa2c7522f" /><br>
- Sau khi cài xong sẽ yêu cầu ta thiết lập username và password<br>
- Bật 2 ô:<br>
  <img width="557" height="491" alt="image" src="https://github.com/user-attachments/assets/0dd26ffd-6643-4552-853b-74173a86566a" /><br>
- Sau đó windows sẽ yêu cầu restart lại máy<br>
2. Cài đặt Docker: <br>
- Tải về Docker Destop for Windows AMD64:<br>
  <img width="1392" height="964" alt="image" src="https://github.com/user-attachments/assets/e759145d-35ec-4777-8540-a435dad75f12" /><br>

- Thực hiện cài đặt và kết nối tới docker desktop:<br>
  <img width="1612" height="905" alt="image" src="https://github.com/user-attachments/assets/6075cb9b-0dc3-40b1-aff3-ad54449a1777" /><br>

3. Sử dụng 1 file docker-compose.yml để cài đặt các docker container: <br>
   mariadb (3306), phpmyadmin (8080), nodered/node-red (1880), influxdb (8086), grafana/grafana (3000), nginx (80,443)<br>

   - Tạo 1 dự án chứa file docker-compose.yml và các file cần thiết để cài đặt các docker container<br>
   - Chạy lệnh docker-compose up để tải xuống các container về docker destop:<br>
     <img width="1045" height="499" alt="image" src="https://github.com/user-attachments/assets/d30ebb9c-31d3-45bb-97d4-763dec232665" /><br>
    <img width="1653" height="928" alt="image" src="https://github.com/user-attachments/assets/42fa77bc-8b2e-48f2-95f6-80f8f58ee623" /><br>

   - Thử truy cập từ các cổng localhost:<br>
     + phpmyadmin:<br>
       <img width="1384" height="770" alt="image" src="https://github.com/user-attachments/assets/90f39bb1-8f3f-4ec7-99ab-4cda0ca27de6" /><br>      + nodered:<br>
       <img width="1185" height="692" alt="image" src="https://github.com/user-attachments/assets/ea3dce40-4ca4-476e-a250-a1b19db82a26" /><br>
     + grafana:<br>
       <img width="1303" height="804" alt="image" src="https://github.com/user-attachments/assets/2d0d2fa8-2aa9-4f37-85aa-999d3ea3f616" /><br>
     + infuxdb:<br>
       <img width="1636" height="944" alt="image" src="https://github.com/user-attachments/assets/fdb117b9-b818-4caf-b53b-e3913505be0c" /><br>
    + nginx: dùng localhost/ các service khác để truy cập được các services qua cổng 80:<br>
      <img width="1174" height="613" alt="image" src="https://github.com/user-attachments/assets/4ba645f0-d487-4406-9283-d84d96aea0de" /><br>
      <img width="1227" height="536" alt="image" src="https://github.com/user-attachments/assets/d857ab9c-92b1-438b-ab1c-e8f4e46bcf6a" /><br>

  
4. Lập trình web frontend+backend:<br>
- Dùng nginx làm web server thực hiện tạo ra frontend ( có js gọi tới các api của nodered):<br>
  a. Cấu hình MariaDB (Dùng phpMyAdmin):<br>
  <img width="1314" height="195" alt="image" src="https://github.com/user-attachments/assets/248deffa-1144-4c80-8030-6232a8c0461b" /><br>
  b. Cấu hình nodered tạo api:<br>
    <img width="1186" height="646" alt="image" src="https://github.com/user-attachments/assets/ec1d5cf8-595d-4db3-b546-f4a2980a16ca" /><br>

  c. Viết frontend chỉ gồm 1 file index.html, toàn bộ giao diện do javascript sinh động.<br>
 <img width="1379" height="718" alt="image" src="https://github.com/user-attachments/assets/f96413bc-14b2-4154-b10a-28a3315b9aa2" /><br>
- Kiểm tra xem frontend đã liên kết được với backend chưa:<br>
  <img width="724" height="734" alt="image" src="https://github.com/user-attachments/assets/f62f44bc-8eeb-4bb2-8bbd-79bdc9843c87" /><br>
<img width="627" height="768" alt="image" src="https://github.com/user-attachments/assets/e256df02-e91d-49b0-aebd-c0e392a6e467" /><br>
<img width="874" height="109" alt="image" src="https://github.com/user-attachments/assets/5bd27096-f7b1-4e0c-a1e7-c84c224bdac9" /><br>
- Sau khi đăng nhập đúng tài khoản vừa đăng kí:<br>
  <img width="1796" height="712" alt="image" src="https://github.com/user-attachments/assets/a29c966d-b134-459b-b355-15b6c3e068b8" /><br>

5. Nginx làm web-server:<br>
    - Cấu hình nginx để chạy được website qua url http://fullname.com:<br>
      + C:\Windows\System32\drivers\etc\hosts thêm dòng này ở cuối: 127.0.0.1   nguyenkhanhduy.com<br>
      + Chỉnh sửa file conf:<br>
        <img width="1794" height="947" alt="image" src="https://github.com/user-attachments/assets/dfc7e053-d2cc-4a02-8911-2462b6971676" /><br>

   
   

