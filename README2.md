# 5. Yêu cầu đầu ra
1. Báo cáo phân tích
- Input: Tổng quan cảm biến độ ẩm của trang trại lan, các bước cài đặt (dòng lệnh terminal), sơ đồ kết nối, vị trí lắp đặt, kết quả là dữ liệu thô đầu vào văn bản 
- Output: Render thành một file Markdown đầy đủ kèm khối code terminal, bảng so sánh và task list kiểm tra thiết bị 
2. Source code
```import time
import RPi.GPIO as GPIO

# Cấu hình chân GPIO
PUMP_PIN = 18  # Chân GPIO kết nối với Relay điều khiển máy bơm

# Thiết lập chế độ chân GPIO
GPIO.setmode(GPIO.BCM)
GPIO.setup(PUMP_PIN, GPIO.OUT)


def control_pump(status):
    """Hàm bật hoặc tắt máy bơm.

    status: True (Bật) hoặc False (Tắt)
    """
    if status:
        GPIO.output(PUMP_PIN, GPIO.HIGH)
        print("[THÔNG BÁO] Máy bơm đã BẬT.")
    else:
        GPIO.output(PUMP_PIN, GPIO.LOW)
        print("[THÔNG BÁO] Máy bơm đã TẮT.")


try:
    print("🚀 Bắt đầu chương trình điều khiển máy bơm...")

    # Vòng lặp thử nghiệm: Bật 5 giây, tắt 5 giây
    while True:
        control_pump(True)  # Bật máy bơm
        time.sleep(5)  # Chờ 5 giây

        control_pump(False)  # Tắt máy bơm
        time.sleep(5)  # Chờ 5 giây

except KeyboardInterrupt:
    print(" Đang dừng chương trình...")

finally:
    GPIO.cleanup()  # Giải phóng các chân GPIO để đảm bảo an toàn
    print("Đã dọn dẹp cấu hình GPIO. Hệ thống an toàn.")
```
- Bảng so sánh

||DHT22 (old)|DHT22 (new)
|-|-|-|
Độ chính xác độ ẩm|Thấp (Sai số ±5%)|Cao (Sai số ±2%)
Độ chính xác nhiệt độ|Thấp (Sai số ±2°C)|Cao (Sai số ±0.5°C)
Dải đo độ ẩm|20% - 80%|0% - 100%
Dải đo nhiệt độ|0°C đến 50°C|-40°C đến 80°C

- Task list

- [x] : Cảm biến độ ẩm (DHT22/AM2302)
- [x] : Raspberry Pi/Jetson/SoC
- [x] : Dây nối Dupont
- [x] : Tua vít, băng keo, ốc vít
- [x] : Thẻ nhớ đã cài hệ điều hành
