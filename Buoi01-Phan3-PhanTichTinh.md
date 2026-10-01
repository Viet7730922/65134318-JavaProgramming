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
| 1 | 9 | `no-unused-vars` | Khai báo thư viện `fs` nhưng không sử dụng ở bất kỳ đâu trong file. | Tốn bộ nhớ nạp module thừa, code rác gây khó hiểu. | SMELL | Xóa dòng `const fs = require('fs');`. |
| 2 | 14 | `no-dupe-keys` | Khóa `noiThanh` bị khai báo lặp lại 2 lần trong object `SHIPPING_CONFIG`. | Giá trị `noiThanh: 25000` bị ghi đè lên `20000`, làm sai lệch giá trị phí nội thành ban đầu. | DEFECT | Xóa dòng `noiThanh: 25000,` thừa ở dòng 14. |
| 3 | 22 | `no-undef` | Biến `totl` trả về chưa được khai báo (gõ sai chính tả của `total`). | Chương trình văng lỗi `ReferenceError: totl is not defined` và dừng đột ngột khi gọi hàm. | DEFECT | Đổi `return totl;` thành `return total;`. |
| 4 | 27 | `eqeqeq` | Dùng toán tử so sánh lỏng lẻo `==` thay vì so sánh nghiêm ngặt `===`. | Có thể xảy ra ép kiểu ngầm định ngoài ý muốn. | SMELL | Đổi thành `if (qty === 0 \|\| qty === '0')` hoặc ép sang số nguyên trước khi so sánh `===`. |
| 5 | 30 | `no-cond-assign` | Dùng phép gán `=` thay vì toán tử so sánh `===` trong biểu thức điều kiện `if`. | Biến `qty` luôn bị gán lại thành `100` (luôn `truthy`), hàm luôn trả về `false` với mọi số lượng. | DEFECT | Sửa `if (qty = 100)` thành `if (qty === 100)` (hoặc sửa logic kiểm tra khoảng 1–99: `if (qty < 1 \|\| qty > 99)`). |
| 6 | 38 | `valid-typeof` | So sánh `typeof price === 'numbr'` bị gõ sai tên kiểu dữ liệu (`'numbr'` thay vì `'number'`). | Biểu thức luôn trả về `false`, bỏ qua bước kiểm tra kiểu dữ liệu của biến. | DEFECT | Sửa `'numbr'` thành `'number'` (hoặc `typeof price !== 'number'`). |
| 7 | 41 | `use-isnan` | So sánh trực tiếp biến với `NaN` bằng `price === NaN`. | Trong JavaScript, `NaN === NaN` luôn là `false`, khiến lệnh kiểm tra bị vô hiệu hóa hoàn toàn. | DEFECT | Đổi thành `if (Number.isNaN(price))`. |
| 8 | 51 | `no-fallthrough` | Thiếu lệnh `break;` ở nhánh `case 'noi-thanh':`. | Luồng thực thi bị rơi xuống nhánh tiếp theo, biến `fee` luôn nhận giá trị của `ngoaiThanh` dù đầu vào là nội thành. | DEFECT | Thêm `break;` ngay sau dòng `fee = SHIPPING_CONFIG.noiThanh;`. |
| 9 | 65 | `no-dupe-else-if` | Điều kiện `customer.type === 'VIP'` bị lặp lại ở cả nhánh `if` và `else if`. | Khối lệnh trong nhánh `else if` không bao giờ được thực thi (Dead code). | DEFECT | Sửa nhánh `else if` thành loại khách hàng phù hợp hoặc xóa nếu trùng lặp. |
| 10 | 69 | `no-unreachable` | Lệnh `console.log(...)` nằm ngay sau câu lệnh `return 0;`. | Dòng lệnh này không bao giờ được chạm tới và thực thi (Dead code). | SMELL | Chuyển `console.log` lên trước câu lệnh `return` hoặc xóa bỏ. |
| 11 | 74 | `no-unsafe-negation` | Toán tử phủ định `!` đặt trước toán tử `in` (`!productId in cart`). | Do thứ tự ưu tiên, JS đánh giá `(!productId) in cart` dẫn đến kết quả logic sai hoàn toàn. | DEFECT | Thêm ngoặc tròn bao quanh: `if (!(productId in cart))`. |
| 12 | 83 | `no-empty` | Khối lệnh `catch (e)` để trống, không xử lý lỗi. | Nuốt lỗi âm thầm (swallow error), gây khó khăn khi debug nếu chuỗi JSON không hợp lệ. | SMELL | Ghi log lỗi `console.error(e)` hoặc xử lý trả về `null`. |
| 13 | 83 | `no-unused-vars` | Biến `e` trong mệnh đề `catch (e)` được khai báo nhưng không dùng. | Biến thừa trong mã nguồn. | SMELL | Sử dụng `e` để log hoặc dùng cú pháp Optional Catch Binding: `catch { ... }`. |
| 14 | 114 | `no-unused-vars` | Tham số `kyHieu` trong hàm `dinhDangTien` được khai báo nhưng không dùng. | Tạo kỳ vọng sai cho người gọi hàm rằng có thể tùy biến ký hiệu tiền tệ. | SMELL | Sử dụng tham số `kyHieu` thay vì hardcode `'đ'`, hoặc xóa tham số thừa nếu không cần. |
| 15 | 10-14 | `prefer-const` / `quotes` | Sử dụng nháy đơn/nháy kép không nhất quán hoặc khai báo biến có thể dùng `const`. | Ảnh hưởng tính đồng nhất của phong cách viết mã (code styling). | SMELL | Chuẩn hóa theo cấu hình style guide quy định. |
| 16 | 20 | `semi` / formatting | Thiếu dấu chấm phẩy hoặc khoảng trắng không đúng chuẩn linter. | Gây cảnh báo style format mã nguồn. | SMELL | Thêm dấu chấm phẩy đầy đủ theo quy định của dự án. |
| 17 | 49 | `default-case` | Cấu trúc `switch` thiếu nhánh `default` để bắt các trường hợp khu vực không hợp lệ. | Khi truyền `zone` sai, `fee` vẫn giữ nguyên giá trị 0 mà không có cảnh báo. | SMELL | Bổ sung nhánh `default: break;` hoặc ném ngoại lệ khi `zone` không hợp lệ. |
| 18 | 90 | `complexity` / `max-depth` | Các khối `if-else` lồng nhau quá sâu trong hàm `xepHangKhachHang`. | Làm tăng độ phức tạp thuật toán (Cyclomatic Complexity), mã khó đọc và khó viết unit test. | SMELL | Tách nhỏ hàm hoặc sử dụng guard clauses để return sớm. |
| 19 | 108 | `no-unused-vars` / `no-console` | Lệnh `console.log` được dùng trong hàm tính toán nghiệp vụ `tinhTongDon`. | Ô nhiễm output terminal khi chạy production/test. | SMELL | Xóa bỏ dòng `console.log` phục vụ debug. |

## 3. Sau khi sửa

Kết quả `npm run lint:lab` sau khi sửa (ảnh chụp hoặc dán kết quả):

```

```

## 4. Lỗi logic ESLint không phát hiện được

| STT | Hàm | Mô tả lỗi | Căn cứ (chú thích hàm / mục SRS) | Vì sao ESLint không phát hiện được? |
|---|---|---|---|---|
| 1 | `tinhTongDon` | Công thức tính toán bị sai dấu: `return tamTinh - giamGia - phi;` (đang trừ phí vận chuyển thay vì cộng). | Chú thích hàm dòng 104 và **Mục FR-05.2 của SRS**: "Tổng tiền phải trả = Tạm tính − Giảm giá + Phí vận chuyển". | ESLint chỉ kiểm tra cú pháp và cấu trúc ngữ pháp tĩnh (Syntax & Structure), không hiểu được ngữ nghĩa và nghiệp vụ logic số học của con người. |
| 2 | `kiemTraSoLuong` | Hàm không kiểm tra các giá trị âm (`qty < 0`), giá trị lớn hơn 100 (`qty > 100`), hoặc kiểu dữ liệu số thực/không phải số nguyên. | Chú thích hàm dòng 25 và **Mục FR-03.2 của SRS**: "Số lượng của mỗi sản phẩm là số nguyên từ 1 đến 99". | Mã nguồn vẫn là cấu trúc `if-return` hợp lệ về mặt ngữ pháp JavaScript, ESLint không thể tự suy luận phạm vi nghiệp vụ từ 1 đến 99. |

## 5. (Không bắt buộc) Nhận xét về phân tích tĩnh trong trình soạn thảo

- **Lợi ích:** Phân tích tĩnh (Static Analysis) như ESLint tích hợp trực tiếp trên IDE (VS Code) giúp phát hiện ngay tức thì các lỗi gõ sai biến (totl), lỗi cú pháp gán nhầm (=), lỗi quên break trong switch-case và code rác ngay khi đang gõ, giúp tiết kiệm thời gian debug run-time rất lớn.   
- **Giới hạn:** Phân tích tĩnh không thể thay thế việc viết Unit Test và kiểm thử chức năng, vì linter hoàn toàn không thể phát hiện các lỗi sai lệch công thức nghiệp vụ (như cộng thành trừ ở hàm tinhTongDon). 