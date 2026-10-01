# BIÊN BẢN REVIEW TÀI LIỆU YÊU CẦU

## Thông tin chung

| Mục | Nội dung |
|---|---|
| Họ tên | Võ Quốc Việt |
| MSSV | 65134318 |
| Tài liệu được review | MSN-SRS – Đặc tả yêu cầu MiniShop NTU, phiên bản 1.0 |
| Loại review | Review theo checklist (cá nhân) |
| Ngày | 27/09/2026 |
| Bước 1 – Khởi động | từ …… đến …… |
| Bước 2 – Đọc lần 1 (theo trình tự) | từ …… đến …… |
| Bước 3 – Đọc lần 2 (đối chiếu chéo) | từ …… đến …… |
| Bước 4 – Hoàn thiện biên bản | từ …… đến …… |

## Danh sách lỗi

Loại lỗi: MƠ HỒ · MÂU THUẪN · THIẾU · KHÔNG KIỂM THỬ ĐƯỢC · KHÔNG KHẢ THI · THUẬT NGỮ · SAI SỐ LIỆU
Mức độ: Major · Minor

| STT | Vị trí (mã yêu cầu / mục) | Mô tả lỗi | Mã checklist | Loại lỗi | Mức độ | Tìm thấy ở lần đọc (1/2) | Đề xuất sửa |
|---|---|---|---|---|---|---|---|
| 1 | Mục 2.2 so với FR-01.3 | Mục 2.2 ghi "từ 18 tuổi trở lên" (>= 18), nhưng FR-01.3 lại ghi "phải trên 18 tuổi" (> 18). | CL-CON-01 | MÂU THUẪN | Major | 2 | Thống nhất thành: "Người dùng phải từ đủ 18 tuổi trở lên mới được đăng ký." |
| 2 | FR-01.4 | Yêu cầu "mật khẩu phải đủ mạnh để đảm bảo an toàn" quá mơ hồ, không có tiêu chí kiểm thử rõ ràng. | CL-AMB-01 | MƠ HỒ | Major | 1 | Quy định cụ thể: "Mật khẩu có từ 8–20 ký tự, gồm ít nhất 1 chữ hoa, 1 chữ thường và 1 số." |
| 3 | FR-02.3 so với NFR-03 | FR-02.3 quy định khóa tài khoản sau 3 lần sai liên tiếp, nhưng NFR-03 lại ghi sau 5 lần sai. | CL-CON-02 | MÂU THUẪN | Major | 2 | Thống nhất quy định là khóa sau 3 lần (hoặc 5 lần) ở cả hai mục. |
| 4 | FR-03.4 | Quy định "Giỏ hàng chỉ được chứa một số lượng sản phẩm hợp lý" định tính, không kiểm thử được. | CL-TST-01 | KHÔNG KIỂM THỬ ĐƯỢC | Minor | 1 | Định lượng rõ: "Giỏ hàng chứa tối đa 20 loại mặt hàng và tổng số lượng không quá 100 sản phẩm." |
| 5 | FR-04.1 so với Phụ lục A dòng 2 | FR-04.1 quy định ngoại thành là 35.000đ, nhưng Phụ lục A (dòng 2) lại tính phí 30.000đ. | CL-DAT-01 | SAI SỐ LIỆU | Major | 2 | Sửa số liệu dòng 2 Phụ lục A từ 30.000đ thành 35.000đ cho khớp với FR-04.1. |
| 6 | FR-04.2 so với Phụ lục A dòng 3 | FR-04.2 ghi "trên 500.000đ" mới miễn phí, nhưng Phụ lục A (dòng 3) tạm tính 500.000đ lại có phí là 0đ. | CL-CON-03 | MÂU THUẪN | Major | 2 | Sửa lại văn bản FR-04.2: "Đơn hàng có tạm tính từ 500.000đ trở lên được miễn phí vận chuyển." |
| 7 | FR-05.3 so với Mục 1.3 & 2.1 | Mục 1.3 và 2.1 chỉ định nghĩa Khách, Thành viên, VIP; không hề có định nghĩa nhóm "Khách hàng thân thiết". | CL-TRM-01 | THUẬT NGỮ | Minor | 2 | Bổ sung định nghĩa "Khách hàng thân thiết" vào mục 1.3, hoặc đổi thành "Thành viên VIP". |
| 8 | FR-05.5 | Quy định "Thành viên có thể hủy đơn hàng" nhưng thiếu hoàn toàn điều kiện và trạng thái được phép hủy. | CL-MIS-01 | THIẾU | Major | 1 | Bổ sung: "Thành viên chỉ được hủy đơn hàng khi đơn còn ở trạng thái 'Chờ xác nhận'." |
| 9 | NFR-01 | Yêu cầu "hệ thống phải phản hồi nhanh với mọi thao tác" mơ hồ, không có mốc đo lường thời gian. | CL-TST-02 | KHÔNG KIỂM THỬ ĐƯỢC | Minor | 1 | Đo lường cụ thể: "Thời gian phản hồi thao tác thông thường không quá 2 giây." |
| 10 | NFR-02 | Yêu cầu "hoạt động 100% thời gian và không bao giờ xảy ra lỗi" là bất khả thi trong thực tế. | CL-FES-01 | KHÔNG KHẢ THI | Major | 1 | Điều chỉnh thành: "Độ sẵn sàng (uptime) đạt 99.5%, có thông báo trước thời gian bảo trì." |
| 11 | UC-03 so với FR-05.1 & 1.2 | Bước 3 của UC-03 có "nhập mã giảm giá", nhưng toàn bộ tài liệu không có yêu cầu nào mô tả tính năng này. | CL-MIS-02 | THIẾU | Minor | 2 | Bổ sung đặc tả tính năng mã giảm giá hoặc loại bỏ bước này khỏi ca sử dụng UC-03. |
| 12 | Trang bìa/Thông tin tài liệu | Mục Ngày: "……/……/20……" và trạng thái phê duyệt còn để trống, chưa hoàn thiện. | CL-DOC-01 | THIẾU | Minor | 1 | Điền đầy đủ ngày phát hành và chuyển trạng thái từ 'Bản nháp' sang bản chính thức. |

(Thêm dòng nếu cần.)

## Thống kê

| Loại lỗi | Số lượng |
|---|---|
| MƠ HỒ | 1 |
| MÂU THUẪN | 3 |
| THIẾU | 3 |
| KHÔNG KIỂM THỬ ĐƯỢC | 2 |
| KHÔNG KHẢ THI | 1 |
| THUẬT NGỮ | 1 |
| SAI SỐ LIỆU | 1 |
| **Tổng** | **12** |
| Trong đó Major / Minor | 7 Major / 5 Minor |

## Các điểm cần hỏi lại BA (em chưa chắc ý đồ tác giả)

1. Mốc miễn phí vận chuyển chính xác là từ 500.000đ trở lên (>= 500.000$đ) hay trên 500.000đ (> 500.000$đ)? Và phí ngoại thành là 30.000đ hay 35.000đ
2. Đối tượng "Khách hàng thân thiết" (giảm 5%) có phải là "Thành viên VIP" không, hay là một nhóm phân hạng người dùng hoàn toàn mới cần bổ sung logic tích điểm?

## Kết luận review

Đánh dấu một lựa chọn:

- [ ] **Chấp nhận** – tài liệu dùng được ngay
- [ ] **Chấp nhận có điều kiện** – dùng được sau khi sửa các lỗi đã nêu, không cần review lại
- [x] **Review lại** – phải sửa và tổ chức review lần 2

Lý do: Lý do: Tài liệu phiên bản 1.0 có quá nhiều lỗi nghiêm trọng (7 lỗi Major), đặc biệt là xung đột mâu thuẫn trực tiếp giữa các yêu cầu chức năng (FR-01.3 vs Mục 2.2, FR-02.3 vs NFR-03, FR-04.1/FR-04.2 vs Phụ lục A). Những mâu thuẫn này dẫn đến việc lập trình viên triển khai sai logic và kiểm thử viên không có cơ sở xác định đúng/sai.

## Tự đánh giá (3–5 câu)

1. Lần đọc thứ hai (đối chiếu chéo) giúp em tìm thêm được bao nhiêu lỗi? Đó là những loại lỗi nào?
2. Nếu tổ chức review theo nhóm (có Moderator, Author, nhiều Reviewer), em nghĩ những lỗi nào sẽ dễ được phát hiện hơn? Vì sao?
3. Lần sau review tài liệu, em sẽ làm khác đi điều gì?

**Trả lời:**

- **Câu 1:** Lần đọc thứ hai (đối chiếu chéo) giúp em tìm thêm được 5 lỗi, chủ yếu là các lỗi mâu thuẫn, sai số liệu và thuật ngữ (giữa phần mô tả chung, bảng yêu cầu FR và bảng dữ liệu Phụ lục A).
- **Câu 2:** Nếu tổ chức review theo nhóm (có Moderator, Author, nhiều Reviewer), các lỗi MƠ HỒ, MÂU THUẪN và KHÔNG KHẢ THI sẽ dễ được phát hiện nhất vì mỗi vai trò (Dev, Tester, BA) sẽ có góc nhìn và góc thử thách khác nhau đối với từng ràng buộc kỹ thuật.
- **Câu 3:** Lần sau review tài liệu, em sẽ lập bảng đối chiếu trực tiếp các bảng số liệu với nội dung mô tả ngay từ đầu, đồng thời chuẩn bị sẵn checklist các từ khóa dễ gây mơ hồ (như "hợp lý", "nhanh", "an toàn", "trên/từ") để quét nhanh hơn.