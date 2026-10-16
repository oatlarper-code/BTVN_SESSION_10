# 5.Yêu cầu đầu ra
1. Phần I. Phân tích
- Input: Đầu vào thu thập dữ liệu (nhiệt độ, độ ẩm,....), gửi dữ liệu lên internet, lưu trữ và xử lý dữ liệu, ứng dụng hiển thị và cảnh báo
- Output: tín hiệu điều khiển phần cứng thực hiện tự động(bơm, quạt, đèn,....), xem lịch sử dữ liệu theo ngày-tuần-tháng, xuất báo cáo khi cần
- Sơ đồ phối hợp phần cứng của hệ thống trang trại: Cảm biến, độ ẩm --> tín hiệu --> vi điều khiển trung tâm (Xử lý và quyết định) + Lệnh điều khiển --> Wifi --> máy chủ 
2. Phần II. Triển khai
## 🌲 Smart-farm IoT: Hệ thống IoT cho trang trại Lan
> Hướng dẫn vận hành hệ thống Smart-farm IoT và kỹ thuật chuyên dụng cho trang trại
![Sơ đồ hướng dẫn sử dụng Smart-farm IoT](https://rikkeiedu-storage.s3.ap-southeast-2.amazonaws.com/uploads/editor-images/1787648283613_687ec2e7-229c-4942-a347-080fae59560a.webp)
## Hướng dẫn cài đặt 
```
- Bước 1. git clone [https://github.com/smart-farm/orchid-iot-system.git](https://github.com/smart-farm/orchid-iot-system.git) (Tải mã nguồn về máy)
- Bước 2. cd orchid-iot-system (Di chuyển thư mục vào thư mục vừa tải về)
- Bước 3. Cài đặt các thư viện phụ thuộc (Arduino/PlatformIO) pio lib install
- Bước 4. Biên dịch và nạp chương trình vào vi điều khiển ESP32 "pio run --target upload"
```
- [x] : Tự động đo đạc và giám sát độ ẩm đất, nhiệt độ không khí 24/7.
- [x] : Kích hoạt hệ thống tưới phun sương tự động khi độ ẩm xuống dưới ngưỡng định hình.
- [x] : Cảnh báo tức thời qua còi và đèn LED khi nhiệt độ vườn vượt ngưỡng chịu đựng của hoa Lan (>35°C).
- [x] : Đồng bộ dữ liệu lên nền tảng Cloud theo thời gian thực giúp người nông dân dễ dàng theo dõi từ xa.
- [x] : Tích hợp trí tuệ nhân tạo dự báo lượng nước tưới dựa trên dữ liệu thời tiết

Tên thiết bị|Cảm biến Model Khoảng đo|Thông số kỹ thuật|Chuẩn giao tiếp
|:-|:-|:-|:-|
Vi điều khiển chính|ESP32 NodeMCU|Tensilica Dual-Core 32-bit, WiFi Bluetooth|Wi-Fi 802.11 b/g/n
Cảm biến nhiệt độ và độ ẩm|DHT22 (AM2302)|-40°C đến +80°C (±0.5°C) / 0-100% RH|Digital (Single-wire)
Cảm biến độ ẩm đất|Capacitive Soil v1.2|Điện dung chống ăn mòn, hoạt động 3.3V/5V|Analog Output

- Chu kỳ hoạt động Fetch-Decode-Execute khi CPU nhận lệnh tưới bằng Lan bằng blockquote
- Fetch(đọc lệnh): CPU truy xuất địa chỉ chứa mã lệnh bật van để tưới và nạp vào thanh ghi lệnh
- Decode(giải mã): Phân tích mã lệnh vừa được xác định tác vụ kích hoạt chân GPIO tín hiệu mở van nước
- Execute(Thực thi): Thuật toán học và mạch điều khiển phát tín hiệu cao tới chân GPIO tương ứng, kích hoạt đóng mạch điện cho van điện tử hoạt động 
> **Mô hình kim tự tháp DIKW trong xử lý dữ liệu nhiệt độ**
- Data(dữ liệu thô): Từ những con số T = 34 độ C, độ ẩm = 55%
- Information: Chuyển đổi từ dữ liệu data thành câu văn cụ thể nhiệt độ ngoài trời là 34 độ C và thời tiết mưa rào độ ẩm = 55%
- Knowledge: Nhiệt độ >32°C kết hợp độ ẩm <60% gây héo lá Lan, cần tưới phun sương làm mát ngay.
- Wisdom: Tự động điều chỉnh quy trình chăm sóc theo mùa (Mùa khô tăng tần suất, mùa mưa ngắt tự động).
3. Phần III: Kiểm thử
- > Kịch bản giả định: RAM của bộ vi điều khiển bị đầy dữ liệu nhật ký (log sensor quá tải do mất kết nối internet dài ngày).
- > **Phương án giải quyết đã cập nhật:** Mục *"Lưu ý vận hành an toàn và xử lý sự cố tràn RAM"* trong file `README.md` ở trên đã cung cấp đầy đủ quy trình 3 bước (Xuất dữ liệu cũ -> Xóa bộ nhớ đệm/Reset phần cứng) giúp người nông dân tại trang trại Lan dễ dàng xử lý mà không làm gián đoạn hệ thống tưới tự động.
