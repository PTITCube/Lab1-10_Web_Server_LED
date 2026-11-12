# Lab 1-11: Máy Chủ Web Điều Khiển Thiết Bị (Web Server LED Control)

> **Phân hệ:** OBC (On-Board Computer)  
> **Thư viện yêu cầu:** `PTITCube Library v1.1.0`  
> **Nền tảng:** PlatformIO / ESP32-WROOM-32 (OBC)

---

## 📖 1. Mục Tiêu & Mô Tả Bài Thực Hành

Khởi tạo Web Server HTTP nhúng trên ESP32, cung cấp giao diện Web trực quan để điều khiển bật tắt LED và giám sát trạng thái qua trình duyệt.

---

## 🔌 2. Sơ Đồ Chân Phần Cứng (Hardware Pinout)

| Ngoại vi | Chân ESP32 | Mô tả |
| :--- | :--- | :--- |
| LED Trạng thái | GPIO 2 | Điều khiển qua giao diện Web HTTP |

---

## 🛠️ 3. Cấu Hình Phần Mềm & Thư Viện

- **Thư viện cốt lõi:** Thư mục `lib/PTITCube` tích hợp sẵn bộ thư viện phiên bản mới nhất `v1.1.0` với các phân hệ phân lớp:
  - `CDH`: Quản lý luồng xuất nhập dữ liệu `cdh` (Stream inheritance) và hệ thống tệp FAT32 trên thẻ nhớ MicroSD.
  - `EPS`: Quản lý năng lượng, đọc IC MAX17048 qua I2C.
  - `Sensor`: Đọc cụm cảm biến môi trường BMP280, cảm biến quán tính 6-DoF MPU6500, từ kế QMC5883L và định vị GNSS L76X.
  - `COM`: Quản lý module vô tuyến LoRa Ebyte E32 qua giao tiếp UART2.
- **Kênh giám sát Console:**
  - **Công cụ:** `Serial (UART0 - 115200 baud)`
  - **Tốc độ Baud:** `115200 bps`
  - **Lưu ý:** Sử dụng đối tượng `Serial` tiêu chuẩn của Arduino với thông điệp log ngắn gọn, chuyên nghiệp.

---

## 🚀 4. Hướng Dẫn Biên Dịch & Nạp Firmware

Sử dụng **PlatformIO CLI** hoặc giao diện **VSCode / PlatformIO IDE**:

```bash
# 1. Di chuyển vào thư mục dự án
cd Lab1-11_Web_Server_LED

# 2. Biên dịch mã nguồn
pio run

# 3. Nạp firmware vào vi điều khiển vệ tinh
pio run -t upload

# 4. Mở cửa sổ giám sát Serial Monitor
pio device monitor -b 115200
```

---

## 📝 5. Lưu Ý Kỹ Thuật

- Sử dụng giao thức HTTP GET/POST điều khiển thiết bị không dây.
- Không chèn các lệnh in `println()` trang trí dư thừa làm nghẽn bộ đệm UART khi vệ tinh vận hành ở tần số cao.
- Kiểm tra kết nối cáp USB-UART và nguồn pin trước khi thực hiện nạp code.
