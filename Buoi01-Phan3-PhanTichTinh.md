# BUỔI 1 – PHẦN 3: PHÂN TÍCH TĨNH VỚI ESLINT

- **Họ tên:** Võ Quốc Việt
- **MSSV:** 65134318

## 1. Kết quả chạy công cụ

Lệnh: `npm run lint:lab`

| Tổng số problem | Số error | Số warning |
|---|---|---|
| 19 | 16 | 3 |

Ảnh chụp kết quả: Đường dẫn ảnh là bai-nop/hinh/65134318-npm-lint-lab-error-warning.png

## 2. Bảng phân tích

Phân loại: **DEFECT** (chắc chắn gây sai/dừng chương trình) · **SMELL** (khó bảo trì, tiềm ẩn rủi ro) · **CHẤP NHẬN** (không cần sửa, giải thích lý do)

| STT | Dòng | Rule | Vấn đề (giải thích bằng lời của bạn) | Hậu quả nếu chạy chương trình | Phân loại | Cách sửa |
|---|---|---|---|---|---|---|
| 1 | 9:7 | `no-unused-vars` | Module `fs` được import nhưng không dùng ở đâu trong file. | Tốn bộ nhớ nạp module thừa, mã nguồn dư thừa gây rối. | SMELL | Xóa dòng `const fs = require('fs');`. |
| 2 | 14:3 | `no-dupe-keys` | Khóa `noiThanh` bị khai báo lặp lại 2 lần trong object `SHIPPING_CONFIG`. | Giá trị `noiThanh: 25000` ở dòng 14 sẽ ghi đè lên `20000`, làm sai phí vận chuyển nội thành. | DEFECT | Xóa dòng `noiThanh: 25000,` thừa ở dòng 14. |
| 3 | 21:5 | `no-unused-vars` | Biến `total` được tính toán nhưng không sử dụng (do lệnh return gõ sai tên). | Tốn tài nguyên tính toán vô ích nếu không trả về giá trị này. | SMELL | Sửa lệnh return ở dòng 23 để sử dụng biến `total`. |
| 4 | 23:10 | `no-undef` | Biến `totl` chưa từng được khai báo (gõ sai chính tả của `total`). Cùng nguyên nhân với dòng 21:5. | Chương trình văng lỗi crash ngay lập tức: `ReferenceError: totl is not defined`. | DEFECT | Sửa `return totl;` thành `return total;`. |
| 5 | 28:11 | `eqeqeq` | Dùng toán tử so sánh lỏng lẻo `==` thay vì so sánh nghiêm ngặt `===`. | Dễ xảy ra ép kiểu ngầm định ngoài kiểm soát (ví dụ `'0' == 0` trả về true). | SMELL | Ép kiểu sang số nguyên và kiểm tra bằng toán tử nghiêm ngặt `===`. |
| 6 | 31:7 | `no-cond-assign` | Dùng phép gán `=` thay vì so sánh trong biểu thức điều kiện `if`. | Gán đè biến `qty` thành 100 thay vì kiểm tra giá trị, làm sai lệch dữ liệu biến truyền vào. | DEFECT | Sửa logic kiểm tra khoảng hợp lệ: `if (num < 1 \|\| num > 99)`. |
| 7 | 31:7 | `no-constant-condition` | Biểu thức gán `qty = 100` luôn trả về 100 (luôn truthy). Cùng nguyên nhân với dòng 31:7 ở trên. | Khối `if` luôn luôn chạy, hàm luôn trả về `false` với mọi giá trị đầu vào. | DEFECT | Thay bằng biểu thức điều kiện so sánh giá trị biên hợp lệ. |
| 8 | 39:24 | `valid-typeof` | So sánh `typeof price === 'numbr'` bị gõ sai tên kiểu dữ liệu (`'numbr'` thay vì `'number'`). | Biểu thức luôn trả về `false`, bỏ qua hoàn toàn bước kiểm tra kiểu dữ liệu số. | DEFECT | Sửa thành `typeof price !== 'number'`. |
| 9 | 42:7 | `use-isnan` | So sánh biến trực tiếp với `NaN` bằng toán tử `===` (`price === NaN`). | Trong JS, `NaN === NaN` luôn là `false`, khiến điều kiện không bao giờ bắt được `NaN`. | DEFECT | Đổi thành hàm kiểm tra chuẩn: `Number.isNaN(price)`. |
| 10 | 54:5 | `no-fallthrough` | Thiếu câu lệnh ngắt `break;` ở cuối nhánh `case 'noi-thanh':`. | Luồng xử lý bị rơi thẳng xuống nhánh ngoại thành, biến `fee` luôn bị gán lại bằng phí ngoại thành. | DEFECT | Bổ sung lệnh `break;` ngay sau dòng gán phí nội thành. |
| 11 | 68:14 | `no-dupe-else-if` | Điều kiện `customer.type === 'VIP'` ở nhánh `else if` trùng lặp hoàn toàn với nhánh `if`. | Khối lệnh bên trong nhánh `else if` không bao giờ được chạm tới (dead code). | DEFECT | Xóa bỏ nhánh `else if` trùng lặp điều kiện. |
| 12 | 72:3 | `no-unreachable` | Câu lệnh `console.log(...)` nằm ngay sau câu lệnh `return 0;`. | Dòng code này không bao giờ được chạm tới và thực thi trong hàm. | SMELL | Xóa bỏ lệnh `console.log` thừa sau câu lệnh return. |
| 13 | 72:3 | `no-console` | Sử dụng lệnh `console.log` trong hàm tính toán `tinhGiamGia`. Cùng vị trí với dòng 72:3 ở trên. | Gây ô nhiễm luồng xuất terminal khi triển khai hệ thống hoặc chạy kiểm thử. | SMELL | Xóa bỏ lệnh `console.log` debug này. |
| 14 | 77:7 | `no-unsafe-negation` | Đặt dấu phủ định `!` đứng trước toán tử `in` (`!productId in cart`). | Do thứ tự ưu tiên, JS tính `(!productId) in cart`, dẫn đến sai hoàn toàn kết quả logic. | DEFECT | Đặt ngoặc đơn để phủ định cả biểu thức: `!(productId in cart)`. |
| 15 | 87:12 | `no-unused-vars` | Tham số ngoại lệ `e` trong mệnh đề `catch (e)` được khai báo nhưng không dùng. | Khai báo biến thừa không sử dụng trong mã nguồn. | SMELL | Sử dụng cú pháp Optional Catch Binding: `catch { return null; }`. |
| 16 | 87:15 | `no-empty` | Khối lệnh `catch` để trống không xử lý lỗi. Cùng nguyên nhân với dòng 87:12 ở trên. | Nuốt lỗi âm thầm (swallow error), gây khó khăn khi debug nếu chuỗi JSON không hợp lệ. | SMELL | Xử lý trả về giá trị an toàn: `return null;`. |
| 17 | 92:1 | `complexity` | Hàm `xepHangKhachHang` có độ phức tạp xoay vòng (complexity) là 9, vượt ngưỡng cho phép (5). | Hàm có nhiều nhánh rẽ lồng nhau, khó đọc, khó bảo trì và dễ sót trường hợp khi kiểm thử. | SMELL | Tách các nhánh xét mức chi tiêu thành 2 hàm con bổ trợ (`xepHangTren10Trieu`, `xepHangTren5Trieu`) để đưa complexity về mức cho phép. |
| 18 | 116:3 | `no-console` | Sử dụng lệnh `console.log` trong hàm tính tiền `tinhTongDon`. | Gây ô nhiễm màn hình terminal và làm giảm hiệu năng hệ thống. | SMELL | Xóa bỏ dòng `console.log` debug này. |
| 19 | 121:31 | `no-unused-vars` | Tham số `kyHieu` được khai báo trong hàm `dinhDangTien` nhưng không được dùng. | Tạo kỳ vọng sai rằng hàm có thể tùy biến ký hiệu tiền tệ, gây hiểu lầm cho người gọi hàm. | SMELL | Xóa bỏ tham số `kyHieu` không sử dụng khỏi khai báo hàm `dinhDangTien(amount)`. |

## 3. Sau khi sửa

Kết quả `npm run lint:lab` sau khi sửa (ảnh chụp hoặc dán kết quả):

```
> minishop-ntu@1.0.0 lint:lab
> eslint src/lab-static
```

## 4. Lỗi logic ESLint không phát hiện được

| STT | Hàm | Mô tả lỗi | Căn cứ (chú thích hàm / mục SRS) | Vì sao ESLint không phát hiện được? |
|---|---|---|---|---|
| 1 | `tinhTongDon` | Công thức tính toán bị sai dấu: `return tamTinh - giamGia - phi;` (đang trừ phí vận chuyển thay vì cộng). | Chú thích hàm dòng 104 và **Mục FR-05.2 của SRS**: "Tổng tiền phải trả = Tạm tính − Giảm giá + Phí vận chuyển". | ESLint chỉ kiểm tra cú pháp và cấu trúc ngữ pháp tĩnh (Syntax & Structure), không hiểu được ngữ nghĩa và nghiệp vụ logic số học của con người. |
| 2 | `kiemTraSoLuong` | Hàm không kiểm tra các giá trị âm (`qty < 0`), giá trị lớn hơn 100 (`qty > 100`), hoặc kiểu dữ liệu số thực/không phải số nguyên. | Chú thích hàm dòng 25 và **Mục FR-03.2 của SRS**: "Số lượng của mỗi sản phẩm là số nguyên từ 1 đến 99". | Mã nguồn vẫn là cấu trúc `if-return` hợp lệ về mặt ngữ pháp JavaScript, ESLint không thể tự suy luận phạm vi nghiệp vụ từ 1 đến 99. |

## 5. (Không bắt buộc) Nhận xét về phân tích tĩnh trong trình soạn thảo

- **Lợi ích:** Phân tích tĩnh (Static Analysis) như ESLint tích hợp trực tiếp trên IDE (VS Code) giúp phát hiện ngay tức thì các lỗi gõ sai biến (totl), lỗi cú pháp gán nhầm (=), lỗi quên break trong switch-case và code rác ngay khi đang gõ, giúp tiết kiệm thời gian debug run-time rất lớn.   
- **Giới hạn:** Phân tích tĩnh không thể thay thế việc viết Unit Test và kiểm thử chức năng, vì linter hoàn toàn không thể phát hiện các lỗi sai lệch công thức nghiệp vụ (như cộng thành trừ ở hàm tinhTongDon). 