# Evidence Pack — Smart Bill Splitting

Nộp kèm thin SPEC cuối Day 05.

## 1. Nhóm và track

**Tên nhóm:** Nhóm [Điền Tên Nhóm]
**Track:** Tài chính cá nhân / Thanh toán nhóm
**Product/app đã chọn:** MoMo (Tính năng Chia tiền nhóm)
**Build slice đang nghĩ:** Dùng Vision AI bóc tách hóa đơn giấy và tạo link chọn món tương tác (Crowdsourcing) để chia tiền.

## 2. Self-use evidence

Nhóm tự dùng app/workflow và ghi lại điểm gãy.

| Observation | Screenshot/link | Path liên quan | Điều học được |
|---|---|---|---|
| Tính năng chia tiền hiện tại của MoMo ép người tạo phải tự gõ số tiền cho từng người. | [Chèn Ảnh chụp màn hình chia tiền MoMo] | Failure | Quá nhiều ma sát (friction) ở khâu nhập liệu. Người trả tiền (chủ chi) chịu toàn bộ gánh nặng (cognitive load) khi phải dò hỏi ai ăn gì. |
| Nếu chỉ chia đều (chia theo tỷ lệ) thì lại gây bất công cho người ăn ít/ăn nhiều. | [Chèn Ảnh chia tiền đều trên MoMo] | Failure | Nhu cầu chia chi tiết theo món là rất lớn, nhưng rào cản thao tác tay làm user bỏ cuộc. |

## 3. User / review / social evidence

| Quote / review / observation | Nguồn | User là ai? | Pain/failure mode |
|---|---|---|---|
| "Đi ăn đông mà chia tiền lẻ tẻ mệt mỏi thực sự, chụp cái bill ném vào Zalo tự cộng tay cho nhanh." | Quan sát thực tế | Nhóm bạn trẻ/Dân văn phòng | Quy trình đòi tiền quá thủ công, dễ cộng sai sót tiền VAT, phí dịch vụ. |
| "Thằng bạn nhắc trả tiền mà mình lười xem lại bill xem nợ bao nhiêu." | Phỏng vấn nhanh user | Người bị đòi tiền | Người nợ thiếu chủ động vì không có UI trực quan để xác nhận món ăn của mình. |

## 4. Competitor / analog evidence

| App / mô hình tham khảo | Họ xử lý task này thế nào? | Pattern học được | Có áp dụng trong 1 ngày không? |
|---|---|---|---|
| Splitwise | Cho phép gõ từng món và gán người, nhưng vẫn là nhập tay toàn bộ. | Rất chi tiết nhưng UX nhập liệu kém và mệt mỏi. | Áp dụng concept gán tên (tagging) nhưng sẽ làm mượt hơn bằng AI. |

## 5. Evidence -> Insight

**Evidence nổi bật nhất:**
User thà vứt ảnh hóa đơn vào group chat tự cộng tay còn hơn là mở tính năng Chia Tiền của MoMo để ngồi gõ lại.

**Insight:**
User không chỉ gặp [khó khăn trong việc cộng trừ nhân chia].
Thật ra họ cần [một trải nghiệm chia tiền tự động, minh bạch và giảm thiểu gánh nặng cho người chủ chi],
vì [việc hỏi từng người "Mày ăn món gì" làm mất vui cuộc đi chơi và dễ sai sót].

**Opportunity:**
AI có thể giúp bằng cách [augment - Vision LLM đọc tờ hóa đơn thành danh sách số hóa], kết hợp với UI tương tác để [nhóm bạn tự click chọn món mình ăn].

## 6. Evidence đổi SPEC như thế nào?

- [x] Đổi build slice.
- [x] Đổi Auto/Aug decision.

Ghi rõ 1-2 thay đổi quan trọng:

Trước evidence, nhóm định: Dùng tính năng chia đều của MoMo.
Sau evidence, nhóm đổi thành: Dùng Vision LLM bóc tách bill và tạo Link tương tác chọn món.
Lý do: Để AI làm phần khó (đọc bill nhăn nheo, tính VAT) và giao phần nhạy cảm (quyết định ai ăn món gì) cho chính người dùng tự chọn qua link (Crowdsourcing), đảm bảo tính minh bạch 100% và giảm áp lực cho Host.
