# Bài 3: Cấu hình xác thực SSH và Đẩy dự án lên GitHub

## 1. Khởi tạo cặp khóa SSH (thuật toán Ed25519)

Mở terminal (Git Bash, PowerShell hoặc Terminal) và chạy lệnh sau để tạo cặp khóa SSH mới (thay thế email của bạn):

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

Khi được hỏi nơi lưu trữ khóa, nhấn **Enter** để chấp nhận đường dẫn mặc định (thường là `~/.ssh/id_ed25519`). Bạn cũng có thể thiết lập mật khẩu (passphrase) cho khóa để tăng cường bảo mật.

Sau khi tạo xong, bật `ssh-agent` chạy ngầm và thêm khóa vào agent:

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

## 2. Thêm khóa công khai (Public Key) vào GitHub

Lấy nội dung của khóa công khai bằng lệnh:

```bash
cat ~/.ssh/id_ed25519.pub
```
*(Trên Windows, bạn cũng có thể mở tệp này bằng Notepad)*

Copy toàn bộ nội dung xuất ra. Đăng nhập vào tài khoản GitHub của bạn:
1. Nhấn vào ảnh đại diện góc trên cùng bên phải và chọn **Settings**.
2. Chọn mục **SSH and GPG keys** ở thanh điều hướng bên trái.
3. Nhấp vào **New SSH key**, đặt tên cho khóa (ví dụ: "Laptop của tôi") và dán nội dung đã copy vào trường **Key**.
4. Chọn **Add SSH key**.

## 3. Kiểm tra kết nối SSH tới GitHub

Kiểm tra xem kết nối đã được thiết lập thành công hay chưa bằng cách sử dụng lệnh:

```bash
ssh -T git@github.com
```

Kết quả mong đợi (nếu thành công, bạn sẽ nhận được thông báo):
```
Hi username! You've successfully authenticated, but GitHub does not provide shell access.
```

## 4. Cấu hình liên kết an toàn (Remote Repository)

Di chuyển vào thư mục dự án cục bộ của bạn. Nếu bạn chưa liên kết với kho lưu trữ từ xa, sử dụng lệnh `add`:

```bash
git remote add origin git@github.com:username/repository.git
```

*(Lưu ý: Thay `username` và `repository.git` bằng thông tin chính xác từ kho lưu trữ GitHub của bạn)*

Nếu dự án của bạn đang sử dụng giao thức HTTPS và bạn muốn chuyển sang SSH, hãy sử dụng lệnh `set-url`:

```bash
git remote set-url origin git@github.com:username/repository.git
```

## 5. Kiểm tra cấu hình remote URL

Kiểm tra lại đường dẫn của kho lưu trữ từ xa bằng lệnh:

```bash
git remote -v
```

Kết quả mong đợi:
```
origin  git@github.com:username/repository.git (fetch)
origin  git@github.com:username/repository.git (push)
```

## 6. Đẩy dự án lên GitHub qua SSH

Cuối cùng, tiến hành đẩy (push) mã nguồn và lịch sử commit của bạn lên nhánh chính trên GitHub:

```bash
git push -u origin main
```

*(Nếu nhánh chính của bạn tên là `master`, hãy thay `main` bằng `master`)*

---

**Link tới kho lưu trữ GitHub đã cấu hình:**
[Thay thế bằng đường dẫn tới kho lưu trữ GitHub của bạn tại đây]
