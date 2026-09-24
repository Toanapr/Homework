# Kế hoạch thực hiện HW01

## Tóm tắt

Hoàn thành ba yêu cầu chính và toàn bộ phần AI compliance theo đề: 10 tin tuyển dụng, 20 software defects, 15 test case cho một thiết bị vật lý, mindmap, bằng chứng thực thi, GitHub Issues, prompt log, AI Audit Report, AI Critique và các biểu mẫu ký tên.

- Deadline: **28/09/2026**.
- Tin tuyển dụng hợp lệ: đăng từ **30/07/2026 đến 28/09/2026**.
- AI chính: **ChatGPT**; đồng thời phải khai báo việc dùng **Codex/OpenAI trong giai đoạn lập kế hoạch này**.
- Chưa thiết kế test case cụ thể cho đến khi có brand, model, năm sản xuất và serial của thiết bị.
- Mục tiêu hoàn thiện và kiểm tra lần cuối vào **27/09**, dành ngày 28/09 làm dự phòng.

Nguồn yêu cầu: :codex-file-citation{path="/Users/toanhuynh/UNI/SOFTWARE TESTING/Homework/2026.HW01.Jobs.Defects.PhysicalProduct_En.pdf" purpose="source"}, :codex-file-citation{path="/Users/toanhuynh/UNI/SOFTWARE TESTING/Homework/AI Templates/[AI-02] - FIT@HCMUS - AI Audit Report_En.docx" purpose="source"}, :codex-file-citation{path="/Users/toanhuynh/UNI/SOFTWARE TESTING/Homework/AI Templates/[AI-03] - FIT@HCMUS - AI Disclosure Form_En.docx" purpose="source"}, :codex-file-citation{path="/Users/toanhuynh/UNI/SOFTWARE TESTING/Homework/AI Templates/[AI-05] - FIT@HCMUS - AI Privacy Checklist_En.docx" purpose="source"}, và :codex-file-citation{path="/Users/toanhuynh/UNI/SOFTWARE TESTING/Homework/AI Templates/[AI-06] - FIT@HCMUS - AI Student Acknowledgement_En.docx" purpose="source"}.

## Cấu trúc bài và dữ liệu

- Main report viết bằng Markdown, xuất PDF; gồm thông tin sinh viên, R1, R2, R3, AI Audit Report, AI Critique, Mandatory Disclosure và Self-assessment.
- Workbook Excel có tối thiểu ba sheet: `Test Cases`, `Checklist`, `Test Summary`.
- `prompt_log.md` ghi mọi prompt, tool, timestamp `HH:MM dd/mm/yyyy` và nguyên văn output.
- Appendix A chia thành `A1 AI Audit Report` và `A2 Full Prompt Log` để xử lý mâu thuẫn cách đặt appendix trong đề.
- Lưu ảnh gốc và video metadata trong GitHub; nhúng ảnh cần chấm trực tiếp vào report để không phụ thuộc hoàn toàn vào liên kết online.
- Gói nộp cuối: `<StudentID>_HW01_AI_<Grade>.zip`, trong đó `<Grade>` là ba chữ số `000–100`.

Các bảng dùng schema cố định:

- Job (đúng theo đề, mỗi tin): link, dated screenshot, job description, required skills, salary/not disclosed, AI Impact Analysis 1–2 câu. Việc tin có yêu cầu AI hay không chỉ ghi ở bảng tóm tắt để đếm điều kiện ≥3 tin.
- Defect: ID, product/system, publicized date, source, description, severity, consequences, solution, AI/LLM-related flag, AI claim, verified error/bias/hallucination, correction and verification source.
- Test case: ID, objective, preconditions, input, steps, expected result, actual result, verdict, technique, edge-case flag, AI-missed evidence, execution/video/issue link.

## Các bước thực hiện

1. **Khởi tạo và ghi log ngay từ đầu**
   - Tạo cấu trúc HW01 và `prompt_log.md` trước khi gửi thêm prompt AI.
   - Lưu cuộc trao đổi lập kế hoạch hiện tại như một lần sử dụng Codex.
   - Kiểm tra AI-06 đã được ký từ Week 1; nếu chưa, hoàn thành trước khi nộp.
   - Commit: `chore(hw01): initialize assignment structure and prompt log`.

2. **Requirement 1 – Job Market 2026+**
   - Thu thập đúng 10 tin còn truy cập được trong cửa sổ ngày hợp lệ; ít nhất 3 tin yêu cầu AI/LLM/AI-assisted automation.
   - Chụp từng tin với ngày đăng và username/display name của tài khoản trong cùng bằng chứng.
   - Không suy đoán salary: ghi `Not disclosed` nếu tin không công bố.
   - Viết 1–2 câu AI Impact Analysis riêng cho từng tin, phân loại AI `replace / assist / cannot replace`.
   - Yêu cầu ChatGPT tạo một mindmap kết hợp **ISTQB test process** và **QA/QC roles 2026+**; xác minh và chỉ ra ít nhất 3 lỗi thật, có nguồn ISTQB/course material và phiên bản sửa.
   - Commit: `docs(hw01): add job market research and mindmap critique`.

3. **Requirement 2 – 20 Software Defects**
   - Chọn đúng 20 defect được công bố trong giai đoạn 2022–2026; tối thiểu 5 defect liên quan AI/LLM như hallucination, prompt injection hoặc bias.
   - Ưu tiên nguồn gốc: vendor advisory, incident report, CVE/NVD, cơ quan quản lý hoặc tài liệu kỹ thuật chính thức.
   - Với từng defect, yêu cầu ChatGPT giải thích rồi kiểm chứng từng khẳng định. Ghi đúng một lỗi có thật thuộc bias, hallucination hoặc thông tin sai không được nguồn hỗ trợ; không được bịa lỗi nếu output đúng.
   - Nếu một output không có lỗi phù hợp, dùng một prompt phân tích khác và tiếp tục kiểm chứng; lưu toàn bộ lần thử trong prompt log.
   - Hoàn thành description, severity, consequences và solution bằng nguồn đã kiểm chứng.
   - Commit: `docs(hw01): document software defects and verified AI errors`.

4. **Requirement 3 – Physical Product**
   - Checkpoint bắt buộc: nhận thiết bị cụ thể từ người dùng; ghi brand, model, year và serial đã che đúng bốn ký tự ở giữa.
   - Người dùng tự chụp ảnh thiết bị và thẻ sinh viên trong cùng khung hình; AI không tạo hoặc chỉnh sửa ảnh này.
   - Cho ChatGPT tạo một batch test case ban đầu, sau đó tự phân tích và hoàn thiện thành đúng 15 test case.
   - Phân bổ bao phủ: chức năng, trạng thái/mode, usability, reliability, recovery và các tình huống biên an toàn; không thực hiện thử nghiệm có nguy cơ điện, nhiệt, nước hoặc phá hỏng thiết bị.
   - Có ít nhất 3 edge case mà output AI ban đầu không đưa ra. Lưu ảnh hội thoại chứng minh thiếu sót và giải thích bằng văn bản vì sao AI bỏ sót.
   - Thực thi ít nhất 5 test case; các case chưa chạy ghi `NOT RUN`, không để trống hoặc giả lập Actual/Verdict.
   - Người dùng tự quay ít nhất 5 video, mỗi video không quá 60 giây và có giọng thuyết minh thật; upload YouTube Unlisted.
   - Mục tiêu tìm ít nhất 5 defect thật. Nếu tìm được defect, tạo GitHub Issue với bước tái hiện, expected/actual, impact và evidence. Không bịa thêm để đủ 5.
   - Chụp trang GitHub Issues có hiển thị GitHub username.
   - Commits:
     - `test(hw01): design physical product test suite`
     - `test(hw01): add execution results and defect evidence`

5. **AI compliance và báo cáo**
   - AI-02: mỗi batch sinh bởi một prompt là một artifact; điền đủ prompt/tool/time, full output, verdict, reasoning có citation và student fix.
   - Tính tỷ lệ `VALID / INVALID / INCOMPLETE`; tổng phải bằng 100%.
   - Viết AI Critique 200–300 từ bằng hiểu biết của sinh viên, đề cập lỗi, bias/incompleteness, nguyên nhân AI bỏ sót và bài học cộng tác.
   - Điền AI-03 với tất cả tool, giai đoạn sử dụng, 2–3 prompt quan trọng, đóng góp cụ thể và cách kiểm chứng.
   - Hoàn thành, ký AI-03 và AI-05; chèn nguyên văn Mandatory Disclosure trước appendices.
   - Tự chấm theo rubric cuối đề: R1 `40`, R2 `20`, R3 `25`, AI compliance `15`.
   - Commit: `docs(hw01): complete AI audit disclosure and self assessment`.

6. **Đóng gói**
   - Xuất Markdown thành PDF và kiểm tra trực quan toàn bộ trang.
   - ZIP chứa: main report PDF, source Markdown, `prompt_log.md`, workbook Excel, device photo, file chứa YouTube links, mindmap, GitHub Issues screenshot, AI-02, AI-03 và AI-05 đã hoàn thành/ký.
   - Commit: `build(hw01): add verified report and submission package`.

## Việc còn lại của R1 (theo dõi nội bộ, không đưa vào report)

- [x] JP05–JP07 đã thay bằng tin ITviec có nhãn “Posted …”: QIG (23/09/2026), FPT Digital (15/09/2026), Saritasa (16/09/2026).
- [x] Đã chụp lại `JP05.png`, `JP06.png`, `JP07.png` trên ITviec (24/09/2026).
- [x] JP01 đã thay bằng Floware – Senior Automation Test (AI, QA QC, API), `datePosted` 04/09/2026.
- [x] Đã chụp `R1_Job_Postings/JP01.png` (Floware) khi đăng nhập ITviec.
- [x] Ảnh không dùng đã xoá; toàn bộ ảnh đặt tên thống nhất `JP01.png`–`JP10.png`.
- [ ] Điền ngày nộp thực tế vào report và kiểm lại cửa sổ 60 ngày.

## Việc còn lại của R2 (theo dõi nội bộ, không đưa vào report)

- [x] 20 defect (D01–D20) đã viết vào report mục 2.2–2.3, mọi dữ kiện đối chiếu với nguồn chính thức; 7 defect AI/LLM (D14–D20).
- [ ] Sinh viên tự gửi prompt cho ChatGPT cho từng defect, ghi vào `prompt_log.md` với timestamp `HH:MM dd/mm/yyyy` và nguyên văn output.
- [ ] So từng khẳng định của AI với bản ghi 2.3 + nguồn; chọn 1 lỗi thật (hallucination / bias / sai lệch không có nguồn) cho mỗi defect, điền bảng 2.4.
- [ ] Nếu output của một defect không có lỗi: dùng prompt khác (hỏi sâu hơn: số liệu, timeline, CVSS, bản vá), không được bịa lỗi.
- [ ] Chụp màn hình hội thoại (có thấy tài khoản) cho các lỗi tiêu biểu để làm bằng chứng.

### Prompt gợi ý (sinh viên tự gửi, tự ghi log)

```text
Explain the software defect "<tên defect>" (<năm>). Include: root cause, exact date,
affected versions or scope, severity (CVSS if any), number of affected users/devices,
consequences, and the official fix. Cite your sources.
```

Các điểm dễ bắt lỗi AI (so với report): ngày công bố, số liệu (8,5 triệu máy, 362.758 xe, 700.000 hành khách, 92 triệu cuộc gọi, CAD 812,02, USD 5.000), điểm CVSS (NVD và vendor khác nhau ở D09, D19), phiên bản vá (D08, D09, D10, D12, D18), nguyên nhân gốc (D02 re-order term BGP, D04 xoá file khi đồng bộ DB, D13 redis-py asyncio), link/nguồn không tồn tại, và thiên lệch khi đổ lỗi (ví dụ đổ cho Microsoft ở D01, cho "tấn công mạng" ở D04).

### Mẫu một entry trong `prompt_log.md`

```text
### R2-D01 – HH:MM dd/mm/yyyy – ChatGPT (<model>)
Prompt: <nguyên văn>
Output: <nguyên văn, không sửa>
Error found: <trích câu sai> → Fact: <đúng theo nguồn> (<link>) – Type: hallucination/bias
```

## Kiểm thử và tiêu chí chấp nhận

- Đúng 10 jobs; tất cả thuộc cửa sổ 60 ngày; ≥3 jobs yêu cầu AI; đủ 10 ảnh có username.
- Đúng 20 defects; ≥5 AI/LLM-related; đủ 20 phân tích lỗi/bias/hallucination của AI có kiểm chứng.
- Đúng 15 test cases; ≥3 AI-missed edge cases; ≥5 case chạy thật; ≥5 video hợp lệ.
- Mọi defect của thiết bị được ghi thành GitHub Issue; không tuyên bố defect thiếu bằng chứng.
- Mindmap có output gốc, 3 lỗi được chỉ ra và phiên bản sửa.
- Prompt log bao phủ mọi AI interaction; Audit Report bao phủ mọi artifact AI.
- AI Critique nằm trong 200–300 từ; disclosure đúng nguyên văn; AI-03 và AI-05 có chữ ký.
- PDF không lỗi bảng, ảnh, liên kết hoặc ký tự; video/link được thử ở chế độ đăng xuất.
- ZIP đúng tên, grade ba chữ số, mỗi file ≤20 MB và sẵn sàng upload Moodle trước deadline.

## Giả định đã khóa

- Dùng ChatGPT làm AI chính, nhưng khai báo thêm Codex vì đã được dùng để đọc đề và lập kế hoạch.
- Không cần AI-04 vì HW01 không được mô tả là Major Project.
- Assignment-specific filename `StudentID_HW01_AI_<grade>.zip` được ưu tiên hơn quy tắc tên chung.
- Trong lúc chưa có thiết bị, chỉ làm R1, R2, mindmap và phần AI compliance; không sinh 15 test case chung chung.
- Bằng chứng chống gian lận—ảnh thiết bị/thẻ, screenshot tài khoản và video có giọng nói—do sinh viên tự tạo, không dùng AI.
