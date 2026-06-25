🚀 Phiên bản 1.0.27

✨ Tính năng mới
- Cập nhật phần mềm từ xa: server đẩy lệnh qua SignalR (CAPNHATPHANMEM), máy tự tải & cài bản mới mà không cần thao tác tay; hỗ trợ lọc theo bãi (region) để triển khai từng nơi.
- Đa làn quẹt thẻ: định tuyến đầu đọc thẻ theo từng làn dựa trên Device ID (hỗ trợ cả cổng COM và HID Raw Input); thêm công cụ dò đầu đọc và chặn phím ảo (wedge) từ đầu đọc HID.

⚡ Tối ưu & ổn định
- Giảm độ trễ nhận diện biển số khi quẹt thẻ (crop ảnh trong bộ nhớ, bỏ bước trung gian GDI).
- Chống kẹt khi quẹt nhiều thẻ liên tiếp: mỗi làn xử lý độc lập, bỏ qua lệnh trùng khi đang bận; thêm cổng làn (lane gate), debounce và timeout cho thao tác nhân viên.
- Gửi trackId 1 lần, tránh trùng lặp.
- Sửa lỗi hộp thoại cập nhật hiện lặp nhiều lần (đăng ký sự kiện đúng 1 lần).

🎨 Giao diện
- Viết lại màn hình Lịch sử.
- Cải tiến crop ảnh, panel snapshot theo làn, panel kết quả quẹt thẻ và thanh trạng thái kết nối.