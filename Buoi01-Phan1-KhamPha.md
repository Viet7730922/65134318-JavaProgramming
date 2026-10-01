# BUỔI 1 – PHẦN 1: CÀI ĐẶT VÀ KHÁM PHÁ HỆ THỐNG

- **Họ tên:** Võ Quốc Việt
- **MSSV:** 65134318
- **Lớp:** 65.CNTT-1

## 1. Môi trường

| Mục | Kết quả |
|---|---|
| Phiên bản Node.js (`node -v`) | v24.21.0 |
| Phiên bản npm (`npm -v`) | 11.19.0 |
| Phiên bản Git (`git --version`) | 2.51.1.windows.1 |
| Hệ điều hành | Windows 11 |
| Kết quả `npm run lint` (số error / warning) | 16/3 |

Ảnh chụp màn hình (chèn ảnh hoặc đặt file ảnh trong thư mục `bai-nop/hinh/` rồi dẫn link):

- Trang web MiniShop NTU: http://localhost:3000
- Terminal đang chạy server: CMD (C:\Users\ASUS\sot357-65134318)

## 2. Kịch bản 1 – Đăng ký với tuổi 17

| Câu hỏi | Trả lời |
|---|---|
| Kết quả thực tế | Đăng ký thành công |
| Kết quả mong đợi (theo SRS, ghi rõ mục) | FR-01.3 |
| Có phải failure không? Vì sao? | Phải đó là failure. Vì kết quả thực tế (hệ thống cho phép đăng ký) sai lệch so với kết quả kỳ vọng/đặc tả yêu cầu (chặn người dùng dưới 18 tuổi). |
| Defect nằm ở đâu (file, số dòng, đoạn mã) | file registration.js, dòng 20 , đoạn mã: } else if (ageNumber < 17 || ageNumber > 100) { |
| Error nào của con người có thể đã gây ra defect này? | Lỗi nhầm lẫn điều kiện biên (Off-by-one Error) hoặc hiểu sai yêu cầu nghiệp vụ: Lập trình viên nhầm lẫn giữa "trên 17 tuổi" (> 17 tức là >= 18) với việc chặn người dùng bằng điều kiện < 17 thay vì < 18 (hoặc sơ suất gõ nhầm số 17 thay cho số 18 khi viết mã) |

## 3. Kịch bản 2 – Đơn hàng 500.000đ, nội thành

| Câu hỏi | Trả lời |
|---|---|
| Tạm tính | 500.000đ |
| Phí vận chuyển hệ thống tính | 20.000đ |
| Theo FR-04.2, phí đúng phải là | 20.000đ |
| Theo Phụ lục A, phí đúng phải là | 0đ (dòng số 3 ghi rõ: Thành viên Thường, Nội thành, Tạm tính 500.000đ có Phí vận chuyển là 0đ) |
| Hệ thống đúng hay sai? Có kết luận được không? Vì sao? | Chưa thể kết luận được hệ thống đúng hay sai. Vì đang có sự "Mâu Thuẫn" nội bộ trong chính tài liệu yêu cầu (SRS): mục FR-04.2 quy định "trên 500.000đ" (tức > 500.000đ, tính phí 20.000đ), nhưng bảng ví dụ ở Phụ lục A (dòng 3) lại minh họa 500.000đ được miễn phí (phí 0đ). Cần liên hệ với Product Owner / Business Analyst (BA) để làm rõ yêu cầu trước. |
| Defect (nếu có) nằm ở đâu: mã nguồn hay tài liệu? | SRS-MiniShop-v1.0.md |

## 4. Kịch bản 3 – Tự khám phá

| Mục | Nội dung |
|---|---|
| Chức năng | Đăng ký tài khoản (Kiểm tra độ dài mật khẩu) |
| Các bước thực hiện | 1. Truy cập trang web MiniShop NTU (http://localhost:3000), mở form Đăng ký tài khoản. <br> 2. Nhập họ tên hợp lệ, email hợp lệ, tuổi hợp lệ (ví dụ: 20 tuổi) và nhập mật khẩu đúng 21 ký tự (ví dụ: 123456789012345678901). <br> 3. Nhấn nút Đăng ký. |
| Dữ liệu sử dụng | Họ Tên: Trần Trung Kiên; Email: kien333@ntu.edu.vn; Tuổi: 21; Mật khẩu: 123456789012345678901 (21 ký tự) |
| Kết quả mong đợi (căn cứ: mục nào của SRS) | Hệ thống báo lỗi và không cho đăng ký vì mật khẩu vượt quá số ký tự quy định. (Căn cứ: Mục FR-01.4 của SRS, quy định: "Mật khẩu có độ dài từ 8 đến 20 ký tự...") |
| Kết quả thực tế | Hệ thống chấp nhận mật khẩu 21 ký tự và thông báo "Đăng ký thành công" (do code tại file registration.js kiểm tra điều kiện lỗi là pwd.length > 21 thay vì > 20). |
| Nhận định (failure? mức độ?) | Là một Failure. Mức độ: Medium (Trung bình) - Hệ thống chấp nhận mật khẩu vượt quá độ dài tối đa cho phép theo đặc tả nghiệp vụ, làm sai lệch ràng buộc dữ liệu đầu vào. |
