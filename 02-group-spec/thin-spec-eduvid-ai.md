# Thin SPEC Cuối Day 05 — EduVid AI

Thin SPEC không phải PRD đầy đủ. Đây là bản cam kết đủ rõ để sáng Day 06 nhóm build ngay.

## 1. Track, product/app và user

**Track:** Education / eLearning / AI for Teachers  
**Product/app thật:** EduVid AI - wizard tạo video bài giảng từ tài liệu có sẵn  
**User cụ thể:** Giáo viên THPT cần tạo video bài giảng 10-15 phút từ tài liệu PDF/PPTX/DOCX.  
**Nhóm có phải user thật không? Nếu không, khác ở đâu?**  
Nhóm không hoàn toàn là user thật. Nhóm có thể mô phỏng workflow tạo bài giảng, nhưng khác giáo viên thật ở kinh nghiệm sư phạm, yêu cầu bám chương trình học, áp lực thời gian, và trách nhiệm về độ chính xác kiến thức. Vì vậy nhóm cần phỏng vấn nhanh giáo viên để kiểm chứng pain.

## 2. Evidence summary

| Evidence | Nguồn | User/pain nói lên điều gì? | SPEC phải đổi gì? |
|---|---|---|---|
| Workflow tạo video bài giảng gồm nhiều bước: đọc tài liệu, làm slide, viết lời giảng, thu âm, dựng video. | Self-use / mô phỏng trong demo EduVid AI | Giáo viên mất thời gian vì phải dùng nhiều công cụ rời rạc. | Build slice cần gom workflow thành wizard 5 bước. |
| AI có thể tạo slide/script nhanh nhưng có rủi ro sai hoặc thiếu kiến thức. | Quan sát từ bước sửa slide/script trong demo | Giáo viên cần giữ quyền duyệt nội dung. | Chọn augmentation thay vì automation hoàn toàn. |
| Các công cụ như Gamma/Canva tạo slide nhanh; Synthesia/HeyGen tạo video/voice; iSpring/Articulate hỗ trợ eLearning/SCORM. | Competitor evidence public | Thị trường có các mảnh giải pháp, nhưng giáo viên vẫn phải ghép nhiều công cụ. | EduVid AI nên tập trung vào workflow tích hợp cho giáo viên Việt Nam. |
| Chưa có phỏng vấn giáo viên thật trong repo. | Gap hiện tại | Evidence user còn yếu. | Cần kiểm bằng phỏng vấn nhanh trước checkpoint M1 Day 06. |

## 3. Pain statement

```text
User giáo viên THPT đang gặp khó ở bước chuyển tài liệu bài giảng có sẵn thành video eLearning,
vì phải tự làm slide, viết lời giảng, thu âm và dựng video bằng nhiều công cụ khác nhau,
dẫn tới mất nhiều thời gian và chất lượng bài giảng không đồng đều.
Bằng chứng chính là self-use workflow và competitor evidence cho thấy mỗi công cụ chỉ giải quyết một phần của quy trình.
```

## 4. Build slice

```text
Cho giáo viên THPT đang cần tạo video bài giảng 10-15 phút từ tài liệu PDF/PPTX/DOCX,
prototype EduVid AI sẽ dùng AI để tạo bản nháp slide, lời giảng và giọng đọc tiếng Việt,
tạo ra video bài giảng MP4,
và xử lý failure mode AI tóm tắt sai hoặc thiếu kiến thức bằng cơ chế giáo viên duyệt/sửa từng slide và script trước khi xuất video.
```

## 5. Auto/Aug decision

Chọn một:

- [x] **Augmentation:** AI gợi ý/draft/phân loại, user quyết cuối.
- [ ] **Conditional automation:** AI tự làm trong case hẹp; case mơ hồ/rủi ro chuyển người.
- [ ] **Automation:** AI tự quyết và tự hành động.

**Lý do chọn:**  
Nội dung bài giảng có rủi ro sai kiến thức. Nếu AI tự động xuất video mà không có giáo viên duyệt, học sinh có thể học sai. Vì vậy AI chỉ nên tạo bản nháp slide, lời giảng và giọng đọc; giáo viên là người quyết định nội dung cuối.

**Human role:** reviewer / decider / rescuer  

Giáo viên review slide, quyết định sửa/xóa/thêm nội dung, và rescue khi AI tạo nội dung không đúng.

## 6. Four paths

| Path | Prototype phải thể hiện gì? |
|---|---|
| Happy | Giáo viên upload tài liệu mẫu "Quang hợp.pdf", chọn 10-15 slide, AI tạo slide, script, chọn giọng đọc, xuất MP4 mô phỏng. |
| Low-confidence | Một slide được đánh dấu "AI chưa chắc - cần giáo viên kiểm tra" khi nội dung tài liệu thiếu rõ ràng hoặc có khái niệm khó. |
| Failure | AI tóm tắt sai/thiếu một ý quan trọng, ví dụ bỏ qua điều kiện cần cho quang hợp hoặc nhầm sản phẩm của quá trình. |
| Correction | Giáo viên sửa tiêu đề/bullet/script, yêu cầu "AI gợi ý sửa", sau đó duyệt lại trước khi xuất video. |

## 7. Failure mode nguy hiểm nhất

```text
Nếu user upload tài liệu chuyên môn có nhiều khái niệm khó hoặc phần scan không rõ,
AI có thể tóm tắt sai, bỏ sót ý quan trọng hoặc diễn giải quá đơn giản,
hậu quả là học sinh tiếp nhận kiến thức sai trong video bài giảng.
Prototype sẽ xử lý bằng giáo viên duyệt/sửa từng slide và script, hiển thị cảnh báo low-confidence, và không cho xuất video khi còn slide cần kiểm tra.
Owner kiểm thử path này là [Tên thành viên phụ trách test].
```

## 8. Owner plan cho sáng Day 06

| Thành viên | Việc phụ trách | Bằng chứng cần có trong repo |
|---|---|---|
| [Tên thành viên 1] | Research / evidence | Ảnh/chụp màn hình workflow hiện tại, link competitor, ghi chú phỏng vấn giáo viên. |
| [Tên thành viên 2] | SPEC | File `thin-spec-eduvid-ai.md` và cập nhật sau khi có evidence thật. |
| [Tên thành viên 3] | Prototype | HTML/CSS/JS demo wizard 5 bước, có dữ liệu bài giảng mẫu. |
| [Tên thành viên 4] | Test / failure path | Checklist happy path, low-confidence, failure, correction; ảnh hoặc video test. |
| [Tên thành viên 5] | Demo script / repo | Script demo 3-5 phút, README nêu cách chạy prototype và flow demo. |

## 9. Demo script ngắn

```text
1. Giáo viên upload tài liệu bài giảng mẫu.
2. Chọn số slide, thời lượng, đối tượng học và yêu cầu thêm.
3. AI tạo bản nháp slide.
4. Giáo viên sửa một slide có nội dung chưa ổn.
5. AI viết lời giảng cho slide.
6. Giáo viên chọn giọng đọc tiếng Việt và tốc độ đọc.
7. Hệ thống xuất video MP4 mô phỏng.
8. Nhóm demo failure path: AI đánh dấu một slide low-confidence và yêu cầu giáo viên duyệt trước khi xuất.
```
