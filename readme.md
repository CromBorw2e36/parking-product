# Hướng dẫn tạo và upload bản Release mới

## 1. Build file .exe bằng Inno Setup
- Mở file script Inno Setup (thường có đuôi `.iss`)
- Compile/build → sẽ tạo ra file thực thi tên là: `app.exe`

## 2. Đổi tên và nén file
- Copy file `app.exe` vừa build được
- Đổi tên file nén theo chuẩn: `app[x.x.x].zip`  
  Ví dụ phiên bản 1.0.2 → tạo file `app1.0.2.zip`
- Nén file `app.exe` thành file zip có đúng tên như trên (dùng 7-Zip, WinRAR hoặc Windows gửi đến → Thư mục nén (zip))

## 3. Tạo Release mới trên GitHub bằng lệnh gh (GitHub CLI)

Mở Command Prompt / PowerShell / Terminal và chạy lệnh sau:

```bash
gh release create v1.0.2 app1.0.2.zip ^
  --title "Version 1.0.2" ^
  --notes "Các cập nhật trong phiên bản này:
- Sửa lỗi tính tiền giờ lẻ
- Thêm tính năng xuất báo cáo theo ca
- Cập nhật giao diện danh sách xe ra vào
- Tối ưu hiệu suất tải dữ liệu"

## 3. Tính checksum SHA256 (bắt buộc)
Mở **PowerShell** (không dùng CMD cũ) và chạy lệnh sau:

```powershell
Get-FileHash app1.0.2.zip -Algorithm SHA256 | Select-Object Hash