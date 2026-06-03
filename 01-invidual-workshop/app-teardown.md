# Workshop — Mổ App AI Thật

**Thời gian:** 35-45 phút  
**Hình thức:** cá nhân trước, chia sẻ theo nhóm sau  
**Output:** finding note + sketch `as-is / to-be`

Mục tiêu không phải chấm "UI đẹp hay xấu". Mục tiêu là dùng sản phẩm thật như một bài needfinding: tìm chỗ product gãy trong workflow thật, rồi viết finding đó thành quyết định product.

## 1. Chọn một sản phẩm để dùng thử

| Sản phẩm | AI feature | Cách truy cập |
|---|---|---|
| **MoMo — Moni** | **Trợ thủ tài chính, phân tích chi tiêu, chatbot** | **App MoMo** |
| Vietnam Airlines — NEO | Chatbot hỗ trợ vé, hành lý, khiếu nại | Website/Zalo VNA |
| V-App — V-AI | Trợ lý voice/text, gợi ý theo ngữ cảnh | App V-App |

*Sản phẩm được chọn để trải nghiệm:* **MoMo — Moni** (Trợ lý AI đóng vai trò như “người quản gia” tài chính cá nhân, giúp người dùng quản lý chi tiêu hiệu quả và tối ưu trải nghiệm trong nền tảng).

## 2. Dùng thử: promise vs reality

### Ghi nhanh:

* **Product hứa gì?**  
  Moni hứa giúp người dùng hỏi và hiểu các thông tin tài chính cá nhân bằng ngôn ngữ tự nhiên, ví dụ như tổng chi tiêu, giao dịch lớn nhất, giao dịch gần nhất, người nhận tiền, danh mục chi tiêu.
* **User nào được hứa sẽ được giúp?**  
  Người dùng MoMo có nhiều giao dịch và muốn xem lại dòng tiền, kiểm tra chi tiêu, hiểu tiền đã đi đâu mà không phải tự lọc thủ công trong lịch sử giao dịch.
* **Bạn kỳ vọng AI làm được task nào?**  
  Tự động tính tổng chi tiêu theo thời gian, tìm giao dịch lớn nhất/gần nhất, tìm lại giao dịch theo số tiền, hiểu câu hỏi follow-up dựa trên các giao dịch vừa hiển thị, và cho phép kiểm chứng hoặc sửa khi kết quả sai.
* **Khi dùng thật, điểm gãy xuất hiện ở đâu?**  
  Gãy ở follow-up query liên quan đến ngữ cảnh (context/retrieval). Moni vừa liệt kê giao dịch gần nhất có khoản 19.000đ Apple Services lúc 20:41:47 ngày 2026-06-01, nhưng khi hỏi tiếp “tìm giao dịch 19k”, Moni lại báo không tìm thấy giao dịch nào trong khoảng thời gian từ 2026-06-01 đến 2026-06-03. Cảm giác sau khi dùng: có ích nhưng cần kiểm chứng lại vì kết quả trả về mâu thuẫn.

### Evidence cần có:

* **Prompt/input đã thử & Hành vi quan sát được:** 
  1. Hỏi: “năm nay tôi đã tiêu bao nhiêu tiền” $\rightarrow$ Trả lời: 38.812.282đ với 165 giao dịch, trung bình 252.027đ/ngày.
  2. Hỏi: “giao dịch nào lớn nhất” $\rightarrow$ Trả lời: 3.149.000đ, ngày 2026-04-18, danh mục Hóa đơn, ghi chú Thanh toán - Vay Nhanh.
  3. Hỏi: “tìm ngày giao dịch gần nhất” $\rightarrow$ Hiển thị danh sách, có giao dịch 19.000đ Apple Services lúc 20:41:47 ngày 2026-06-01.
  4. Hỏi: “tìm giao dịch 19k” $\rightarrow$ Trả lời: Không tìm thấy giao dịch nào với số tiền 19.000đ trong khoảng thời gian từ 2026-06-01 đến 2026-06-03.
* **Nhận xét điểm gãy:** Câu trả lời sau mâu thuẫn trực tiếp với dữ liệu do chính AI hiển thị ngay phía trên. Phản hồi feedback khi chọn "Không hữu ích" chỉ là một câu hỏi khảo sát lý do chung chung, không đi kèm hành động sửa lỗi cụ thể cho user.

## 3. Vẽ 4 paths

| Path | Câu hỏi cần trả lời | Quan sát thực tế & Đánh giá trên Moni |
|---|---|---|
| **Happy** | Khi AI đúng và tự tin, user thấy gì? | User hỏi “năm nay tôi đã tiêu bao nhiêu tiền” hoặc “giao dịch nào lớn nhất”, Moni phản hồi chính xác và chi tiết (số tiền, ngày, danh mục, ghi chú). Hoạt động tốt với câu hỏi tổng hợp rõ ràng. |
| **Low-confidence** | Khi AI không chắc, hệ thống có hỏi lại, show options hoặc chuyển người không? | User hỏi “tôi chuyển tiền cho ai nhiều nhất”, Moni trả lời tổng số lần chuyển/tiền nhưng nói chưa xác định được người nhận nhiều nhất, rồi hỏi user có muốn liệt kê chi tiết từng người không. Có hỏi lại thay vì bịa kết quả. |
| **Failure** | Khi AI sai, user biết bằng cách nào và sửa thế nào? | Moni vừa liệt kê giao dịch 19.000đ Apple Services nhưng khi hỏi ngay sau đó “tìm giao dịch 19k” lại báo không tìm thấy. User phát hiện lỗi do dữ liệu mâu thuẫn trực tiếp trên màn hình chat, nhưng không có cách nào tự sửa filter/truy vấn. |
| **Correction** | Khi user sửa, correction có được lưu/log/học lại không hay biến mất? | Khi user bấm “Không” ở phần đánh giá độ hữu ích, Moni hỏi lý do chưa hài lòng để ghi nhận log, nhưng chưa cung cấp correction path thực tế (như sửa lại filter, khoanh vùng tìm kiếm hoặc gợi ý hành động cụ thể để tìm lại). |

## 4. Viết finding thành quyết định

Không viết:
```text
Bot ngu, trả lời sai.
```

Viết:
```text
Khi user hỏi lại về một giao dịch vừa được Moni liệt kê ở câu trả lời ngay trước đó,
AI không lưu giữ/không sử dụng đúng context của kết quả trước,
hậu quả là Moni trả lời phủ định không tìm thấy giao dịch đó, gây ra sự mâu thuẫn dữ liệu và làm giảm độ tin cậy của trợ lý tài chính.
Lỗi thuộc layer Data-tool + Context Memory + UX Recovery.
Nên sửa bằng:
- Thiết lập lưu context các giao dịch vừa được Moni trả về trong phiên trò chuyện hiện tại.
- Gán transaction reference nội bộ cho mỗi giao dịch được hiển thị để AI có thể truy xuất ngược lại khi user hỏi bằng số tiền, tên người nhận, thời gian hoặc nội dung.
- Thiết lập low-confidence path: Khi user hỏi “tìm giao dịch 19k”, AI nên hiểu đây có thể là follow-up từ kết quả trước. Nếu không chắc chắn, hệ thống nên hỏi lại để xác nhận phạm vi: “Bạn muốn tìm trong các giao dịch vừa hiển thị hay trên toàn bộ lịch sử giao dịch?” thay vì trả lời phủ định ngay lập tức.
- UX Recovery: Khi user bấm “Không hữu ích”, hiển thị các nút hành động nhanh hỗ trợ sửa lỗi: “Tìm lại trong khoảng thời gian khác”, “Tìm trong kết quả vừa hiển thị”, “Tìm theo nội dung/người nhận”, “Báo cáo kết quả sai”.
```

## 5. Sketch as-is / to-be

Vẽ 2 cột:
* **As-is:** flow hiện tại, đánh dấu điểm gãy.
* **To-be:** flow đề xuất, đánh dấu path đã sửa.

### Luồng As-is (Hiện tại)
```text
User mở MoMo -> Tìm kiếm "Moni" -> Moni chào
  -> User hỏi: "tìm ngày giao dịch gần nhất"
  -> Moni hiển thị danh sách giao dịch gần nhất (trong đó có giao dịch 19.000đ Apple Services)
  -> User hỏi tiếp: "tìm giao dịch 19k"
  -> Moni xử lý độc lập, không mang theo context trước đó 
  -> Moni trả lời: "Không tìm thấy giao dịch nào 19.000đ từ 2026-06-01 đến 2026-06-03" (ĐIỂM GÃY - Dữ liệu mâu thuẫn)
  -> User bấm "Không hữu ích"
  -> Moni chỉ hỏi lý do khảo sát (ĐIỂM GÃY - Không hỗ trợ khắc phục)
```

### Luồng To-be (Đề xuất)
```text
User mở MoMo -> Tìm kiếm "Moni" -> Moni chào
  -> User hỏi: "tìm ngày giao dịch gần nhất"
  -> Moni hiển thị danh sách dưới dạng các Thẻ giao dịch (có gắn kèm Transaction Reference)
  -> User hỏi tiếp: "tìm giao dịch 19k"
  -> Moni nhận diện query là follow-up và kiểm tra trong Context Memory
  -> Moni khớp thông tin (19k = 19.000đ Apple Services)
  -> Moni phản hồi: "Mình tìm thấy giao dịch 19.000đ Apple Services lúc 20:41:47 ngày 2026-06-01. Bạn muốn xem chi tiết hay tìm giao dịch 19.000đ khác?" (PATH ĐÃ SỬA)
  * Nếu không chắc chắn: Moni hỏi lại: "Bạn muốn tìm trong kết quả vừa hiển thị hay trên toàn bộ lịch sử MoMo?"
  * Nếu user bấm "Không hữu ích": Moni hiển thị menu sửa lỗi nhanh (Tìm lại theo thời gian/Nội dung/Báo lỗi).
```

## 6. Tự kiểm trước khi nộp

- [x] Có ít nhất 1 screenshot hoặc observation cụ thể.
- [x] Có đủ 4 paths hoặc nói rõ path nào chưa có trong product.
- [x] Finding được viết thành product decision, không chỉ là nhận xét.
- [x] Sketch có as-is và to-be.
- [x] Có một câu nói rõ finding này sẽ đổi gì trong SPEC.

> **Quyết định thay đổi SPEC:** Bổ sung yêu cầu kỹ thuật vào SPEC: Moni bắt buộc phải lưu context của các giao dịch đã trả về trong phiên hội thoại và hỗ trợ follow-up query dựa trên context này qua transaction reference. Khi truy vấn không chắc chắn, hệ thống phải kích hoạt low-confidence path hỏi lại phạm vi thay vì báo không tìm thấy; khi user phản hồi không hữu ích, phải kích hoạt UX recovery bằng menu hành động khắc phục lỗi trực tiếp.
