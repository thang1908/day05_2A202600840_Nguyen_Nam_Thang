# Evidence Pack — Chatbot hỗ trợ đặt lịch khám bệnh viện

Nộp kèm thin SPEC cuối Day 05.

## 1. Nhóm và track

**Tên nhóm:** Nhóm Chatbot đặt lịch khám bệnh viện  
**Track:** Healthcare / Hospital service workflow  
**Product/app đã chọn:** Chatbot hỗ trợ đặt lịch khám cho bệnh viện  
**Build slice đang nghĩ:** Chatbot hỏi nhanh triệu chứng/mục tiêu đi khám, gợi ý chuyên khoa phù hợp, đề xuất 2-3 khung giờ còn trống và chỉ tạo lịch sau khi user xác nhận.

## 2. Self-use evidence

Nhóm tự mô phỏng workflow đặt lịch khám của một bệnh nhân lần đầu đi khám tại bệnh viện.

| Observation | Screenshot/link | Path liên quan | Điều học được |
|---|---|---|---|
| Khi user chỉ nói "tôi đau bụng muốn đặt lịch khám", hệ thống không nên nhảy thẳng tới đặt lịch vì còn thiếu mức độ đau, thời gian đau, dấu hiệu nguy hiểm và chuyên khoa. | Screenshot self-use sẽ bổ sung trong Day 06 khi prototype chạy. | Low-confidence | Chatbot cần hỏi 2-4 câu phân loại trước khi gợi ý chuyên khoa. |
| User thường không biết nên chọn Nội tổng quát, Tiêu hóa, Tim mạch hay Cấp cứu nếu chỉ mô tả triệu chứng bằng ngôn ngữ đời thường. | Ghi chú self-use từ nhóm. | Happy / Low-confidence | AI hữu ích nhất ở bước chuyển mô tả triệu chứng thành gợi ý chuyên khoa, nhưng không được chẩn đoán bệnh. |
| Nếu user nhập triệu chứng có dấu hiệu nguy hiểm như "đau ngực dữ dội", "khó thở", "ngất", chatbot không nên tiếp tục flow đặt lịch thường. | Test case dự kiến. | Failure | Cần red-flag path: dừng đặt lịch thường và hướng dẫn liên hệ cấp cứu/nhân viên bệnh viện. |
| Sau khi có chuyên khoa, user vẫn cần thông tin slot khám rõ ràng: ngày, giờ, bác sĩ/khoa, chi phí dự kiến nếu có, và cách sửa thông tin. | Ghi chú self-use từ nhóm. | Correction | Prototype phải có bước xác nhận và cho phép sửa chuyên khoa/giờ khám trước khi tạo lịch. |

## 3. User / review / social evidence

Hiện tại nhóm chưa có nguồn ngoài nhóm đã kiểm chứng trực tiếp. Đây là giả định cần kiểm trước checkpoint M1 Day 06.

| Quote / review / observation | Nguồn | User là ai? | Pain/failure mode |
|---|---|---|---|
| "Em không biết triệu chứng này nên khám khoa nào." | Giả định từ bối cảnh bệnh nhân lần đầu; sẽ kiểm bằng phỏng vấn nhanh 2-3 người từng tự đặt lịch khám. | Bệnh nhân lần đầu hoặc người nhà bệnh nhân. | Chọn sai chuyên khoa, mất thời gian chuyển khoa. |
| "Tôi chỉ muốn biết còn lịch khám sáng mai không." | Giả định; sẽ kiểm bằng khảo sát nhanh trong nhóm/lớp. | Người cần đặt lịch nhanh. | Workflow đặt lịch quá dài, hỏi nhiều thông tin trước khi cho biết slot. |
| "Nếu triệu chứng nguy hiểm mà bot vẫn cho đặt lịch bình thường thì rất rủi ro." | Giả định từ phân tích rủi ro healthcare; sẽ kiểm bằng hỏi mentor/giảng viên. | Bệnh nhân có triệu chứng nặng. | Bot bỏ sót tình huống cần cấp cứu hoặc nhân viên hỗ trợ. |

```text
Đây là giả định. Nhóm sẽ kiểm bằng phỏng vấn nhanh 2-3 người đã từng đặt lịch khám online, test self-use trên prototype, và nhờ giảng viên/mentor phản biện red-flag path trước checkpoint M1 Day 06.
```

## 4. Competitor / analog evidence

| App / mô hình tham khảo | Họ xử lý task này thế nào? | Pattern học được | Có áp dụng trong 1 ngày không? |
|---|---|---|---|
| Form đặt lịch bệnh viện truyền thống | User tự chọn chuyên khoa, ngày, giờ, thông tin cá nhân. | Form rõ ràng nhưng không giúp user quyết định nên khám khoa nào. | Có. Dùng form xác nhận cuối flow. |
| Chatbot chăm sóc khách hàng | Thu thập intent, hỏi thêm thông tin, chuyển nhân viên khi không chắc. | Cần có confidence thấp và human handoff. | Có. Dùng trạng thái "AI chưa đủ chắc" và đề nghị nhân viên hỗ trợ. |
| Symptom checker / medical triage assistant | Hỏi triệu chứng theo bước, phân loại mức độ khẩn cấp, nhắc không thay thế bác sĩ. | Không chẩn đoán; chỉ gợi ý hướng đi và cảnh báo red flag. | Có một phần. Chỉ làm rule red-flag + gợi ý chuyên khoa đơn giản. |

## 5. Evidence -> Insight

```text
Evidence nổi bật nhất:
User mô tả nhu cầu khám bằng triệu chứng đời thường, nhưng hệ thống đặt lịch thường yêu cầu họ tự biết chuyên khoa và tự chọn slot.

Insight:
User không chỉ gặp vấn đề "không có chatbot đặt lịch".
Thật ra họ cần hỗ trợ ra quyết định an toàn trước khi đặt lịch: nên khám khoa nào, khi nào cần cấp cứu/nhân viên thật, và thông tin nào phải xác nhận trước khi tạo lịch.

Opportunity:
AI có thể giúp bằng cách biến mô tả triệu chứng thành gợi ý chuyên khoa + slot khám phù hợp, trong khi vẫn kiểm soát rủi ro bằng red-flag detection, low-confidence fallback và bước user xác nhận.
```

## 6. Evidence đổi SPEC như thế nào?

- [x] Đổi user chính.
- [x] Đổi pain statement.
- [x] Đổi build slice.
- [x] Đổi Auto/Aug decision.
- [x] Đổi 4 paths.
- [x] Đổi failure mode.
- [x] Đổi owner/test plan.

Ghi rõ 1-2 thay đổi quan trọng:

```text
Trước evidence, nhóm định build chatbot đặt lịch khám tổng quát: hỏi thông tin cá nhân, chọn bác sĩ, chọn ngày giờ, lưu lịch.

Sau evidence, nhóm đổi thành build một slice hẹp hơn:
Bệnh nhân lần đầu mô tả triệu chứng -> AI hỏi thêm 2-4 câu -> gợi ý chuyên khoa và 2-3 slot khám -> user xác nhận -> tạo lịch nháp.

Lý do:
Rủi ro lớn nhất không nằm ở thao tác đặt lịch, mà ở bước user không biết chọn chuyên khoa và AI có thể xử lý sai triệu chứng nguy hiểm. Slice mới vừa nhỏ hơn để demo trong 1 ngày, vừa thể hiện rõ giá trị AI và failure path.
```
