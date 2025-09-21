# STM32F103 – I2C Master giao tiếp EEPROM và UART hiển thị dữ liệu

## 📌 Mô tả
Chương trình sử dụng **STM32F103C8T6** làm **Master I2C** để giao tiếp với EEPROM (ví dụ 24C02).  
- Ghi một byte dữ liệu vào EEPROM qua I2C.  
- Đọc lại dữ liệu từ EEPROM.  
- Gửi dữ liệu đọc được lên terminal qua UART để quan sát.  

---

## 🛠️ Yêu cầu phần cứng
- **Board**: STM32F103C8T6 (Blue Pill).  
- **EEPROM**: 24C02 hoặc IC tương tự dùng I2C.  
- **USB-TTL** để kết nối UART với máy tính.  
- **Kết nối chân**:  
  - I2C (STM32 Master ↔ EEPROM):  
    - PB6 (SCL) → SCL EEPROM  
    - PB7 (SDA) → SDA EEPROM  
    - 10kΩ pull-up cho SDA, SCL lên VCC 3.3V  
  - UART (STM32 ↔ PC qua USB-TTL):  
    - PA9 (TX)  → RX USB-TTL  
    - PA10 (RX) → TX USB-TTL  
    - GND       ↔ GND  

---

## ⚙️ Cấu hình

### 1. I2C1 (Master)
- Pin: PB6 (SCL), PB7 (SDA).  
- Mode: I2C Master.  
- Speed: 100kHz (chuẩn).  
- Duty cycle: Standard mode.  
- Pull-up: Bắt buộc (ngoài).  

### 2. EEPROM (ví dụ 24C02)
- Địa chỉ mặc định: `0xA0` (ghi), `0xA1` (đọc).  
- Bộ nhớ: 2Kb, tổ chức 256 × 8-bit.  

### 3. UART1
- Baudrate: 9600.  
- Word length: 8 bit.  
- Stop bit: 1.  
- Parity: None.  
- Mode: TX (chỉ cần gửi dữ liệu lên terminal).  

---

## 🖥️ Terminal
Mở phần mềm terminal (PuTTY, TeraTerm, RealTerm, …) với cấu hình:  
- Baudrate: 9600  
- Data bits: 8  
- Stop bits: 1  
- Parity: None  

**Kết quả mong đợi**:  
- Sau reset, STM32 ghi một giá trị vào EEPROM.  
- Đọc lại giá trị đó.  
- Hiển thị trên terminal, ví dụ:  
