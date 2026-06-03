# Workshop — Mổ App AI Thật

# Product

**NEO – Vietnam Airlines Chatbot**

---

# 1. Promise vs Reality

## Product Promise

NEO là trợ lý ảo hỗ trợ khách hàng 24/7 về:

* Tra cứu chuyến bay
* Tra cứu giá vé
* Hành lý
* Hoàn/đổi vé
* Thủ tục hàng không
* Hỗ trợ khách hàng

Người dùng có thể giao tiếp bằng ngôn ngữ tự nhiên thay vì tìm kiếm thông tin thủ công trên website.

---

## User Expectation

Người dùng kỳ vọng:

* Nhận thông tin nhanh chóng.
* Hoàn thành tác vụ qua hội thoại.
* Được hỗ trợ bởi nhân viên khi chatbot không xử lý được.
* Không phải thực hiện quá nhiều bước xác nhận.

---

# 2. Evidence

## Case 1 – Tra cứu hành lý xách tay

### Input

> Hành lý xách tay bao nhiêu kg?

### Observation

NEO trả lời chi tiết:

* Theo hạng vé
* Theo hành trình
* Theo loại máy bay
* Có lưu ý về phụ kiện đi kèm

### Result

Task hoàn thành ngay trong 1 lượt hỏi đáp.

### Assessment

✅ Thành công

---

## Case 2 – Chuyển sang nhân viên hỗ trợ

### Input

> Tôi muốn nói chuyện với nhân viên.

### Observation

NEO phản hồi:

> Xin quý khách vui lòng chờ một lát, nhân viên hỗ trợ sẽ kết nối với quý khách trong thời gian sớm nhất.

Tuy nhiên:

* Không có ETA dự kiến
* Không có trạng thái hàng đợi
* Không có cập nhật tiến độ
* Người dùng phải chờ khá lâu mới có nhân viên phản hồi

### Assessment

⚠️ Có Human Handoff nhưng trải nghiệm chờ chưa tốt

---

## Case 3 – Tra cứu giá vé

### Input

> Giá vé ngày mai Hà Nội tới Lạng Sơn

### Observation

NEO:

* Hiểu nhu cầu tra cứu giá vé
* Hiểu ngày đi là ngày mai
* Hiểu điểm đi là Hà Nội
* Phát hiện Lạng Sơn không phải sân bay hợp lệ

Sau đó yêu cầu sửa điểm đến.

---

### Input

> Điểm đến Đà Nẵng

### Observation

NEO yêu cầu cung cấp số lượng hành khách.

---

### Input

> 1 người

### Observation

NEO yêu cầu xác nhận lại toàn bộ thông tin.

---

### Input

> Ừ

### Observation

NEO hiển thị danh sách chuyến bay và giá vé.

### Assessment

✅ Kết quả chính xác

❌ Workflow dài dòng

---

# 3. Four Paths

## Happy Path

### Scenario

Tra cứu hành lý.

### Flow

User hỏi

↓

NEO hiểu intent

↓

Trả lời chính xác

↓

Task hoàn thành

### Assessment

✅ Tốt

---

## Low Confidence Path

### Scenario

User nhập điểm đến không hợp lệ.

### Flow

User:

> Hà Nội → Lạng Sơn

↓

NEO phát hiện lỗi

↓

Yêu cầu nhập lại điểm đến

↓

Workflow tiếp tục

### Assessment

✅ Hệ thống xử lý tốt dữ liệu không hợp lệ

---

## Failure Path

### Scenario 1

User muốn nhận giá vé nhanh.

### Flow

User hỏi giá vé

↓

NEO thu thập từng trường

↓

Yêu cầu xác nhận

↓

Mới hiển thị kết quả

### Impact

Tăng số lượt hội thoại không cần thiết.

---

### Scenario 2

User yêu cầu nhân viên hỗ trợ.

### Flow

User yêu cầu nhân viên

↓

NEO báo chờ

↓

Không có ETA

↓

Không có cập nhật

↓

User chờ lâu

### Impact

Giảm độ tin cậy của trải nghiệm hỗ trợ.

---

## Correction Path

### Scenario

User nhập điểm đến không hợp lệ.

### Flow

User:

> Lạng Sơn

↓

NEO báo lỗi

↓

User:

> Đà Nẵng

↓

Workflow tiếp tục bình thường

### Assessment

✅ Correction hoạt động tốt

---

# 4. Main Finding

## Finding 1 (Chính)

Khi người dùng tra cứu giá vé bằng ngôn ngữ tự nhiên,

NEO có khả năng suy luận đúng phần lớn thông tin cần thiết nhưng vẫn thu thập dữ liệu theo mô hình form truyền thống và yêu cầu xác nhận lại trước khi hiển thị kết quả.

Hậu quả là số lượt hội thoại tăng lên đáng kể dù hệ thống đã có đủ dữ liệu để cung cấp kết quả sơ bộ.

### Layer

* UX Recovery
* Workflow Design

---

## Finding 2

Khi người dùng yêu cầu hỗ trợ từ nhân viên,

NEO có khả năng chuyển tiếp yêu cầu nhưng không cung cấp trạng thái xử lý hoặc thời gian chờ dự kiến.

Hậu quả là người dùng không biết yêu cầu của mình đã được tiếp nhận hay chưa và dễ mất kiên nhẫn trong thời gian chờ.

### Layer

* UX Recovery
* Human Handoff Experience

---

# 5. Product Decisions

## Decision 1

Chuyển từ:

Form Filling Conversation

sang:

Progressive Disclosure Conversation

Nguyên tắc:

Hiển thị kết quả sớm nhất có thể.

Cho phép chỉnh sửa sau.

---

## Decision 2

Thiết kế lại Human Handoff Flow.

Bổ sung:

* ETA
* Queue Status
* Progress Updates
* Alternative Channels

---

# 6. As-Is / To-Be

| As-Is                            | To-Be                          |
| -------------------------------- | ------------------------------ |
| User hỏi giá vé                  | User hỏi giá vé                |
| NEO thu thập từng trường dữ liệu | NEO suy luận tối đa từ câu hỏi |
| Hỏi số lượng khách               | Mặc định 1 người lớn           |
| Yêu cầu xác nhận lại toàn bộ     | Hiển thị kết quả ngay          |
| User phải xác nhận thêm          | Cho phép chỉnh sửa sau         |
| Mất 5-6 lượt hội thoại           | Nhận kết quả trong 1-2 lượt    |
| Trải nghiệm giống điền form      | Trải nghiệm giống hội thoại AI |

| As-Is                                     | To-Be                          |
| ----------------------------------------- | ------------------------------ |
| User yêu cầu nhân viên                    | User yêu cầu nhân viên         |
| NEO báo "vui lòng chờ"                    | NEO xác nhận tiếp nhận yêu cầu |
| Không có ETA                              | Hiển thị ETA dự kiến           |
| Không có trạng thái hàng đợi              | Hiển thị queue status          |
| Không có cập nhật                         | Cập nhật định kỳ               |
| User chờ trong trạng thái không chắc chắn | User biết rõ trạng thái xử lý  |

---

# 7. SPEC Changes

## Spec 1 – Fare Search

Nếu hệ thống đã xác định được:

* Điểm đi
* Điểm đến
* Ngày bay

Thì hiển thị ngay:

* Giá vé tham khảo
* Danh sách chuyến bay

Không yêu cầu xác nhận toàn bộ dữ liệu trước.

---

## Spec 2 – Human Handoff

Khi Human Handoff được kích hoạt:

Hiển thị:

* Thời gian chờ dự kiến
* Trạng thái hàng đợi

Nếu thời gian chờ vượt SLA:

Hiển thị:

* Hotline
* Email
* Form liên hệ

---

# 8. Success Metrics

### Fare Search

* Average Turns To Resolution
* Time To First Result
* Search Completion Rate

### Human Handoff

* Average Wait Time
* Human Handoff Completion Rate
* Conversation Abandonment Rate
* CSAT

---

# 9. Conclusion

NEO thể hiện khả năng hiểu intent và xử lý dữ liệu đầu vào khá tốt, đặc biệt trong các tác vụ tra cứu thông tin và sửa lỗi dữ liệu.

Tuy nhiên, trải nghiệm hội thoại vẫn mang nhiều đặc điểm của một form truyền thống, khiến người dùng phải trải qua nhiều bước xác nhận không cần thiết. Đồng thời, trải nghiệm chuyển sang nhân viên hỗ trợ còn thiếu minh bạch về trạng thái và thời gian chờ.

Hai cơ hội cải thiện lớn nhất là:

1. Hiển thị kết quả sớm hơn dựa trên dữ liệu đã suy luận được.
2. Thiết kế lại Human Handoff Flow để giảm sự không chắc chắn trong thời gian chờ hỗ trợ.
