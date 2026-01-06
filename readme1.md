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
gh release create v1.0.10 app.exe   --title "Version 1.0.10"   --notes "Không gắn lại trackId empty sau khi timeout xong"

## 3. Tính checksum SHA256 (bắt buộc)
Mở **PowerShell** (không dùng CMD cũ) và chạy lệnh sau:

```powershell
Get-FileHash app.exe -Algorithm SHA256 | Select-Object Hash

## 4. Cập nhật lại ở SQL

| Tên cột | Giá trị | Mô tả |
|---------|---------|-------|
| AppDesktopVersion | 1.0.0 | Version của phần mềm |
| AppUrlRelease | https://github.com/CromBorw2e36/parking-product/releases/download/v1.0.3/app.exe | Đường dẫn của file release |
| AppChangeLogUrl | https://github.com/CromBorw2e36/parking-product/releases/tag/v1.0.3 | Nội dung update phần mềm |
| AppMandatoryUpdate | true | Giá trị: true/false; Nếu bản sửa lỗi gấp thì true |
| AppChecksum | 85865A2B866307B1143D4D669B801428BC5FA053289E36546F0BB014572E79BF | Mã checksum SHA256 |
Cập nhật version ở 
```bash
K:\Project\HungDuyCoLTD\HungDuyParking\HungDuyParking\Properties\AssemblyInfo.cs

[assembly: AssemblyVersion("1.0.2.0")]
[assembly: AssemblyFileVersion("1.0.2.0")]
```