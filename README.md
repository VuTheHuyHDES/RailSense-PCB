# RailSense – Autonomous Rail Inspection System (PCB & Firmware)

[![GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-Live%20Demo-brightgreen?style=for-the-badge&logo=github)](https://YOUR_GITHUB_USERNAME.github.io/RailSense-PCB/)
[![Altium 365](https://img.shields.io/badge/Altium%20365-Interactive%203D-blue?style=for-the-badge&logo=altium)](https://365.altium.com/)
[![ESP32](https://img.shields.io/badge/Hardware-ESP32-cyan?style=for-the-badge&logo=espressif)](https://www.espressif.com/)

Dự án nghiên cứu, thiết kế phần cứng và lập trình nhúng cho **Xe tự hành chạy trên đường ray tàu hỏa phục vụ kiểm tra khuyết tật bề mặt bằng phương pháp siêu âm (NDT)**. Hệ thống sử dụng cấu trúc điều khiển phân tán gồm hai mạch ESP32 giao tiếp thời gian thực qua giao thức **ESP-NOW**.

---

## 🚀 Tính năng nổi bật của phần cứng

### 1. Mạch VCU (Vehicle Control Unit - Xe tự hành)
*   **MCU trung tâm**: ESP32-WROOM-32E (Dual-Core 240MHz).
*   **Quản lý nguồn (Power Management)**:
    *   Nguồn cấp chính: Pin Li-ion 24V (6S3P).
    *   Tách biệt hoàn toàn phần nguồn động lực (24V cho động cơ, van bơm) và nguồn điều khiển (5V/3.3V cho MCU và cảm biến) để chống nhiễu chéo (EMI/EMC).
    *   Đường mạch nguồn kích thước lớn (6.5mm, 1oz copper) chịu dòng đỉnh lên tới 11A (tính toán chuẩn IPC-2221).
*   **Mạch điều khiển động cơ (Motor Driver)**:
    *   Giao tiếp I2C điều khiển chip mở rộng PWM PCA9685 (16 kênh).
    *   Cách ly tín hiệu và điều khiển 4 mạch cầu H BTS7960B độc lập (2 động cơ di chuyển hành trình, 2 động cơ vitme nâng hạ đầu dò).
*   **Khối cảm biến & Cơ cấu chấp hành**:
    *   Đọc phản hồi xung từ Encoder 600 PPR tốc độ cao dùng ngắt ngoài.
    *   Giao tiếp I2C LCD, cảm biến nhiệt độ.
    *   Hỗ trợ 4 Limit Switch bảo vệ hành trình vitme nâng hạ.
    *   Khối MOSFET IRF7832 đóng ngắt van bơm gel siêu âm và đèn cảnh báo.

### 2. Mạch RCU (Remote Control Unit - Tay điều khiển)
*   **MCU trung tâm**: ESP32-WROOM-32E.
*   **Giao diện người dùng**:
    *   8 nút nhấn chức năng thiết kế dạng ma trận/nút nhấn riêng biệt có chống dội bằng phần cứng & phần mềm.
    *   2 biến trở analog (ADC) điều chỉnh vô cấp tốc độ đặt (Setpoint) và thời gian quét tự động.
    *   Màn hình LCD 20x4 giao tiếp I2C hiển thị thông số thời gian thực: vận tốc thực, quãng đường, chế độ hoạt động (MANUAL/AUTO), trạng thái kết nối.
*   **Thời gian trễ truyền nhận cực thấp**: `< 5ms` thông qua giao thức ESP-NOW (không phụ thuộc vào router trung gian).

---

## 🖥️ Xem PCB 3D tương tác & Sơ đồ nguyên lý

Bạn có thể xem trực tiếp PCB dạng 3D xoay/lật và Schematic tại trang **GitHub Pages** của dự án hoặc qua link Altium 365 dưới đây:

*   🌐 **Trang Portfolio GitHub Pages**: [https://YOUR_GITHUB_USERNAME.github.io/RailSense-PCB/](https://YOUR_GITHUB_USERNAME.github.io/RailSense-PCB/)
*   🚂 **Mạch VCU (Xe tự hành)**: [Altium 365 Viewer - RailSense VCU](https://365.altium.com/files/D97F3CD4-1BBE-41F5-9CD4-5D6C0D82514E?variant=[No+Variations])
*   🎮 **Mạch RCU (Tay điều khiển)**: [Altium 365 Viewer - RailSense RCU](https://365.altium.com/files/4F8EC39F-F583-4526-B163-FFBB24310D29)

*Lưu ý: Altium 365 cho phép đo đạc kích thước linh kiện, xem từng lớp đồng (layers), xem schematic và bom (BOM) trực tuyến cực kỳ trực quan.*

---

## 📁 Cấu trúc thư mục dự án

```text
RailSense-PCB/
├── docs/
│   └── index.html      # Trang web GitHub Pages (Embed Altium 365 và thông số)
├── .gitignore          # File cấu hình bỏ qua các file tạm của Altium / IDE
└── README.md           # Tài liệu dự án (File này)
```

*(Mã nguồn firmware điều khiển RX/TX được lưu trữ tại repo chính của dự án).*

---

## 🛠️ Hướng dẫn cài đặt và chạy thử local

Nếu bạn muốn chạy thử trang web showcase local trên máy của mình:

1.  Clone thư mục này về máy:
    ```bash
    git clone https://github.com/YOUR_GITHUB_USERNAME/RailSense-PCB.git
    ```
2.  Mở file `docs/index.html` bằng trình duyệt web bất kỳ.

---

## 👨‍💻 Thông tin tác giả
*   **Họ và tên**: Vũ Thế Huy
*   **Chuyên ngành**: Kỹ thuật Điện tử & Tin học Công nghiệp 1, Khóa 62
*   **Đề tài Đồ án**: Nghiên cứu và chế tạo xe tự hành kiểm tra đường ray tàu hỏa
