## PHẦN 1 — PHÂN TÍCH QUY TRÌNH NGHIỆP VỤ

### 1.1. Các thành phần của Activity Diagram

Start Node: Điểm bắt đầu khi Khách hàng mở ứng dụng và bắt đầu tìm kiếm món ăn

End Node: Điểm kết thúc sau khi Shipper hoàn tất giao hàng cho Khách hàng hoặc khi quy trình bị kết thúc do món ăn hết

Action Nodes: Mở ứng dụng, Tìm kiếm món ăn, Nhấn Đặt hàng, Kiểm tra tồn kho, Hiển thị tổng tiền, Gọi Cổng Momo, Xác nhận thanh toán, Xử lý thanh toán, Hiển thị lỗi, Chọn lại phương thức thanh toán, Gửi SMS xác nhận, Thông báo đơn hàng mới, Nhận đơn, Giao hàng

Decision Node 1: Kiểm tra tồn kho — xác định món ăn còn hàng hoặc hết hàng

Decision Node 2: Kiểm tra thanh toán — xác định thanh toán thành công hoặc thất bại

Fork Node: Sau khi thanh toán thành công, hệ thống tách thành 2 luồng xử lý song song gồm gửi SMS xác nhận cho Khách hàng và thông báo đơn hàng mới cho Shipper

Join Node: Đồng bộ 2 nhánh xử lý song song trước khi kết thúc quy trình

## PHẦN 2 — NHẬN DIỆN TÁC NHÂN VÀ TRÍCH XUẤT CA SỬ DỤNG

### 2.1. Các tác nhân

Actor chính: Khách hàng

tìm kiếm món ăn, đặt đồ ăn, thực hiện thanh toán và lựa chọn phương thức thanh toán

Actor chính: Shipper

nhận đơn hàng mới và tiến hành giao đồ ăn cho Khách hàng

Actor phụ: Cổng Momo

tiếp nhận và xử lý giao dịch thanh toán, sau đó trả về kết quả thành công hoặc thất bại cho Hệ thống QuickBite

Actor phụ: Máy chủ SMS

gửi tin nhắn SMS xác nhận đơn hàng cho Khách hàng

### 2.2. Các case sử dụng

Use Case 1: Tìm kiếm món ăn

Use Case 2: Đặt đồ ăn

Use Case 3: Xác thực tài khoản (include từ Use Case 2, bắt buộc phải thực hiện để hoàn thành đặt đồ ăn)

Use Case 4: Thanh toán đơn hàng

Use Case 5: Áp mã giảm giá (extend từ Use Case 2 khi Khách hàng có nhu cầu sử dụng mã giảm giá)

Use Case 6: Nhận đơn giao hàng

Use Case 7: Giao hàng

Use Case 8: Gửi thông báo SMS

## PHẦN 3 — ĐẶC TẢ USE CASE

### Use Case: Đặt đồ ăn và Thanh toán

#### Tên và ID Use Case

Tên: Đặt đồ ăn và Thanh toán

ID: UC-01

####  Actor và Mô tả

Actor chính: Khách hàng

Actor phụ: Cổng Momo, Máy chủ SMS

Mô tả: Khách hàng lựa chọn món ăn và thực hiện đặt hàng. Hệ thống QuickBite kiểm tra tồn kho, xử lý thanh toán qua Cổng Momo và xác nhận đơn hàng sau khi thanh toán thành công.

#### Pre-conditions

Khách hàng đã đăng nhập tài khoản QuickBite

Khách hàng đã lựa chọn ít nhất một món ăn để đặt

Món ăn đang được bán trên hệ thống

Cổng Momo đang sẵn sàng tiếp nhận giao dịch thanh toán

#### Post-conditions

Đơn hàng được tạo thành công

Kết quả thanh toán được ghi nhận thành công

Khách hàng nhận được SMS xác nhận đơn hàng

Shipper nhận được thông báo có đơn hàng mới

#### Main Flow

Bước 1: Khách hàng tìm kiếm và lựa chọn món ăn, sau đó nhấn [Đặt hàng]

Bước 2: Hệ thống QuickBite kiểm tra số lượng tồn kho và hiển thị tổng tiền của đơn hàng

Bước 3: Hệ thống QuickBite gửi yêu cầu thanh toán sang Cổng Momo

Bước 4: Khách hàng xác nhận thanh toán trên Cổng Momo

Bước 5: Cổng Momo xử lý giao dịch và trả về kết quả thanh toán thành công cho Hệ thống QuickBite

Bước 6: Hệ thống QuickBite ghi nhận đơn hàng đã thanh toán, đồng thời gửi SMS xác nhận cho Khách hàng và thông báo đơn hàng mới cho Shipper

#### Alternative Flow

A1: Hết món ăn trong kho

A1.1: Rẽ nhánh từ Bước 2 của Main Flow khi Hệ thống QuickBite phát hiện món ăn đã hết

A1.2: Hệ thống hiển thị thông báo "Món ăn đã hết"

A1.3: Hệ thống không tạo đơn hàng và đóng Use Case

A2: Thanh toán Momo thất bại

A2.1: Rẽ nhánh từ Bước 5 của Main Flow khi Cổng Momo trả về kết quả thanh toán thất bại

A2.2: Hệ thống hiển thị thông báo "Thanh toán thất bại"

A2.3: Hệ thống cho phép Khách hàng chọn lại phương thức thanh toán

A2.4: Khách hàng chọn lại phương thức thanh toán, hệ thống quay lại Bước 3 để tiếp tục thực hiện thanh toán
