# 🚀 Smart-Farm – Hệ thống IoT cho Trang trại Lan

![Sơ đồ hệ thống Smart-Farm tại trang trại Lan](https://rikkeiedu-storage.s3.ap-southeast-2.amazonaws.com/uploads/editor-images/1787648283613_687ec2e7-229c-4942-a347-080fae59560a.webp)

## 1. Mô tả

**Smart-Farm** là hệ thống hỗ trợ giám sát và tưới cây tự động cho trang trại Lan bằng công nghệ *IoT (Internet of Things – Internet vạn vật)*.

Hệ thống thu thập dữ liệu từ các cảm biến, xử lý dữ liệu bằng bộ điều khiển trung tâm và điều khiển máy bơm nước theo điều kiện thực tế. Mục tiêu là giúp người nông dân **giảm thao tác thủ công**, *theo dõi môi trường dễ dàng* và sử dụng nước hiệu quả hơn.

### Phân tích Input / Process / Output

| Thành phần | Nội dung | Ví dụ |
| --- | --- | --- |
| **Input – Đầu vào** | Dữ liệu từ cảm biến | Nhiệt độ, độ ẩm đất, độ ẩm không khí |
| **Process – Xử lý** | Bộ điều khiển phân tích dữ liệu và so sánh với ngưỡng | Kiểm tra đất có quá khô hay không |
| **Output – Đầu ra** | Thiết bị thực hiện hành động | Bật/tắt máy bơm, gửi cảnh báo |

### Sơ đồ phối hợp phần cứng

```text
[Cảm biến nhiệt độ] ─┐
[Cảm biến độ ẩm đất] ├──> [Bộ điều khiển / SoC] ───> [Relay] ───> [Máy bơm]
[Cảm biến độ ẩm KK] ─┘             │
                                   └────> [Màn hình / Ứng dụng giám sát]
```

Trong đó, **SoC (System on Chip – hệ thống trên chip)** đóng vai trò trung tâm, tiếp nhận dữ liệu từ cảm biến, xử lý lệnh và điều khiển thiết bị đầu ra.

---

## 2. Hướng dẫn cài đặt

### Yêu cầu

- Bộ điều khiển IoT hoặc SoC tương thích.
- Cảm biến nhiệt độ và độ ẩm.
- Cảm biến độ ẩm đất.
- Relay điều khiển máy bơm.
- Máy tính có Git và môi trường chạy chương trình.

### Cài đặt

Mở Terminal hoặc PowerShell và chạy:

```bash
git clone https://github.com/example/smart-farm.git
cd smart-farm
npm install
npm start
```

Sau khi chương trình khởi động, kiểm tra kết nối giữa cảm biến, bộ điều khiển và máy bơm trước khi bật chế độ tưới tự động.

---

## 3. Tính năng

- [x] Đọc nhiệt độ môi trường.
- [x] Đọc độ ẩm đất.
- [x] Hiển thị dữ liệu cảm biến.
- [x] Tự động bật máy bơm khi đất khô.
- [x] Tắt máy bơm khi độ ẩm đạt mức yêu cầu.
- [ ] Gửi cảnh báo về điện thoại khi cảm biến gặp lỗi.
- [ ] Đồng bộ dữ liệu lên hệ thống đám mây.

---

## 4. Bảng thông số

| Thông số | Giá trị tham khảo | Đơn vị | Mục đích |
| :--- | :---: | :---: | --- |
| Nhiệt độ cảnh báo cao | 35 | °C | Cảnh báo môi trường quá nóng |
| Độ ẩm đất tối thiểu | 40 | % | Ngưỡng kích hoạt tưới |
| Độ ẩm đất mục tiêu | 70 | % | Ngưỡng dừng tưới |
| Chu kỳ đọc cảm biến | 5 | giây | Cập nhật dữ liệu |
| Thời gian tưới tối đa | 10 | phút | Tránh tưới quá lâu |

---

## 5. Hoạt động của hệ thống

### Chu kỳ Fetch–Decode–Execute của CPU khi nhận lệnh tưới Lan

> **Fetch – Nạp lệnh:** CPU lấy lệnh điều khiển tưới từ bộ nhớ chương trình.
>
> **Decode – Giải mã:** CPU xác định lệnh yêu cầu kiểm tra độ ẩm đất và điều khiển máy bơm.
>
> **Execute – Thực thi:** CPU gửi tín hiệu đến relay để bật máy bơm nếu độ ẩm đất thấp hơn ngưỡng cho phép.
>
> Sau khi thực thi, CPU tiếp tục chu kỳ mới để theo dõi trạng thái cảm biến và quyết định khi nào cần tắt máy bơm.

### Mô hình DIKW trong Smart-Farm

Quy trình chuyển dữ liệu nhiệt độ và độ ẩm thành hành động tưới có thể mô tả bằng kim tự tháp **DIKW**:

```text
                 /\
                /  \
               / W  \     Wisdom – Trí tuệ
              /------\    Quyết định tưới phù hợp để bảo vệ cây
             /   K    \   Knowledge – Kiến thức
            /----------\  Biết đất khô + nhiệt độ cao làm cây cần nước
           /     I      \ Information – Thông tin
          /--------------\ Dữ liệu được so sánh với ngưỡng
         /       D        \ Data – Dữ liệu
        /------------------\ 36°C, độ ẩm đất 32%
```

Ví dụ:

1. **Data – Dữ liệu:** Cảm biến ghi nhận nhiệt độ `36°C` và độ ẩm đất `32%`.
2. **Information – Thông tin:** Hệ thống nhận ra độ ẩm đất đang thấp hơn ngưỡng `40%`.
3. **Knowledge – Kiến thức:** Hệ thống biết đất khô trong điều kiện nhiệt độ cao có thể khiến cây Lan thiếu nước.
4. **Wisdom – Trí tuệ:** Hệ thống quyết định bật máy bơm trong giới hạn an toàn và dừng khi đất đạt độ ẩm mục tiêu.

---

## Lưu ý

- Không bật chế độ tưới tự động nếu cảm biến độ ẩm đất chưa được kết nối đúng.
- Kiểm tra relay và nguồn cấp trước khi vận hành máy bơm.
- Không để máy bơm hoạt động liên tục vượt quá thời gian tưới tối đa.
- Nên sao lưu dữ liệu quan trọng trước khi cập nhật chương trình.

### Xử lý khi RAM bị đầy do dữ liệu nhật ký

Nếu hệ thống có dấu hiệu chậm, treo hoặc RAM bị đầy do file nhật ký tăng quá nhanh:

1. **Không xóa tiến trình hoặc tắt nguồn đột ngột** nếu hệ thống đang điều khiển máy bơm.
2. Chuyển hệ thống sang **chế độ điều khiển thủ công** hoặc tạm dừng chức năng ghi log nếu có thể.
3. Kiểm tra dung lượng log và xác định file nào đang tăng bất thường.
4. Sao lưu các log quan trọng trước khi xóa hoặc lưu trữ.
5. Xóa hoặc nén các log cũ thay vì xóa toàn bộ dữ liệu.
6. Khởi động lại dịch vụ ghi log sau khi bộ nhớ đã được giải phóng.
7. Thiết lập cơ chế **log rotation** để giới hạn kích thước và số lượng file log trong tương lai.

Ví dụ kiểm tra dung lượng file log trên Linux:

```bash
du -sh logs/*
```

Ví dụ nén log cũ:

```bash
gzip logs/smart-farm-old.log
```

> **Khuyến nghị:** Hệ thống nên giới hạn kích thước mỗi file log và tự động xoay vòng nhật ký để tránh tình trạng RAM hoặc bộ nhớ lưu trữ bị sử dụng hết.

---

## Ghi nhớ nhanh

```text
Cảm biến → Input
SoC/CPU → Process
Máy bơm / Cảnh báo → Output

CPU: Fetch → Decode → Execute
DIKW: Data → Information → Knowledge → Wisdom
```

**Smart-Farm** giúp biến dữ liệu cảm biến thành quyết định và hành động thực tế, từ đó hỗ trợ người nông dân chăm sóc cây Lan chính xác và an toàn hơn.
