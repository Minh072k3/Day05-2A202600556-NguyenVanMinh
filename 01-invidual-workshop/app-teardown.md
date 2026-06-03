# Workshop — Mổ App AI Thật: MoMo Moni

## 1. Sản phẩm được chọn

**Sản phẩm:** MoMo — Moni
**AI feature:** Trợ thủ tài chính cá nhân, phân tích chi tiêu, chatbot trong app
**Cách truy cập:** Mở app MoMo → tìm kiếm “Moni”

MoMo định vị sản phẩm là “Trợ Thủ Tài Chính với AI”, trong đó tính năng quản lý chi tiêu có các promise như tự động phân loại nhiều giao dịch, báo cáo chi tiêu chi tiết, dễ hiểu và được hỗ trợ bởi trợ thủ AI thông minh. Moni cũng được MoMo mô tả là trợ lý AI đóng vai trò như “người quản gia” tài chính cá nhân, giúp người dùng quản lý chi tiêu hiệu quả và tối ưu trải nghiệm trong nền tảng.

## 2. Promise vs reality

### Product hứa gì?

Moni hứa giúp người dùng hỏi và hiểu các thông tin tài chính cá nhân bằng ngôn ngữ tự nhiên, ví dụ như tổng chi tiêu, giao dịch lớn nhất, giao dịch gần nhất, người nhận tiền, danh mục chi tiêu.

### User nào được hứa sẽ được giúp?

Người dùng MoMo có nhiều giao dịch và muốn xem lại dòng tiền, kiểm tra chi tiêu, hiểu tiền đã đi đâu mà không phải tự lọc thủ công trong lịch sử giao dịch.

### Tôi kỳ vọng AI làm được task nào?

Tôi kỳ vọng Moni có thể:

* Tính tổng chi tiêu theo thời gian.
* Tìm giao dịch lớn nhất/gần nhất.
* Tìm lại giao dịch theo số tiền.
* Hiểu câu hỏi follow-up dựa trên các giao dịch vừa hiển thị.
* Cho phép kiểm chứng hoặc sửa khi kết quả sai.

### Reality khi dùng thật

Moni có ích ở các câu hỏi tổng hợp. Ví dụ, khi hỏi “năm nay tôi đã tiêu bao nhiêu tiền”, Moni trả lời được tổng chi tiêu từ 2026-01-01 đến 2026-06-03 là 38.812.282đ với 165 giao dịch, trung bình 252.027đ/ngày. Khi hỏi “giao dịch nào lớn nhất”, Moni trả lời được giao dịch lớn nhất là 3.149.000đ, ngày 2026-04-18, danh mục Hóa đơn, ghi chú Thanh toán - Vay Nhanh.

Tuy nhiên, điểm gãy xuất hiện ở follow-up query. Moni từng liệt kê giao dịch gần nhất có khoản 19.000đ Apple Services lúc 20:41:47, nhưng khi tôi hỏi tiếp “tìm giao dịch 19k”, Moni lại trả lời không tìm được giao dịch nào với số tiền 19.000đ trong khoảng thời gian từ 2026-06-01 đến 2026-06-03.

Cảm giác sau khi dùng: **có ích nhưng cần kiểm chứng**. Moni trả lời được một số câu, nhưng user vẫn cần tự kiểm tra lại vì có trường hợp kết quả mâu thuẫn.

## 3. Bốn paths

| Path           | Quan sát thực tế                                                                                                                                                                                         | Đánh giá                                                                                                    |
| -------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| Happy          | User hỏi “năm nay tôi đã tiêu bao nhiêu tiền”, Moni trả lời tổng tiền, số giao dịch, trung bình/ngày. User hỏi “giao dịch nào lớn nhất”, Moni trả lời số tiền, ngày, danh mục, ghi chú.                  | Hoạt động tốt với câu hỏi tổng hợp rõ ràng.                                                                 |
| Low-confidence | User hỏi “tôi chuyển tiền cho ai nhiều nhất”, Moni trả lời tổng số lần chuyển và tổng tiền, nhưng nói chưa xác định được người nhận nhiều nhất, rồi hỏi user có muốn liệt kê chi tiết từng người không.  | Có hỏi lại thay vì bịa kết quả. Đây là điểm tích cực.                                                       |
| Failure        | Moni vừa liệt kê giao dịch 19.000đ Apple Services trong danh sách giao dịch gần nhất, nhưng khi user hỏi “tìm giao dịch 19k”, Moni lại nói không tìm thấy giao dịch 19.000đ trong cùng khoảng thời gian. | Gãy ở context/retrieval. Câu trả lời sau mâu thuẫn với câu trả lời trước.                                   |
| Correction     | Khi user bấm “Không” ở câu “Câu trả lời có hữu ích không?”, Moni hỏi lý do chưa hài lòng.                                                                                                                | Có feedback path, nhưng chưa có correction path thật để tìm lại, sửa filter hoặc dùng kết quả vừa hiển thị. |

## 4. Finding thành quyết định product

Khi user hỏi lại về một giao dịch vừa được Moni liệt kê, AI không giữ/không dùng đúng context của kết quả trước đó, dẫn đến việc Moni vừa hiển thị giao dịch 19.000đ nhưng sau đó lại nói không tìm thấy giao dịch 19.000đ.

Hậu quả là user thấy Moni có ích nhưng cần kiểm chứng, vì các câu trả lời tài chính có thể mâu thuẫn. Với sản phẩm tài chính cá nhân, đây là vấn đề lớn vì user cần độ tin cậy cao khi kiểm tra tiền, giao dịch và chi tiêu.

Lỗi thuộc layer **Data-tool + Context Memory + UX Recovery**.

Nên sửa bằng:

* Lưu context các giao dịch vừa được Moni trả về trong phiên trò chuyện.
* Mỗi giao dịch được hiển thị cần có transaction reference nội bộ để AI có thể truy xuất lại.
* Khi user hỏi “tìm giao dịch 19k”, Moni nên hiểu đây có thể là follow-up từ giao dịch 19.000đ vừa hiển thị.
* Nếu không chắc, Moni nên hỏi lại: “Bạn muốn tìm trong các giao dịch vừa hiển thị hay toàn bộ lịch sử?”
* Khi user bấm “Không hữu ích”, Moni nên đưa các hành động sửa cụ thể như “Tìm lại”, “Đổi khoảng thời gian”, “Tìm trong kết quả vừa hiển thị”, “Báo kết quả sai”.

## 5. Sketch as-is / to-be

### As-is

User mở MoMo
→ Tìm kiếm “Moni”
→ Moni chào: “Chào Minh, Moni có thể giúp gì cho bạn?”
→ User hỏi: “năm nay tôi đã tiêu bao nhiêu tiền”
→ Moni trả lời tổng chi tiêu, số giao dịch, trung bình/ngày
→ User hỏi: “tìm ngày giao dịch gần nhất”
→ Moni liệt kê các giao dịch gần nhất, trong đó có giao dịch 19.000đ Apple Services
→ User hỏi tiếp: “tìm giao dịch 19k”
→ Moni trả lời không tìm được giao dịch 19.000đ
→ **Điểm gãy:** câu trả lời mâu thuẫn với chính dữ liệu Moni vừa hiển thị
→ User bấm “Không”
→ Moni hỏi lý do chưa hài lòng
→ **Điểm gãy tiếp:** feedback chưa dẫn đến hành động sửa cụ thể

### To-be

User mở MoMo
→ Tìm kiếm “Moni”
→ User hỏi: “tìm ngày giao dịch gần nhất”
→ Moni liệt kê các giao dịch gần nhất dưới dạng card có transaction reference
→ User hỏi tiếp: “tìm giao dịch 19k”
→ Moni match với giao dịch 19.000đ Apple Services vừa hiển thị
→ Moni trả lời: “Mình tìm thấy giao dịch 19.000đ Apple Services lúc 20:41:47 ngày 2026-06-01. Bạn muốn xem chi tiết hay tìm thêm giao dịch 19.000đ khác?”
→ Nếu không chắc, Moni hỏi: “Bạn muốn tìm trong kết quả vừa hiển thị hay toàn bộ lịch sử MoMo?”
→ Nếu user bấm “Không hữu ích”, Moni hiện các option:

1. Tìm lại trong khoảng thời gian khác
2. Tìm trong kết quả vừa hiển thị
3. Tìm theo người nhận/nội dung
4. Báo kết quả sai

## 6. SPEC change

Bổ sung requirement vào SPEC:

**Moni phải hỗ trợ follow-up query dựa trên các giao dịch vừa trả về trong cùng cuộc trò chuyện. Mỗi giao dịch trong câu trả lời cần có transaction reference để AI có thể truy xuất lại khi user hỏi bằng số tiền, người nhận, thời gian hoặc nội dung giao dịch. Khi kết quả không chắc chắn, Moni phải hỏi lại phạm vi tìm kiếm thay vì trả lời phủ định ngay.**
