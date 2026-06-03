# Evidence Pack — EduVid AI

Nộp kèm thin SPEC cuối Day 05.

## 1. Nhóm và track

**Tên nhóm:** [Điền tên nhóm]  
**Track:** Education / eLearning / AI for Teachers  
**Product/app đã chọn:** EduVid AI  
**Build slice đang nghĩ:** Giáo viên upload tài liệu PDF/PPTX/DOCX, AI tạo bản nháp slide, lời giảng và giọng đọc tiếng Việt, sau đó xuất video bài giảng MP4.

## 2. Self-use evidence

Nhóm tự mô phỏng workflow của một giáo viên khi cần tạo video bài giảng từ tài liệu có sẵn.

| Observation | Screenshot/link | Path liên quan | Điều học được |
|---|---|---|---|
| Để tạo một video bài giảng, giáo viên thường phải đi qua nhiều bước rời rạc: đọc tài liệu, chọn ý chính, làm slide, viết lời giảng, thu âm, ghép audio với slide, xuất video. | File demo: `eduvid_wizard_demo(2).html` | Happy | Có thể gom quy trình này thành một wizard 5 bước để giảm tải thao tác cho giáo viên. |
| Khi AI tự tạo slide/lời giảng, giáo viên vẫn cần sửa lại nội dung vì kiến thức chuyên môn có thể bị tóm tắt thiếu hoặc sai. | Quan sát từ bước "Xem & sửa slide" và "Lời giảng" trong demo | Correction / Failure | Sản phẩm không nên tự động xuất video ngay. Cần có bước giáo viên duyệt slide và script trước khi tạo audio/video. |
| Việc chọn giọng đọc tiếng Việt là một bước quan trọng vì giáo viên có thể cần giọng miền Bắc, miền Nam, miền Trung hoặc tốc độ đọc khác nhau. | Bước "Giọng đọc" trong demo | Happy / Correction | Voice-over nên là lựa chọn có thể tùy chỉnh, không nên cố định một giọng đọc duy nhất. |
| Nếu chỉ xuất MP4 thì dễ demo trong một ngày, nhưng nếu muốn dùng trong LMS chuyên nghiệp thì sau này cần thêm SCORM/xAPI. | So sánh với các công cụ như iSpring, Articulate | Backlog | MVP nên xuất MP4 trước; SCORM để sau vì scope lớn. |

## 3. User / review / social evidence

Nguồn có thể là review App Store/Play, group, comment, phỏng vấn nhanh, hoặc nguồn public khác.

| Quote / review / observation | Nguồn | User là ai? | Pain/failure mode |
|---|---|---|---|
| Đây là giả định cần kiểm: giáo viên mất nhiều thời gian khi phải tự chuyển tài liệu thành slide, tự ghi âm và dựng video. | Cần phỏng vấn nhanh 1-2 giáo viên trước checkpoint M1 Day 06 | Giáo viên phổ thông / giảng viên / giáo viên trung tâm | Workflow tạo bài giảng video quá nhiều bước, phải dùng nhiều công cụ. |
| Gamma cho phép tạo presentation từ prompt hoặc nội dung có sẵn, cho thấy thị trường đã có nhu cầu tạo slide nhanh bằng AI. | https://gamma.app/ | Người tạo slide / giáo viên / nhân sự đào tạo | AI tạo slide nhanh nhưng chưa tối ưu riêng cho quy trình eLearning tiếng Việt. |
| iSpring Suite hỗ trợ PowerPoint-to-eLearning, quiz, video lecture và chuẩn SCORM, cho thấy LMS/SCORM là nhu cầu thật trong eLearning chuyên nghiệp. | https://www.ispringsolutions.com/ispring-suite | Instructional designer / giáo viên / doanh nghiệp đào tạo | Công cụ chuyên nghiệp mạnh nhưng giáo viên phổ thông có thể thấy nặng và cần học nhiều. |
| Synthesia và HeyGen cho thấy AI avatar/voice/video là xu hướng phổ biến trong đào tạo và truyền thông. | https://www.synthesia.io/ ; https://www.heygen.com/ | Người tạo video đào tạo | Có thể tạo video nhanh, nhưng chưa giải quyết trọn workflow từ giáo trình -> slide -> script -> video cho giáo viên Việt Nam. |

Nếu chưa có nguồn ngoài nhóm, ghi rõ:

```text
Đây là giả định. Nhóm sẽ kiểm bằng cách phỏng vấn nhanh 1-2 giáo viên hoặc giảng viên trước checkpoint M1 Day 06.
Câu hỏi kiểm:
1. Thầy/cô hiện tạo video bài giảng bằng những công cụ nào?
2. Mất bao lâu để biến một tài liệu có sẵn thành video bài giảng 10-15 phút?
3. Bước nào mất thời gian nhất: làm slide, viết lời giảng, thu âm, hay dựng video?
4. Nếu dùng AI, thầy/cô muốn AI tự làm phần nào và phần nào bắt buộc phải tự duyệt?
```

## 4. Competitor / analog evidence

| App / mô hình tham khảo | Họ xử lý task này thế nào? | Pattern học được | Có áp dụng trong 1 ngày không? |
|---|---|---|---|
| Gamma | Nhập prompt/tài liệu để tạo presentation nhanh. | Người dùng không muốn bắt đầu từ slide trắng; AI nên tạo bản nháp có cấu trúc trước. | Có. Áp dụng ở bước AI tạo outline/slide. |
| Canva | Tạo slide, hình ảnh, video và template nhanh. | Template đẹp giúp giáo viên tiết kiệm thời gian thiết kế. | Một phần. Demo bằng template slide đơn giản. |
| iSpring Suite | Biến PowerPoint thành eLearning, có quiz, video lecture, SCORM. | eLearning chuyên nghiệp cần quiz và xuất LMS. | Chưa nên làm SCORM trong MVP; để backlog. |
| Articulate 360 | Tạo khóa học tương tác, quiz, mô phỏng, hỗ trợ AI. | Chuẩn ngành eLearning cần review, tương tác và chuẩn xuất bản. | Không trong MVP; chỉ học pattern duyệt nội dung và interaction. |
| Synthesia / HeyGen | Tạo video bằng AI avatar và voice. | Video bài giảng có thể tạo từ script, không cần giáo viên tự quay. | Một phần. MVP chọn voice-over trước, avatar để backlog. |

## 5. Evidence -> Insight

```text
Evidence nổi bật nhất:
Quy trình tạo video bài giảng hiện bị chia nhỏ qua nhiều công cụ: tài liệu gốc, slide, script, thu âm, dựng video và LMS.

Insight:
Giáo viên không chỉ cần một công cụ tạo slide đẹp.
Thật ra họ cần một workflow giúp biến tài liệu chuyên môn thành bài giảng video có thể kiểm soát được,
vì rủi ro lớn nhất không phải thiết kế xấu mà là nội dung bị sai, thiếu hoặc không phù hợp trình độ học sinh.

Opportunity:
AI có thể giúp bằng cách tạo bản nháp slide, lời giảng và giọng đọc tiếng Việt,
nhưng giáo viên vẫn duyệt/sửa nội dung trước khi xuất video.
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
Trước evidence, nhóm định làm một nền tảng tạo bài giảng eLearning gần như tự động hoàn toàn.

Sau evidence, nhóm đổi thành một wizard hỗ trợ giáo viên tạo video bài giảng từ tài liệu có sẵn,
trong đó AI tạo bản nháp slide, lời giảng và giọng đọc, còn giáo viên duyệt trước khi xuất video.

Lý do:
Tự động hoàn toàn có rủi ro sai kiến thức và scope quá lớn cho Day 06.
MVP dạng augmentation vừa demo được nhanh, vừa thể hiện rõ vai trò của AI và human review.
```
