# 📚 **AutoBank Plugin - README**

## 🎯 **Mô Tả Tổng Quan**

**AutoBank** là một plugin Bukkit/Spigot toàn diện cho hệ thống nạp tiền và quản lý giao dịch trong Minecraft server. Plugin hỗ trợ cả nạp tiền qua ngân hàng (MB Bank) và nạp thẻ cào (Card Partner API), với giao diện GUI thân thiện và hệ thống quản lý giao dịch chuyên nghiệp.

---

## ✨ **Tính Năng Chính**

### 🏦 **Hệ Thống ATM (Nạp Tiền Ngân Hàng)**
- **QR Code tự động**: Tạo mã QR cho từng giao dịch
- **Tích hợp MB Bank**: Hỗ trợ API MB Bank để kiểm tra giao dịch
- **GUI tùy chỉnh**: Giao diện ATM với các mốc nạp có thể cấu hình
- **Phần thưởng tự động**: Thực thi lệnh khi nạp thành công
- **Lịch sử giao dịch**: Theo dõi và quản lý tất cả giao dịch

### 📱 **Hệ Thống Nạp Thẻ Cào**
- **Hỗ trợ 6 nhà mạng**: VIETTEL, MOBIFONE, VINAPHONE, VIETNAMOBILE, ZING, GARENA
- **9 mệnh giá**: Từ 10K đến 1M VND
- **GUI tùy chỉnh**: Giao diện chọn nhà mạng và mệnh giá
- **Card Partner API**: Tích hợp với TheSieuRe.com
- **Check trạng thái tự động**: Theo dõi trạng thái thẻ real-time

### 🔧 **Tính Năng Quản Trị**
- **Reload config**: Reload tất cả cấu hình với một lệnh
- **Fake giao dịch**: Tạo giao dịch ảo để test
- **Check thẻ thủ công**: Kiểm tra trạng thái thẻ theo yêu cầu
- **Discord logging**: Gửi log giao dịch lên Discord
- **SQLite database**: Lưu trữ dữ liệu giao dịch

---

## 🚀 **Cài Đặt**

### **Yêu Cầu Hệ Thống**
- **Minecraft Server**: 1.20+ (Spigot/Paper)
- **Java**: Java 16+
- **Plugin Dependencies**: PlaceholderAPI (khuyến nghị)

### **Bước 1: Tải Plugin**
```bash
# Tải file JAR từ target/
AutoBank-1.0-SNAPSHOT.jar
```

### **Bước 2: Cài Đặt**
1. Đặt file JAR vào thư mục `plugins/`
2. Khởi động server
3. Plugin sẽ tự động tạo các file cấu hình

### **Bước 3: Cấu Hình**
```yaml
# config.yml - Cấu hình chính
# nap-card-gui.yml - Giao diện nạp thẻ
# plugin.yml - Thông tin plugin
```

---

## ⚙️ **Cấu Hình**

### **1. Config.yml - Cấu Hình Chính**

```yaml
# Cấu hình MB Bank
mbbank:
  account: "0376311426"
  descriptionPrefix: "dlmc"
  api-url: "http://localhost:6868/"
  thoi-gian-check-giao-dich: 10

# Cấu hình thẻ cào
card:
  api-url: "http://thesieure.com/chargingws/v2"
  partner-id: "YOUR_PARTNER_ID"
  partner-key: "YOUR_PARTNER_KEY"
  
# Cấu hình Discord
discord:
  token: "YOUR_BOT_TOKEN"
  channel-id: "YOUR_CHANNEL_ID"
```

### **2. Nap-card-gui.yml - Giao Diện Nạp Thẻ**

```yaml
settings:
  telco-gui-title: "§6§l📱 Chọn Nhà Mạng"
  telco-gui-size: 27

telcos:
  VIETTEL:
    display-name: "§a📱 VIETTEL"
    material: "DIAMOND"
    slot: 10
    enabled: true
    lore:
      - "§7Click để chọn nhà mạng này"
      - "§7Nhà mạng di động lớn nhất Việt Nam"
```

### **3. ATM-GUI Items - Cấu Hình Mốc Nạp**

```yaml
ATM-GUI:
  Items:
    nap10k:
      slot: 10
      amount: 10000
      item: BOOK
      custommodeldata: 123456
      name: "&aNạp 10,000 VND"
      lore:
        - "&7Click để nạp &a10,000 VND"
      command:
        - "give <player> diamond 1"
        - "eco give <player> 10000"
```

---

## 🎮 **Lệnh Sử Dụng**

### **Lệnh ATM**
```bash
/atm                    # Mở GUI ATM
/atm reload            # Reload toàn bộ config
/atm lichsu            # Xem lịch sử giao dịch
/atm fake <số_tiền> <player>  # Tạo giao dịch ảo
/atm checkcard <transaction_id>  # Check trạng thái thẻ
```

### **Lệnh Nạp Thẻ**
```bash
/napthe                # Mở GUI nạp thẻ
/napthe reload         # Reload config GUI
/napthe test           # Test cấu hình GUI
/napthe <telco> <amount> <code> <serial>  # Nạp thẻ trực tiếp
```

---

## 🔐 **Quyền Hạn**

```yaml
permissions:
  autobank.admin:      # Quyền quản trị (reload, fake, checkcard)
  atm.use:             # Sử dụng ATM
  atm.napthe:          # Nạp thẻ cào
  atm.lichsu:           # Xem lịch sử
  atm.top:              # Xem top nạp tiền
```

---

## 📊 **Placeholder API**

Plugin hỗ trợ PlaceholderAPI với các placeholder:

```yaml
# Top nạp tiền theo thời gian
%autobank_top_day_sv1_1%    # Top 1 ngày của server 1
%autobank_top_month_sv1_1%  # Top 1 tháng của server 1

# Tổng nạp tiền
%autobank_total_sv1%        # Tổng nạp của player hiện tại
%autobank_total_sv1_playername%  # Tổng nạp của player cụ thể

# Số tiền thô (không format)
%autobank_total_raw_sv1_playername%
```

---

## 🗄️ **Cơ Sở Dữ Liệu**

Plugin sử dụng SQLite để lưu trữ:

```sql
CREATE TABLE giao_dich (
    id BIGINT PRIMARY KEY,
    player VARCHAR(50),
    amount INT,
    status VARCHAR(20),
    timestamp DATETIME,
    server VARCHAR(50)
);
```

**Trạng thái giao dịch:**
- `PENDING`: Đang chờ xử lý
- `COMPLETED`: Hoàn thành
- `REJECTED`: Bị từ chối
- `CANCELLED`: Đã hủy

---

## 🔧 **Tùy Chỉnh Giao Diện**

### **ATM GUI**
- Thay đổi material, slot, tên, lore
- Sử dụng CustomModelData cho texture pack
- Cấu hình lệnh phần thưởng

### **Nạp Thẻ GUI**
- Tùy chỉnh nhà mạng (material, slot, enabled)
- Tùy chỉnh mệnh giá (layout, material)
- Thay đổi thông báo và validation

---

## 📝 **Log và Debug**

### **Console Logs**
```bash
[AutoBank] ✅ Đã reload cấu hình GUI nạp thẻ.
[AutoBank] 🎉 Đã reload toàn bộ cấu hình và chức năng!
[CardCharging] 🔍 Test cấu hình GUI:
```

### **Debug Mode**
```yaml
# config.yml
dev-log: true  # Bật log chi tiết
```

---

## 🚨 **Xử Lý Lỗi**

### **Lỗi Thường Gặp**
1. **Config không load**: Kiểm tra quyền file và syntax YAML
2. **API không hoạt động**: Kiểm tra URL và credentials
3. **GUI không hiển thị**: Sử dụng `/napthe test` để debug

### **Troubleshooting**
```bash
# Test cấu hình GUI
/napthe test

# Reload toàn bộ
/atm reload

# Kiểm tra log console
# Tìm các dòng [AutoBank] và [CardCharging]
```

---

## 🔄 **API Integration**

### **MB Bank API**
- Endpoint: `http://localhost:6868/`
- Method: GET
- Response: JSON với transaction history

### **Card Partner API (TheSieuRe)**
- Endpoint: `http://thesieure.com/chargingws/v2`
- Method: POST
- Authentication: Partner ID + Key
- Sign: MD5 hash

---

## 📈 **Hiệu Suất**

- **Async operations**: HTTP requests và database operations
- **Connection pooling**: SQLite connection management
- **Caching**: Placeholder cache mỗi phút
- **Background tasks**: Card status checking mỗi 30 giây

---

## 🛡️ **Bảo Mật**

- **Permission-based access**: Quyền hạn chi tiết
- **Input validation**: Kiểm tra độ dài mã thẻ/serial
- **MD5 signing**: Chữ ký API requests
- **Transaction isolation**: Mỗi giao dịch có ID duy nhất

---

## 🔮 **Tính Năng Tương Lai**

- [ ] Hỗ trợ MySQL/PostgreSQL
- [ ] Webhook notifications
- [ ] Multi-currency support
- [ ] Advanced analytics dashboard
- [ ] Mobile app integration

---

## 🆘 **Hỗ Trợ**

### **Discord Support**
```
https://discord.gg/gQvPub5KM7
```

### **Tác Giả**
- **Developer**: hoangkiet
- **Version**: 1.2
- **API Version**: 1.20

---

## 📄 **License**

Plugin này được phát triển bởi hoangkiet. Vui lòng liên hệ tác giả để được phép sử dụng thương mại.

---

## 🎯 **Kết Luận**

AutoBank là một plugin hoàn chỉnh và chuyên nghiệp cho hệ thống nạp tiền Minecraft. Với giao diện tùy chỉnh, tích hợp API đa dạng, và hệ thống quản lý giao dịch mạnh mẽ, plugin này đáp ứng mọi nhu cầu của server nạp tiền từ nhỏ đến lớn.

**Đánh giá: ⭐⭐⭐⭐⭐ (5/5)**

Plugin sẵn sàng sử dụng production với cấu hình đầy đủ và tài liệu chi tiết! 🚀

---

## 📁 **Cấu Trúc File**

```
AutoBank/
├── src/
│   └── main/
│       ├── java/org/hoangkiet/autobank/
│       │   ├── AutoBank.java              # Class chính
│       │   ├── CardCharging.java          # Xử lý nạp thẻ
│       │   ├── SQLiteManager.java         # Quản lý database
│       │   ├── DiscordLogger.java         # Log Discord
│       │   └── AutoBankPlaceholder.java   # Placeholder API
│       └── resources/
│           ├── config.yml                  # Cấu hình chính
│           ├── nap-card-gui.yml           # GUI nạp thẻ
│           ├── plugin.yml                  # Thông tin plugin
│           └── atm-gui-example.yml        # Ví dụ ATM GUI
├── target/
│   └── AutoBank-1.0-SNAPSHOT.jar         # File JAR
├── pom.xml                                # Maven config
└── README.md                              # Tài liệu này
```

---

## 🚀 **Quick Start**

1. **Tải plugin** và đặt vào `plugins/`
2. **Khởi động server** để tạo config files
3. **Chỉnh sửa config.yml** với thông tin API của bạn
4. **Reload plugin** với `/atm reload`
5. **Test GUI** với `/napthe` và `/atm`

**Chúc bạn sử dụng plugin thành công! 🎉**
