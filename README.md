## Các bước thực hiện chi tiết:
### Bước 1: Đăng ký và xác thực tài khoản DigitalOcean
1. Truy cập trang chủ DigitalOcean và nhấn nút Sign Up.
2. Đăng ký tài khoản bằng email cá nhân.
3. Xác thực số điện thoại (nếu được yêu cầu) và liên kết thẻ thanh toán.
4. Kích hoạt tài khoản: Kiểm tra email để xác nhận. Tài khoản mới thường được tặng gói credit dùng thử 100 USD dùng trong 
60 ngày, đủ để thực hiện toàn bộ bài tập mà không phát sinh chi phí thực tế.

### Bước 2: Tạo cặp khóa SSH (SSH Keypair) trên máy cá nhân
1. Mở Terminal (macOS/Linux) hoặc PowerShell (Windows).
2. Chạy lệnh sau để tạo cặp khóa theo chuẩn ed25519 (chuẩn hiện đại, an toàn và nhanh hơn RSA):
`ssh-keygen -t ed25519 -C "email_cua_ban@example.com"`
3. Nhấn Enter để chấp nhận đường dẫn lưu mặc định ~/.ssh/id_ed25519.
4. Nhấn Enter hai lần để bỏ qua mật khẩu bảo vệ khóa riêng (hoặc nhập passphrase nếu muốn tăng bảo mật).
5. Kiểm tra nội dung khóa công khai:
`cat ~/.ssh/id_ed25519.pub`
6. Sao chép toàn bộ nội dung hiển thị, có dạng bắt đầu bằng `ssh-ed25519`.

### Bước 3: Lựa chọn cấu hình và khởi tạo Droplet
1. Truy cập bảng điều khiển: Đăng nhập vào DigitalOcean Console, nhấn nút Create → chọn Droplets.
2. Chọn hệ điều hành: Trong mục Choose an image, chọn tab Distributions, chọn Ubuntu 22.04 LTS.
3. Chọn gói cấu hình: Tại Choose a plan, chọn Basic plan → tab Regular SSD → Shared CPU. Chọn gói rẻ nhất từ $4-6/tháng 
với cấu hình 1 CPU, 512MB-1GB RAM, 10-25GB SSD, đủ dùng cho máy chủ thử nghiệm web.
4. Chọn vùng dữ liệu: Tại Choose a datacenter region, chọn Singapore (SGP1) - khu vực gần Việt Nam nhất cho độ trễ thấp nhất.
5. Thiết lập xác thực: Tại mục Authentication, chọn SSH Keys. Nhấn New SSH Key, dán nội dung khóa công khai đã sao chép ở
Bước 2, đặt tên ví dụ Laptop ca nhan, sau đó nhấn Add SSH Key.
6. Các tùy chọn bổ sung: Bật Monitoring (miễn phí) để theo dõi tài nguyên. Bỏ qua Backups, IPv6, Private Network để tiết 
kiệm chi phí.
7. Đặt tên và tạo: Đặt tên Droplet ví dụ dev-test-server-01, số lượng 1, sau đó nhấn nút Create Droplet.
8. Chờ khởi tạo: Quá trình cung cấp máy chủ mất khoảng 30-60 giây. Khi trạng thái chuyển sang Running, ghi lại địa chỉ IP
Public hiển thị bên cạnh tên Droplet.

### Bước 4: Kết nối thành công qua SSH
1. Mở Terminal trên máy cá nhân, chạy lệnh:
`ssh -i ~/.ssh/id_ed25519 root@<IP_PUBLIC_CUA_DROPLET>`
2. Lần đầu kết nối, gõ yes và nhấn Enter để xác nhận tiếp tục khi có cảnh báo xác thực máy chủ.
3. Nếu cấu hình đúng, bạn sẽ truy cập trực tiếp vào giao diện dòng lệnh của Ubuntu 