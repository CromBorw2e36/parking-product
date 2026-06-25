## ĐƯỜNG DÃN CLIENT DOWNLOAD PHẦN MỀM BÃI XE KHI CÓ VERSION MỚI
## LƯU Ý: CHUYỂN REPO SANG PUBLIC

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
gh release create v1.0.27 app.exe `
  --title "Version 1.0.27" `
  --notes "🚀 Cập nhật tính năng mới:
- Cập nhật phần mềm từ xa: server đẩy lệnh qua SignalR, máy tự tải & cài bản mới (không cần thao tác tay).
- Sửa lỗi hộp thoại cập nhật hiện lặp nhiều lần (đăng ký sự kiện đúng 1 lần).
- Gửi trackId 1 lần, tránh trùng lặp.
- Cải tiến giao diện: màn hình lịch sử, crop ảnh, panel làn/quẹt thẻ."
```

Hoặc commit theo file mô tả
```bash
gh release create v1.0.27 app.exe `
  --title "v1.0.27 – Cập nhật từ xa, đa làn quẹt thẻ & tối ưu OCR" `
  --notes-file RELEASE_NOTES.md
```


## 4. Tính checksum SHA256 (bắt buộc)
Mở **PowerShell** (không dùng CMD cũ) và chạy lệnh sau:

```powershell
Get-FileHash app.exe -Algorithm SHA256 | Select-Object Hash
```

## 5. Cập nhật lại ở SQL

| Tên cột | Giá trị | Mô tả |
|---------|---------|-------|
| AppDesktopVersion | 1.0.x | Version của phần mềm |
| AppUrlRelease | https://github.com/[username]/[repo]/releases/download/v1.0.x/app.exe | Đường dẫn của file release |
| AppChangeLogUrl | https://github.com/[username]/[repo]/releases/tag/v1.0.x | Nội dung update phần mềm |
| AppMandatoryUpdate | true | Giá trị: true/false; Nếu bản sửa lỗi gấp thì true |
| AppChecksum | [SHA256_HASH] | Mã checksum SHA256 |

## 6. Cập nhật version trong source code

Cập nhật version trong file AssemblyInfo:
File Name: AssemblyInfo.cs
```csharp
[assembly: AssemblyVersion("1.0.x.0")]
[assembly: AssemblyFileVersion("1.0.x.0")]
```
