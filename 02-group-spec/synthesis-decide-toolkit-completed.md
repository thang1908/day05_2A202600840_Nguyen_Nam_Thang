# Toolkit — Từ Evidence Đến Build Slice

Dùng sau khi nhóm đã có evidence. Mục tiêu là chốt một build slice đủ nhỏ cho Day 06.

## 1. Gom evidence thành cụm

Gom theo workflow/pain, không gom theo tên feature.

- **Không biết chọn chuyên khoa:** User mô tả "đau bụng", "đau đầu", "khó thở" nhưng không biết nên khám khoa nào.
- **Workflow đặt lịch dài:** User muốn biết nhanh còn lịch khám phù hợp không, nhưng thường phải điền nhiều trường trước.
- **Rủi ro triệu chứng nguy hiểm:** Nếu có dấu hiệu cấp cứu, chatbot không được tiếp tục đặt lịch thường như một case bình thường.
- **Cần quyền sửa/xác nhận:** User có thể mô tả thiếu hoặc sai thông tin, nên cần sửa triệu chứng, chuyên khoa, ngày giờ trước khi chốt.
- **Cần niềm tin:** User cần biết AI chỉ gợi ý hướng khám, không chẩn đoán bệnh và không thay thế bác sĩ.

## 2. Viết insight

```text
User bệnh nhân lần đầu không chỉ cần một form đặt lịch nhanh.
Họ thật ra cần được hỗ trợ ra quyết định an toàn trước khi đặt lịch,
vì evidence/self-use cho thấy họ thường không biết chọn chuyên khoa từ triệu chứng đời thường, trong khi healthcare có rủi ro nếu bỏ sót dấu hiệu nguy hiểm.
```

## 3. Viết opportunity

```text
Cơ hội là dùng AI để augment bước phân loại nhu cầu khám:
AI hỏi thêm vài câu, gợi ý chuyên khoa và slot khám phù hợp,
giúp user đi tới lịch khám cụ thể nhanh hơn,
trong khi vẫn kiểm soát rủi ro bằng red-flag fallback, low-confidence handoff và bước xác nhận của user.
```

## 4. Chọn build slice

| Câu hỏi | Đạt khi |
|---|---|
| User cụ thể chưa? | Có. Bệnh nhân lần đầu hoặc người nhà bệnh nhân muốn đặt lịch khám nhưng chưa biết chuyên khoa. |
| Task đủ hẹp chưa? | Có. Chỉ xử lý flow mô tả triệu chứng -> gợi ý chuyên khoa -> chọn slot -> xác nhận lịch nháp. |
| AI decision rõ chưa? | Có. AI quyết định mức confidence, gợi ý chuyên khoa, phát hiện red flag, đề xuất câu hỏi tiếp theo. |
| Failure path rõ chưa? | Có. Triệu chứng nguy hiểm hoặc mô tả quá mơ hồ sẽ không cho đặt lịch thường. |
| Có evidence không? | Có self-use và giả định cần kiểm chứng. Nguồn ngoài nhóm sẽ lấy bằng phỏng vấn nhanh trước M1 Day 06. |

## 5. Quyết định: giữ, giảm scope, hay đổi hướng?

| Tình huống | Quyết định |
|---|---|
| Evidence yếu, user mơ hồ | Giữ scope hẹp và ghi rõ cần kiểm bằng phỏng vấn nhanh 2-3 người trước M1. |
| Ý tưởng quá rộng | Giảm từ "chatbot bệnh viện đầy đủ" xuống "gợi ý chuyên khoa + đặt lịch nháp". |
| AI không cần thiết | AI cần ở bước hiểu mô tả triệu chứng tự nhiên và sinh câu hỏi làm rõ; form/rule xử lý bước xác nhận. |
| Rủi ro cao | Chọn augmentation/conditional automation, không automation hoàn toàn. |
| Không demo được trong 1 ngày | Đưa login, thanh toán, hồ sơ bệnh án, tích hợp HIS thật vào backlog. |

## 6. Câu chốt cuối

```text
Dựa trên evidence self-use và giả định cần kiểm chứng,
nhóm sẽ build prototype chatbot gợi ý chuyên khoa và tạo lịch khám nháp,
cho bệnh nhân lần đầu hoặc người nhà đang không biết nên chọn khoa nào,
để giải quyết pain chọn sai chuyên khoa/đặt lịch quá chậm,
bằng cách AI augment bước hỏi triệu chứng, gợi ý chuyên khoa, đề xuất slot khám,
và sẽ test failure path triệu chứng nguy hiểm hoặc mô tả quá mơ hồ.
```

## 7. Backlog

Những thứ không build trong Day 06:

- Tích hợp hệ thống lịch khám thật của bệnh viện.
- Tài khoản bệnh nhân, đăng nhập, xác thực OTP.
- Thanh toán cọc/viện phí.
- Chọn bác sĩ cụ thể theo lịch trực thật.
- Lưu hồ sơ bệnh án dài hạn.
- Chẩn đoán bệnh hoặc kê đơn thuốc.
- Đa ngôn ngữ.
- Dashboard cho nhân viên bệnh viện.
- Tối ưu mô hình bằng dữ liệu y khoa thật.
