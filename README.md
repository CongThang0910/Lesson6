# STM32F103 – I2C Master giao tiếp DS1307 và UART hiển thị dữ liệu

## 📌 Mô tả
Chương trình sử dụng **STM32F103C8T6** làm **Master I2C** để giao tiếp với **DS1307 RTC** (Real-Time Clock).  
- STM32 ghi giá trị thời gian ban đầu (12:34:50) vào DS1307 qua I2C.  
- Sau đó, đọc lại dữ liệu thời gian (giờ : phút : giây) từ DS1307.  
- Thời gian đọc được sẽ được gửi qua UART và hiển thị trên terminal máy tính.  

---

## 🛠️ Yêu cầu phần cứng
- **Board**: STM32F103C8T6 (Blue Pill).  
- **IC RTC**: DS1307 (giao tiếp I2C).  
- **USB-TTL** để kết nối UART với máy tính.  
- **Kết nối chân**:  
  - I2C (STM32 ↔ DS1307):  
    - PB6 (SCL) → SCL DS1307  
    - PB7 (SDA) → SDA DS1307  
    - 10kΩ pull-up cho SDA, SCL lên VCC 5V hoặc 3.3V  
  - UART (STM32 ↔ PC qua USB-TTL):  
    - PA9 (TX)  → RX USB-TTL  
    - PA10 (RX) → TX USB-TTL  
    - GND       ↔ GND  

---

## ⚙️ Cấu hình

### 1. I2C1 (Master)
- Pin: PB6 (SCL), PB7 (SDA).  
- Mode: I2C Master.  
- Clock: 100kHz (chuẩn).  
- Địa chỉ DS1307: `0x68` (7-bit) → `0xD0` (ghi), `0xD1` (đọc).  
- Kiểu truyền: Start → Address → Data → Stop.  

### 2. DS1307 RTC
- Thanh ghi địa chỉ:  
  - 0x00: giây  
  - 0x01: phút  
  - 0x02: giờ  
- Dữ liệu lưu dưới dạng **BCD (Binary-Coded Decimal)**.  
- Cần chuyển đổi BCD ↔ Decimal khi xử lý.  

### 3. UART1
- Baudrate: 9600.  
- Word length: 8 bit.  
- Stop bit: 1.  
- Parity: None.  
- Mode: TX + RX (chỉ cần TX để gửi dữ liệu về PC).  

---

## 🖥️ Terminal
Mở phần mềm terminal (PuTTY, TeraTerm, RealTerm, …) với cấu hình:  
- Baudrate: 9600  
- Data bits: 8  
- Stop bits: 1  
- Parity: None  

**Kết quả mong đợi**:  
- Sau reset, terminal in ra:  
