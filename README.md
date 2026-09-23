# 🚀 QvAuto - iOS Touch Automation & Multi-Account Profile Suite

<p align="center">
  <img src="CydiaIcon.png" width="120" height="120" style="border-radius: 26px; box-shadow: 0 8px 24px rgba(0,122,255,0.35);" alt="QvAuto Logo">
</p>

<p align="center">
  <b>Hệ thống Tự Động Hoá Cảm Ứng & Quản Lý Đa Tài Khoản Chuyên Nghiệp Dành Cho iPhone Jailbreak</b>
</p>

<p align="center">
  <a href="https://t.me/viethappy_0205"><img src="https://img.shields.io/badge/Telegram-@viethappy__0205-2CA5E0?style=for-the-badge&logo=telegram&logoColor=white" alt="Telegram Contact"></a>
  <img src="https://img.shields.io/badge/iOS-14.0%20--%2016.6.1-007AFF?style=for-the-badge&logo=apple&logoColor=white" alt="iOS Support">
  <img src="https://img.shields.io/badge/Jailbreak-Dopamine%20%7C%20Rootless%20%7C%20Rootful-success?style=for-the-badge" alt="Jailbreak Support">
</p>

---

## 🌟 Giới Thiệu Tổng Quan (Overview)

**QvAuto** là bộ công cụ tự động hoá toàn diện hoạt động theo mô hình **Hybrid 2-trong-1**:
1. **Chế độ độc lập (Standalone Mode):** iPhone tự chạy kịch bản kịch bản tự động hoá trực tiếp trên thiết bị, kích hoạt bằng Menu nổi (HUD) hoặc phím cứng (Volume Down).
2. **Chế độ điều khiển từ xa (Remote Control Mode):** Máy tính (Windows / macOS / Linux) gửi lệnh điều khiển mượt mà qua Wi-Fi (LAN) hoặc Cáp USB (`iproxy`) thông qua hệ thống **REST API cổng 8080**.

---

## 🔥 Các Tính Năng Nổi Bật (Key Features)

### 👥 1. Quản Lý Đa Tài Khoản (Native Profile Manager - Thay thế Tweak Crane $4.99)
* **Không giới hạn số lượng Profile & Ứng dụng:** Nuôi hàng trăm nick TikTok, Facebook, Shopee, Telegram, Zalo... trên cùng một chiếc iPhone.
* **Cô lập dữ liệu triệt để:** Hoán đổi Sandbox Container (`Documents`, `Preferences`, `Cookies`, `Keychain SQLite`, `AppGroups`) độc lập giữa các nick mà **không bao giờ bị mất đăng nhập**.
* **Anti-Detection (Chống phát hiện thiết bị):**
  - Tự động cấp `identifierForVendor` (IDFV) và `advertisingIdentifier` (IDFA) ngẫu nhiên cho từng profile.
  - Gán Proxy riêng biệt (HTTP / SOCKS5) cho từng tài khoản.
  - Tự động bật/tắt chế độ máy bay (Airplane Mode) để xoay IP 4G trước khi mở app.
  - Fake quốc gia, Múi giờ (GMT), Locale và Toạ độ GPS jitter quanh thành phố mục tiêu.
* **Deep Clean (Xoá sâu dấu vết):** Đưa app về trạng thái như vừa đập hộp máy mới xuất xưởng (chuẩn Factory Reset cho riêng app).
* **Dọn rác giữ đăng nhập (`clearDataKeepLogin`):** Giải phóng hàng GB bộ nhớ cache rác nhưng bảo toàn 100% tài khoản.

---

### ⚡ 2. Tầng Lõi Cảm Ứng & Trí Tuệ Nhân Tạo (Core Automation)
* **Mô phỏng cảm ứng mượt mà (Touch Injection):** Can thiệp trực tiếp tầng `IOHIDEvent` qua tiến trình `backboardd`, vuốt chạm tự nhiên không giật lag.
* **Nhận diện chữ siêu tốc (Vision AI OCR):** Tận dụng nhân **Apple Neural Engine (NPU)** trên chip Apple A-series, quét chữ màn hình chỉ mất **15 - 30ms**.
* **Chụp màn hình thời gian thực (Screen Capture):** Xuất ảnh trực tiếp từ `IOSurface` chuẩn 60 FPS không làm nóng máy.

---

## 📲 Hướng Dẫn Cài Đặt Qua Sileo / Zebra / Cydia

### Cách 1: Thêm nguồn trực tiếp (Khuyên dùng)
1. Mở ứng dụng **Sileo** (hoặc **Zebra / Cydia**).
2. Chuyển sang tab **Sources (Nguồn)** $\rightarrow$ Bấm nút **"+"**.
3. Dán địa chỉ Repo sau:
   ```
   https://quocviet0304.github.io/ios_automation/
   ```
4. Bấm **Thêm nguồn (Add Source)**.
5. Tìm kiếm package **`QvAuto`** và bấm **Cài đặt (Get)**.

---

## 💻 Hỗ Trợ Lập Trình & Tự Động Hoá (API & SDK)

Hệ thống mở sẵn Embedded HTTP Server tại cổng `8080`. Bạn có thể dùng bất kỳ ngôn ngữ nào (Python, Node.js, C#, cURL) để điều khiển:

```python
import requests

IPHONE_URL = "http://192.168.1.100:8080"

# 1. Chuyển sang profile TikTok khác (tự động xoay IP 4G)
requests.post(f"{IPHONE_URL}/api/v1/profile/switch", json={
    "bundle_id": "com.ss.iphone.ugc.Ame",
    "name": "TikTok_Acc_02",
    "auto_rotate_ip": True,
    "auto_relaunch": True
})

# 2. Chạm vào màn hình (Tap)
requests.post(f"{IPHONE_URL}/api/v1/touch/tap", json={"x": 200, "y": 450})

# 3. Quét chữ trên màn hình (OCR)
ocr_res = requests.post(f"{IPHONE_URL}/api/v1/vision/ocr", json={}).json()
print("Kết quả quét chữ:", ocr_res)
```

---

## 💬 Liên Hệ Hỗ Trợ & Mua Bản Quyền (Contact & Support)

Mọi thắc mắc về cài đặt, hỗ trợ kỹ thuật kịch bản tự động hoá hoặc đăng ký kích hoạt bản quyền License Key:

* **Telegram:** [@viethappy_0205](https://t.me/viethappy_0205) *(Hỗ trợ 24/7)*
* **Kênh trao đổi:** [https://t.me/viethappy_0205](https://t.me/viethappy_0205)

---

<p align="center">
  <b>© 2026 QvAuto Team. All Rights Reserved.</b>
</p>
