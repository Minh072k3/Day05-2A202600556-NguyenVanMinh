# Thin SPEC Cuối Day 05 — Smart Bill Splitting

Thin SPEC không phải PRD đầy đủ. Đây là bản cam kết đủ rõ để sáng Day 06 nhóm build ngay.

## 1. Track, product/app và user

**Track:** Tài chính cá nhân / Thanh toán nhóm  
**Product/app thật:** MoMo (Tính năng Chia Tiền / Đòi Nợ)  
**User cụ thể:** Nhóm bạn bè, đồng nghiệp thường xuyên đi ăn chung, trong đó có một người đại diện trả tiền trước (Người Host).  
**Nhóm có phải user thật không? Nếu không, khác ở đâu?** Có, nhóm là user thật, thường xuyên gặp nỗi đau chia tiền sau khi đi ăn quán.  

## 2. Evidence summary

| Evidence | Nguồn | User/pain nói lên điều gì? | SPEC phải đổi gì? |
|---|---|---|---|
| Cầm bill gõ tay từng món quá mệt | Tự trải nghiệm/Phỏng vấn | Host chịu tải lớn, dễ tính nhầm thuế phí. | Giao việc nhập liệu cho AI (Vision LLM đọc bill). |
| Đòi tiền lắt nhắt gây ngại, không minh bạch | Quan sát thực tế | Cần một cách mượt mà để chia đều trách nhiệm. | Giao quyền chọn món lại cho người ăn qua Link tương tác (Crowdsourcing). |

## 3. Pain statement

```text
User [Người Host trả tiền] đang gặp khó ở [bước chia bill đòi tiền sau bữa ăn],
vì [việc cầm hóa đơn giấy, gõ lại từng món, sau đó ngồi hỏi từng người xem ai ăn món nào mất quá nhiều thao tác và dễ tính sai thuế phí],
dẫn tới [sự ngại ngùng khi đòi tiền lẻ hoặc thất thoát tiền bạc vì tính nhầm].
Bằng chứng chính là [hành vi chụp ảnh hóa đơn gửi vào group chat zalo và bắt mọi người tự cộng tiền rồi chuyển khoản].
```

## 4. Build slice

```text
Cho [Người Host] đang [cầm tờ hóa đơn giấy sau bữa ăn],
prototype sẽ dùng AI để [Vision LLM: bóc tách tên món, giá tiền, thuế VAT thành một danh sách số hóa],
tạo ra [một Link tương tác chọn món gửi vào group chat],
và xử lý [vấn đề không biết ai ăn món gì] bằng [cơ chế crowdsourcing: bạn bè bấm vào link, ai ăn gì tự tick vào món đó để hệ thống tự chia tiền].
```

## 5. Auto/Aug decision

Chọn một:
- [x] **Augmentation:** AI bóc tách hóa đơn tạo bản nháp (draft), user và bạn bè tự click chọn món (người quyết định cuối).

**Lý do chọn:** Vấn đề tiền bạc cực kỳ nhạy cảm, AI không thể tự đoán đúng 100% ai ăn món gì. Để bạn bè tự tick chọn (Crowdsourcing) vừa vui vẻ, vừa minh bạch tuyệt đối, xóa bỏ cảm giác "bị đòi nợ".
**Human role:** Reviewer / Decider (Người Host chốt đơn, Bạn bè chọn món).  

## 6. Four paths

| Path | Prototype phải thể hiện gì? |
|---|---|
| Happy | Host up ảnh bill -> AI trả về JSON chuẩn xác 100% -> Hiện UI danh sách -> Host share link -> 3 bạn bè vào tick món -> Bấm "Thanh toán ngay". |
| Low-confidence | Bill có món "Combo Lẩu 4 Người". AI không biết gán cho ai -> Bôi vàng và hiện Popup hỏi: "Món Combo này chia đều cả bàn hay gán cho 1 người?" để Host chốt. |
| Failure | AI đọc nhầm phí "Khăn lạnh/Gửi xe" thành một món ăn độc lập cần có người tick trả tiền, thay vì đưa vào phí chung chia đều. |
| Correction | Host nhấp vào dòng "Khăn lạnh/Gửi xe", chọn "Chuyển thành Phí chung". Hệ thống tự động xóa khỏi danh sách món, cộng vào phí chung và chia đều cho cả bàn. |

## 7. Failure mode nguy hiểm nhất

```text
Nếu user [AI đọc sai đơn giá (ví dụ 150.000đ thành 1.500.000đ) hoặc bạn bè click nhầm món],
AI có thể [tính tiền sai lệch nghiêm trọng],
hậu quả là [Host đòi tiền sai gây cãi vã, mất lòng].
Prototype sẽ xử lý bằng [Luôn hiển thị ảnh bill gốc thu nhỏ bên cạnh để đối chiếu. Cho phép Host bấm vào con số để gõ đè (Override) sửa tay trước khi gửi link, và có quyền Admin "Gỡ tick" nếu bạn bè chọn sai].
Owner kiểm thử path này là Nguyễn Văn Minh.
```

## 8. Owner plan cho sáng Day 06

| Thành viên | Việc phụ trách | Bằng chứng cần có trong repo |
|---|---|---|
| Đoàn Minh Hiếu | Dev AI: Tạo Prompt gửi ảnh bill lên LLM (Vision), nhận về JSON bóc tách. | Script gọi API AI và log kết quả JSON. |
| Lê Nguyễn Minh Quân | Backend: Viết API nhận ảnh, giao tiếp với AI và xử lý logic chia tiền. | Code logic Backend (Node.js/Python). |
| Phạm Hoàng Anh | Dev Web (Frontend): Code UI upload ảnh và giao diện tương tác chọn món. | Code giao diện Web (HTML/React). |
| Nguyễn Dương Hiếu | Research & Test: Làm Slide, thu thập bill thực tế, test độ thông minh của Prompt. | Slide hoàn chỉnh và thư mục Data hóa đơn test. |
| Nguyễn Văn Minh | Research & Test: Đóng vai user test lỗi UI, test logic chia tiền, chuẩn bị Q&A. | Bảng log bug/lỗi tính toán và kịch bản Q&A. |
