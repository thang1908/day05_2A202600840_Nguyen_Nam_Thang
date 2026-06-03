# Thin SPEC Cuối Day 05 — Chatbot hỗ trợ đặt lịch khám bệnh viện

Thin SPEC không phải PRD đầy đủ. Đây là bản cam kết đủ rõ để sáng Day 06 nhóm build ngay.

## 1. Track, product/app và user

**Track:** Healthcare / Hospital service workflow
**Product/app thật:** Chatbot hỗ trợ đặt lịch khám cho bệnh viện
**User cụ thể:** Bệnh nhân lần đầu hoặc người nhà bệnh nhân muốn đặt lịch khám nhưng chưa biết nên chọn chuyên khoa nào.
**Nhóm có phải user thật không? Nếu không, khác ở đâu?** Nhóm có thể đóng vai user self-use nhưng chưa phải user thật thường xuyên của bệnh viện. Khác biệt chính là bệnh nhân thật có áp lực thời gian, lo lắng sức khỏe, thông tin triệu chứng không đầy đủ và có rủi ro cao hơn nếu được hướng dẫn sai.

## 2. Evidence summary

| Evidence                                                                                       | Nguồn                                       | User/pain nói lên điều gì?                                                    | SPEC phải đổi gì?                                                                           |
| ---------------------------------------------------------------------------------------------- | -------------------------------------------- | ---------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| User nói "tôi đau bụng muốn đặt lịch khám" nhưng chưa biết chọn chuyên khoa.     | Self-use / mô phỏng workflow.              | Vấn đề không chỉ là đặt lịch, mà là quyết định nên khám khoa nào. | AI phải hỏi thêm câu làm rõ và gợi ý chuyên khoa, không chỉ hiện form.             |
| Triệu chứng như đau ngực dữ dội, khó thở, ngất có thể là tình huống nguy hiểm. | Test case rủi ro healthcare.                | Nếu bot xử lý như lịch khám thường, hậu quả có thể nghiêm trọng.     | Thêm red-flag path: dừng flow thường, khuyến nghị cấp cứu/liên hệ nhân viên.        |
| User cần biết nhanh slot khám còn trống và được sửa trước khi chốt.               | Self-use / phân tích workflow đặt lịch. | Workflow dài làm user bỏ cuộc hoặc chọn đại.                               | Sau khi gợi ý chuyên khoa, hiển thị 2-3 slot và có bước xác nhận/sửa.               |
| Nhóm chưa có nguồn ngoài nhóm đã kiểm chứng.                                         | Kế hoạch research Day 06.                  | Evidence hiện tại còn yếu, cần kiểm trước demo.                            | Owner research phải phỏng vấn nhanh 2-3 người hoặc lấy review/comment public trước M1. |

## 3. Pain statement

```text
User bệnh nhân lần đầu đang gặp khó ở bước chọn chuyên khoa và khung giờ khám,
vì họ chỉ biết mô tả triệu chứng bằng ngôn ngữ đời thường nhưng hệ thống đặt lịch thường bắt họ tự chọn khoa/ngày/giờ,
dẫn tới chọn sai chuyên khoa, mất thời gian, hoặc bỏ sót tình huống cần hỗ trợ khẩn cấp.
Bằng chứng chính là self-use workflow với case "tôi đau bụng muốn đặt lịch khám" và test rủi ro "đau ngực dữ dội/khó thở".
```

## 4. Build slice

```text
Cho bệnh nhân lần đầu hoặc người nhà bệnh nhân đang muốn đặt lịch khám nhưng chưa biết chọn chuyên khoa,
prototype sẽ dùng AI để hỏi 2-4 câu làm rõ triệu chứng, phát hiện red flag, gợi ý 1-2 chuyên khoa và 2-3 slot khám phù hợp,
tạo ra lịch khám nháp có chuyên khoa, ngày giờ, thông tin liên hệ và ghi chú triệu chứng,
và xử lý failure mode triệu chứng nguy hiểm/mô tả quá mơ hồ bằng cảnh báo, hỏi lại hoặc chuyển sang nhân viên/cấp cứu thay vì đặt lịch thường.
```

## 5. Auto/Aug decision

Chọn một:

- [X] **Augmentation:** AI gợi ý/draft/phân loại, user quyết cuối.
- [ ] **Conditional automation:** AI tự làm trong case hẹp; case mơ hồ/rủi ro chuyển người.
- [ ] **Automation:** AI tự quyết và tự hành động.

**Lý do chọn:** Healthcare có rủi ro cao. AI không nên tự chẩn đoán, tự quyết chuyên khoa hoặc tự chốt lịch khi user chưa xác nhận. AI chỉ hỗ trợ phân loại, hỏi thêm, gợi ý chuyên khoa/slot và tạo lịch nháp.
**Human role:** User là decider cuối; nhân viên bệnh viện là rescuer khi low-confidence/red-flag; nhóm test là reviewer cho failure path.

## 6. Four paths

| Path           | Prototype phải thể hiện gì?                                                                                                                                                 |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Happy          | User nhập triệu chứng không nguy hiểm, AI hỏi thêm 2-3 câu, gợi ý chuyên khoa hợp lý, hiện 2-3 slot, user xác nhận, chatbot tạo lịch nháp.                   |
| Low-confidence | User mô tả quá chung như "tôi thấy mệt", AI không đủ chắc, hỏi thêm hoặc đưa lựa chọn "Nội tổng quát / gặp nhân viên tư vấn" thay vì tự kết luận. |
| Failure        | User nhập red flag như "đau ngực dữ dội và khó thở", chatbot không cho đặt lịch thường, hiển thị cảnh báo liên hệ cấp cứu/nhân viên bệnh viện.       |
| Correction     | User sửa thông tin như đổi từ "đau bụng" sang "đau dạ dày sau ăn" hoặc đổi giờ khám, chatbot cập nhật chuyên khoa/slot và yêu cầu xác nhận lại.       |

## 7. Failure mode nguy hiểm nhất

```text
Nếu user mô tả triệu chứng có dấu hiệu nguy hiểm như đau ngực dữ dội, khó thở, ngất hoặc chảy máu nhiều,
AI có thể hiểu nhầm thành case đặt lịch khám thường,
hậu quả là user bị trì hoãn xử lý y tế khẩn cấp.
Prototype sẽ xử lý bằng red-flag detection, dừng flow đặt lịch thường, hiển thị thông báo liên hệ cấp cứu/nhân viên bệnh viện, và không tạo lịch tự động.
Owner kiểm thử path này là thành viên phụ trách Test / failure path.
```

## 8. Owner plan cho sáng Day 06

| Thành viên                         | Việc phụ trách                | Bằng chứng cần có trong repo                                                                     |
| ------------------------------------ | -------------------------------- | ---------------------------------------------------------------------------------------------------- |
| Trần Trúc Quỳnh                   | SPEC / tổng hợp nội dung repo | `thin-spec.md`, link prototype, phần giải thích build slice.                                    |
| Nguyễn Xuân Tới                   | Research / evidence              | Ghi chú phỏng vấn nhanh 2-3 người hoặc review/comment public, cập nhật `evidence-pack.md`. |
| Nguyễn Huy Cảnh+Nguyễn Nam Thắng | Prototype                        | Source code chatbot, màn hình chat, flow gợi ý chuyên khoa và slot khám.                      |
| Phạm Thị Bích Ngọc               | Test / failure path              | Test cases happy, low-confidence, failure, correction; screenshot kết quả.                         |
| Nguyễn Tiến Huân                  | Demo script / repo               | Kịch bản demo 3-5 phút, README, ảnh minh họa trước/sau.                                       |
