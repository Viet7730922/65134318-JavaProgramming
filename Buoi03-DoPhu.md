# BUỔI 3 – BÁO CÁO BAO PHỦ MÃ NGUỒN

- **Họ tên:** Võ Quốc Việt
- **MSSV:** 65134318

## 1. Kết quả đo lần đầu (chỉ với ca của Phần 1)

Chạy `npm run coverage` **trước khi** bổ sung ca ở Phần 3.

| File | % Statements | % Branch | % Functions |
|---|---|---|---|
| src/services/shipping.js | 69.23 | 41.66 | 100 |
| src/services/cart.js | 16.66 | 14.28 | 16.66 |
| src/services/registration.js | 60.00 | 65.38 | 50.00 |
| src/services/auth.js | 0 | 0 | 0 |

## 2. Các nhánh chưa được phủ

Mở `coverage/lcov-report/index.html` để xem chi tiết. Liệt kê các nhánh chưa phủ của hai file cần đạt 100%.

| File | Dòng | Nhánh chưa phủ (mô tả) | Vì sao bộ ca Phần 1 không chạm tới |
|---|---|---|---|
| src/services/shipping.js | 9 | Nhánh ném lỗi: `!Object.prototype.hasOwnProperty.call(FEES, zone)` khi zone không thuộc danh sách | Dữ liệu CSV Buổi 2 chỉ thử nghiệm các khu vực hợp lệ ('noi-thanh', 'ngoai-thanh') để tính tiền, chưa kiểm thử ca ngoại lệ ở tầng đơn vị. |
| src/services/shipping.js | 12 | Nhánh ném lỗi: `typeof subtotal !== 'number' \|\| subtotal < 0` khi giá trị đơn hàng sai kiểu hoặc âm | Bộ ca Phần 1 chỉ truyền subtotal là số nguyên dương hợp lệ, chưa kiểm tra dữ liệu đầu vào bất thường. |
| src/services/shipping.js | 18 | Nhánh điều kiện: `customerType === 'VIP' && zone === 'noi-thanh'` nhánh rẽ false khi là VIP nhưng không phải nội thành | Phần 1 có ca VIP ngoại thành nhưng do mã nguồn viết điều kiện `&&`, nhánh VIP ngoại thành rơi xuống lệnh trả về cuối cùng mà không bao phủ đủ nhánh quyết định. |
| src/services/cart.js | 6 | `Number.isInteger(n) && n >= 0 && n <= MAX_QTY` các nhánh biên sai (số thực, số âm, số > 99) | Phần 1 mới kiểm thử một số giá trị biên cơ bản của `validateQuantity`, chưa quét hết mọi nhánh tổ hợp logic sai. |
| src/services/cart.js | 12 | `!store.carts[email]` nhánh false khi email đã tồn tại giỏ hàng | Phần 1 chưa gọi các hàm thao tác giỏ hàng liên tiếp trên cùng một email. |
| src/services/cart.js | 20, 23 | Toán tử 3 ngôi `product ? product.price : 0` khi sản phẩm không tồn tại trong kho | Phần 1 chỉ kiểm thử hàm `validateQuantity`, chưa gọi tới `cartDetail` với sản phẩm không hợp lệ. |
| src/services/cart.js | 33 | `!validateQuantity(qty)` trả về lỗi 400 | Hàm `addToCart` chưa được kiểm thử trong Phần 1. |
| src/services/cart.js | 37, 39 | `line` đã tồn tại (cập nhật số lượng) vs chưa tồn tại (thêm mới vào mảng) | Hàm `addToCart` chưa được kiểm thử trong Phần 1. |
| src/services/cart.js | 47 | `index === -1` sản phẩm không có trong giỏ hàng báo 404 | Hàm `removeFromCart` chưa được kiểm thử trong Phần 1. |

## 3. Kết quả sau khi bổ sung ca

| File | % Statements | % Branch | % Functions |
|---|---|---|---|
| src/services/shipping.js | 100 | 100 | 100 |
| src/services/cart.js | 100 | 100 | 100 |

Số ca đã bổ sung: 17 ca

## 4. Câu hỏi phân tích

**4.1.** Một hàm đạt 100% bao phủ câu lệnh nhưng chỉ 60% bao phủ nhánh. Điều đó nghĩa là gì? Cho ví dụ cụ thể từ mã nguồn MiniShop.

**4.2.** Giả sử `calcShippingFee` đạt 100% bao phủ nhánh và tất cả ca đều xanh. Có thể kết luận hàm này không còn lỗi không? Giải thích.

**4.3.** Trong bốn file ở mục 1, file nào có bao phủ thấp nhất? Nếu chỉ còn thời gian viết thêm 3 ca kiểm thử, sẽ viết cho hàm nào và vì sao?

**Trả lời:**

## 4. Câu hỏi phân tích

**4.1.** Một hàm đạt 100% bao phủ câu lệnh nhưng chỉ 60% bao phủ nhánh. Điều đó nghĩa là gì? Cho ví dụ cụ thể từ mã nguồn MiniShop.

- **Ý nghĩa:** Đạt 100% bao phủ câu lệnh (Statement Coverage) có nghĩa là toàn bộ các dòng lệnh trong hàm đều đã được chạy qua ít nhất một lần. Tuy nhiên, chỉ đạt 60% bao phủ nhánh (Branch Coverage) nghĩa là vẫn còn 40% các hướng rẽ quyết định (nhánh đúng hoặc nhánh sai của các cấu trúc điều kiện `if`, toán tử ba ngôi `? :`, hoặc biểu thức logic) chưa từng được kiểm tra. Một câu lệnh có thể được thực thi khi điều kiện thỏa mãn, nhưng trường hợp điều kiện không thỏa mãn (nhánh `false`) lại bị bỏ sót.

- **Ví dụ cụ thể từ mã nguồn MiniShop:** Trong hàm `getCart(email)` tại file `src/services/cart.js`:

  ```javascript
  function getCart(email) {
    if (!store.carts[email]) {
      store.carts[email] = [];
    }
    return store.carts[email];
  }
  ```

**4.2.** Giả sử `calcShippingFee` đạt 100% bao phủ nhánh và tất cả ca đều xanh. Có thể kết luận hàm này không còn lỗi không? Giải thích.

- **Không thể kết luận hàm không còn lỗi.**

- **Giải thích:**
  1. Bao phủ nhánh chỉ đo mã nguồn hiện có, không phát hiện được yêu cầu bị thiếu (omission errors): Độ bao phủ nhánh chỉ kiểm tra các nhánh rẽ đã được lập trình viên viết ra trong code, hoàn toàn không phát hiện được các quy tắc nghiệp vụ trong tài liệu SRS bị bỏ sót.
  2. Trường hợp ca kiểm thử viết bám theo hành vi sai của mã nguồn thay vì theo đặc tả: Trong file `src/services/shipping.js`:
     - Yêu cầu FR-04.2 quy định miễn phí vận chuyển cho đơn hàng có tạm tính "từ 500.000đ trở lên" (`>= 500000`), nhưng mã nguồn viết `subtotal > FREE_SHIPPING_THRESHOLD`.
     - Yêu cầu FR-04.3 quy định thành viên VIP được miễn phí vận chuyển ở mọi khu vực, nhưng mã nguồn chỉ miễn phí khi `zone === 'noi-thanh'`.
     
     Nếu kiểm thử viên thiết kế ca kiểm thử bám theo đúng cách viết sai của code thay vì bám sát SRS, tất cả các ca kiểm thử vẫn chạy màu xanh (Pass) và đạt 100% Branch Coverage, nhưng hàm thực tế vẫn tồn tại lỗi nghiệp vụ nghiêm trọng.

**4.3.** Trong bốn file ở mục 1, file nào có bao phủ thấp nhất? Nếu chỉ còn thời gian viết thêm 3 ca kiểm thử, sẽ viết cho hàm nào và vì sao?

- **File có bao phủ thấp nhất:** `src/services/auth.js` (đạt 0% ở tất cả các chỉ số bao phủ sau Phần 1).

- **Nếu chỉ còn thời gian viết thêm 3 ca kiểm thử:** Nên ưu tiên viết cho hàm `login` trong `src/services/auth.js` vì:
  1. **Tính chất an ninh và bảo mật cốt lõi (Security):** Đăng nhập là chốt chặn xác thực đầu tiên của hệ thống. Nếu chức năng xác thực bị lỗi, hệ thống có thể từ chối người dùng hợp lệ hoặc tạo lỗ hổng cho các cuộc tấn công dò quét mật khẩu (brute-force).
  2. **Quy tắc nghiệp vụ chuyển trạng thái phức tạp (FR-02.3, FR-02.4):** Chức năng này quản lý biến đếm số lần sai liên tiếp và trạng thái khóa tài khoản trong 15 phút. Ba ca kiểm thử cần thiết nhất bao gồm:
     - Đăng nhập thành công với email và mật khẩu chính xác.
     - Đăng nhập thất bại khi sai mật khẩu và kiểm tra tăng biến đếm `failedAttempts`.
     - Khóa tài khoản (`locked = true`) khi nhập sai mật khẩu đủ 3 lần liên tiếp theo ngưỡng `MAX_FAILED_ATTEMPTS`.



