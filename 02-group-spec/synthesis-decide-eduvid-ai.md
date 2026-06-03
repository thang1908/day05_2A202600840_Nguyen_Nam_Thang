# Synthesis & Decide — EduVid AI

Dùng sau khi nhóm đã có evidence. Mục tiêu là chốt một build slice đủ nhỏ cho Day 06.

## 1. Gom evidence thành cụm

Gom theo workflow/pain, không gom theo tên feature.

| Cụm evidence | Evidence liên quan | Ý nghĩa với sản phẩm |
|---|---|---|
| Tạo bài giảng video mất nhiều bước | Giáo viên phải làm slide, viết lời giảng, thu âm, dựng video bằng nhiều công cụ | EduVid AI nên gom thành một wizard liền mạch. |
| Giáo viên không muốn bắt đầu từ trang trắng | Gamma/Canva cho thấy nhu cầu tạo slide nhanh từ prompt/tài liệu | AI nên tạo bản nháp outline/slide trước để giáo viên sửa. |
| Nội dung chuyên môn cần kiểm soát | AI có thể tóm tắt sai hoặc thiếu ý từ giáo trình | Phải có bước review từng slide/script trước khi xuất. |
| Giọng đọc tiếng Việt là phần khó | Giáo viên không phải ai cũng có thời gian/thiết bị thu âm tốt | Nên có TTS tiếng Việt, chọn vùng miền và tốc độ đọc. |
| LMS/SCORM là nhu cầu chuyên nghiệp nhưng scope lớn | iSpring/Articulate hỗ trợ SCORM/xAPI | MVP xuất MP4; SCORM đưa vào backlog. |

## 2. Viết insight

```text
Giáo viên phổ thông không chỉ cần một công cụ thiết kế slide.
Họ thật ra cần một quy trình nhanh để biến tài liệu chuyên môn thành video bài giảng có thể kiểm soát chất lượng,
vì workflow hiện tại bị chia nhỏ qua nhiều công cụ và AI có thể gây rủi ro sai kiến thức nếu tự động hoàn toàn.
```

## 3. Viết opportunity

```text
Cơ hội là dùng AI để tạo bản nháp slide, lời giảng và giọng đọc tiếng Việt từ tài liệu có sẵn,
giúp giáo viên tạo video bài giảng nhanh hơn,
trong khi vẫn kiểm soát rủi ro sai kiến thức bằng cơ chế giáo viên duyệt/sửa trước khi xuất video.
```

## 4. Chọn build slice

Build slice tốt phải qua 5 câu hỏi:

| Câu hỏi | Đạt khi | EduVid AI |
|---|---|---|
| User cụ thể chưa? | Nói được ai dùng, trong bối cảnh nào. | Giáo viên THPT cần tạo video bài giảng từ tài liệu có sẵn. |
| Task đủ hẹp chưa? | Demo được trong 3-5 phút. | Upload tài liệu mẫu -> tạo slide -> sửa script -> chọn giọng -> xuất MP4 mô phỏng. |
| AI decision rõ chưa? | AI gợi ý/tự làm một việc cụ thể. | AI tạo bản nháp slide, script và voice-over. |
| Failure path rõ chưa? | Có một case AI không chắc hoặc sai để test. | AI tóm tắt sai/thiếu kiến thức, hệ thống yêu cầu giáo viên kiểm tra. |
| Có evidence không? | Có bằng chứng từ self-use/review/user/competitor. | Có self-use từ demo workflow, competitor evidence; cần bổ sung phỏng vấn giáo viên. |

## 5. Quyết định: giữ, giảm scope, hay đổi hướng?

| Tình huống | Quyết định cho EduVid AI |
|---|---|
| Evidence yếu, user mơ hồ | Giữ user hẹp là giáo viên THPT; phỏng vấn nhanh 1-2 giáo viên để kiểm pain. |
| Ý tưởng quá rộng | Không làm full LMS, avatar, SCORM trong MVP. |
| AI không cần thiết | AI cần thiết ở bước tóm tắt tài liệu, tạo slide, viết lời giảng và TTS. |
| Rủi ro cao | Chọn augmentation: AI draft, giáo viên duyệt. |
| Không demo được trong 1 ngày | Chỉ demo wizard 5 bước với dữ liệu mẫu; xuất video là trạng thái mô phỏng. |

## 6. Câu chốt cuối

```text
Dựa trên evidence về việc giáo viên phải dùng nhiều công cụ để tạo video bài giảng,
nhóm sẽ build prototype EduVid AI dạng wizard 5 bước,
cho giáo viên THPT,
để giải quyết pain chuyển tài liệu có sẵn thành video eLearning mất nhiều thời gian,
bằng cách AI tạo bản nháp slide, lời giảng và giọng đọc tiếng Việt,
và sẽ test failure path AI tóm tắt sai hoặc thiếu kiến thức chuyên môn.
```

## 7. Backlog

Những thứ không build trong Day 06:

- Xuất SCORM/xAPI/cmi5 để đưa lên LMS.
- Tích hợp trực tiếp Moodle, Google Classroom hoặc Canvas.
- AI avatar giống giáo viên.
- Clone giọng giáo viên.
- Tạo quiz tương tác nâng cao.
- Kho template theo từng môn học/lớp học.
- Kiểm tra đạo văn hoặc bản quyền tài liệu.
- Collaborative editing nhiều giáo viên.
- Analytics học sinh xem video và làm bài.
