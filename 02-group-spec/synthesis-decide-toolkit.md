# Toolkit — Từ Evidence Đến Build Slice

## 1. Gom evidence thành cụm

- "Nhập liệu tay quá mệt mỏi cho người chủ chi."
- "Chia đều thì bất công, mà chia chi tiết thì phiền phức."
- "Dễ tính sai tiền VAT và phí phục vụ."
- "Ngại nhắn tin đòi tiền lắt nhắt."

## 2. Viết insight

User [nhóm bạn trẻ/đồng nghiệp đi ăn chung] không chỉ cần [một công cụ máy tính để cộng trừ].
Họ thật ra cần [một trải nghiệm chia tiền tự động, minh bạch và vui vẻ],
vì [việc chia bill hiện tại đổ dồn gánh nặng thao tác tay cho người trả tiền trước, gây tâm lý ngại ngùng].

## 3. Viết opportunity

Cơ hội là dùng AI để [Vision AI: bóc tách hóa đơn thành danh sách món ăn số hóa],
giúp user [tạo ra một link chia sẻ để bạn bè tự vào click chọn món mình ăn],
trong khi vẫn kiểm soát [rủi ro tranh cãi bằng cách để host review tổng bill trước khi đòi tiền].

## 4. Chọn build slice

Build slice tốt phải qua 5 câu hỏi:

| Câu hỏi | Đạt khi | Đánh giá của nhóm |
|---|---|---|
| User cụ thể chưa? | Nói được ai dùng, trong bối cảnh nào. | Đạt. Nhóm bạn bè/đồng nghiệp sau khi đi ăn quán chung. |
| Task đủ hẹp chưa? | Demo được trong 3-5 phút. | Đạt. Chụp bill -> Ra link -> Bạn bè Click chọn -> Chốt thanh toán. |
| AI decision rõ chưa? | AI gợi ý/tự làm một việc cụ thể. | Đạt. AI Augment (Bóc tách danh sách món từ ảnh bill và tự chia tiền theo lựa chọn của user). |
| Failure path rõ chưa? | Có một case AI không chắc hoặc sai để test. | Đạt. Case hóa đơn có "Combo chung" không rõ người nhận, AI đọc sai giá. |
| Có evidence không? | Có bằng chứng từ self-use/review. | Đạt. Nỗi đau này cực kỳ phổ biến và dễ dàng quan sát trên bàn nhậu/bàn ăn. |

## 5. Quyết định: giữ, giảm scope, hay đổi hướng?

| Tình huống | Quyết định |
|---|---|
| Giữ domain, cắt xuống một flow. | **Chốt:** Chỉ demo flow bóc tách 1 ảnh bill có sẵn và luồng UI user click chọn món. Bỏ qua việc tích hợp trực tiếp API cổng thanh toán của ngân hàng/MoMo thực tế (chỉ làm màn hình giả lập chốt bill). |

## 6. Câu chốt cuối

Dựa trên [nỗi đau nhập tay bill mất thời gian],
nhóm sẽ build [prototype Smart Bill Splitting bằng Vision LLM],
cho [nhóm bạn bè đi ăn chung],
để giải quyết [gánh nặng chia tiền của người host],
bằng cách AI [bóc tách tên món, giá tiền, thuế VAT thành link chọn món tương tác],
và sẽ test failure path [AI đọc nhầm phí "Gửi xe" thành một món ăn, Host phải gán nó thành Phí chung].

## 7. Backlog

Những thứ **không build trong Day 06**:
- Tích hợp cổng thanh toán ngân hàng thật (chỉ giả lập UI).
- Quản lý lịch sử nợ nần dài hạn (chỉ giải quyết xong 1 bill là đóng).
- Nhận diện bill ngoại tệ và tự động quy đổi tỷ giá.
