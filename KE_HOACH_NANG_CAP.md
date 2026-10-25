# KẾ HOẠCH RÀ SOÁT & NÂNG CẤP TÍNH NĂNG: TRỢ LÝ VẼ HÌNH _ PHẠM HẬU
> **Căn cứ tham chiếu**: Bộ tài nguyên chuyên sâu **SKILL EDUCATION (14 Skills)** và yêu cầu thực tế của giáo viên Toán Việt Nam.

---

## I. TỔNG QUAN RÀ SOÁT ỨNG DỤNG HIỆN TẠI

### 1. Những điểm đã làm tốt (Ưu điểm cốt lõi)
- **Đúng định vị**: Đã chuyển đổi thành công từ một app giáo án cồng kềnh sang **"Trợ lý Nạp đề & Vẽ hình"** tinh gọn, tốc độ cao.
- **Đồng bộ trực tiếp**: Nạp đề (văn bản/ảnh OCR/bài mẫu) $\rightarrow$ Khung vẽ 3D/2D cập nhật tức thì.
- **Hình vẽ 3D Three.js mượt mà**: Có phân biệt nét liền/nét đứt, nhãn điểm không gian, góc nhìn SGK chuẩn mực.
- **Tiện ích cho giáo viên**: Đã có **Chế độ Giấy Trắng (White Paper Mode)** và nút **"Chép vào Word"** (1-click copy ảnh vào khay nhớ tạm).
- **Hạ tầng AI tin cậy**: Hỗ trợ nhập Gemini API Key cá nhân, lưu trữ an toàn trong `localStorage`, có cơ chế Fallback tự động khi gặp lỗi 429 quota.

### 2. Những khoảng trống cần bổ sung (Gaps & Opportunities)
| Tiêu chí | Trạng thái hiện tại | Hạn chế còn tồn tại | Cơ hội nâng cấp từ SKILL EDUCATION |
| :--- | :--- | :--- | :--- |
| **Xuất dữ liệu** | Mới có xuất ảnh PNG, SVG, copy clipboard | Giáo viên vẫn phải tự tạo file Word/PowerPoint thủ công | Tích hợp `docx-official` & `pptx-official` để xuất trọn gói đề thi/bài giảng |
| **Độ chuẩn xác hình học** | AI tạo tọa độ 1 lượt | Một số bài toán khó (khoảng cách, góc nhị diện, thiết diện xiên) chưa có bước tự động kiểm tra định lý hình học | Tích hợp `ai-agents-architect` & `langgraph` để kiểm toán tọa độ 2 lớp (Geometry Validator) |
| **Ký hiệu hình học** | Mới có các đỉnh và cạnh | Chưa có ký hiệu góc vuông ($\perp$), ký hiệu góc phẳng nhị diện ($\angle, \varphi$), mũi tên vector | Tích hợp `algorithmic-art` vẽ ký hiệu toán học chuyên nghiệp lên không gian 3D |
| **Tương tác trực tiếp** | Chỉ xoay/zoom và kéo thanh trượt thiết diện | Chưa cho phép giáo viên vẽ thêm nét phụ trực tiếp bằng cách click chọn 2 điểm | Bộ công cụ dựng hình tương tác (Interactive Constructing Tool) |
| **Kho học liệu** | Mới có 3 bài mẫu | Chưa có thư viện chuyên đề toàn diện hình học 10, 11, 12 | Thư viện hơn 50+ khối hình SGK chuẩn hóa theo từng bài học |

---

## II. DANH MỤC CÁC TÍNH NĂNG ĐỀ XUẤT NÂNG CẤP (DỰA TRÊN SKILL EDUCATION)

### 1. Nhóm Ký hiệu hình học & Tương tác thông minh (Ưu tiên P1)
1. **Ký hiệu góc vuông 3D ($\perp$)**: Tự động phát hiện các đoạn vuông góc (ví dụ: $SA \perp (ABCD)$, $AB \perp BC$) và vẽ ký hiệu vuông góc 3D định vị chuẩn trên mặt phẳng.
2. **Ký hiệu góc phẳng nhị diện & góc tạo bởi đường thẳng**: Cung tròn góc đánh dấu sinh động kèm nhãn chữ $\alpha, \beta, \varphi$.
3. **Công cụ "Kẻ thêm nét phụ" (Interactive Construction Tool)**: Giáo viên chỉ cần click chọn 2 điểm trên hình $S, A, B...$ để nối thêm đoạn thẳng phụ (chọn nét đứt hoặc nét liền), rất thuận tiện khi giảng bài trên lớp.

### 2. Nhóm Xuất bản Giáo án & Đề thi tự động (P2 - Tham chiếu `docx-official` & `pptx-official`)
1. **Xuất file Microsoft Word (.docx)**:
   - Tạo sẵn file đề kiểm tra / phiếu bài tập chuẩn thể thức Bộ GD&ĐT.
   - Nhúng hình vẽ tự động, kèm đề bài, gợi ý phương pháp giải và bảng đáp án.
2. **Xuất Slide bài giảng Microsoft PowerPoint (.pptx)**:
   - Tạo slide trình chiếu gồm Slide Đề bài $\rightarrow$ Slide Phân tích hình học $\rightarrow$ Slide Hình vẽ phóng to $\rightarrow$ Slide Kết luận.

### 3. Nhóm AI Agent kiểm toán tọa độ & hình học (P3 - Tham chiếu `ai-agents-architect` & `langgraph`)
1. **Geometry Integrity Validator**:
   - Tự động kiểm tra tích vô hướng $\vec{u} \cdot \vec{v} = 0$ với quan hệ vuông góc.
   - Đảm bảo các điểm thuộc cùng một mặt phẳng (thiết diện) có phương trình đồng phẳng chuẩn xác 100%.
   - Thuật toán tự động tối ưu góc quan sát để không bị hiện tượng 2 điểm hoặc 2 cạnh đè khít lên nhau (trùng nét).

### 4. Nhóm Kho học liệu chuẩn hóa SGK (P4 - Tham chiếu `firebase` & `frontend-design`)
1. **Thư viện 50+ dạng toán hình học không gian 10, 11, 12**:
   - Hình chóp tam giác, chóp tứ giác, chóp đều, chóp có cạnh bên/mặt bên vuông góc đáy.
   - Lăng trụ đứng, lăng trụ xiên, hình hộp chữ nhật, hình lập phương.
   - Khối tròn xoay: Khối nón, khối trụ, mặt cầu nội/ngoại tiếp.
   - Tọa độ không gian $Oxyz$.
2. **Kho hình vẽ cá nhân ("My Geometry Vault")**: Lưu lại các bài toán giáo viên đã nạp và chỉnh sửa vào bộ nhớ máy để mở lại bất kỳ lúc nào.

### 5. Nhóm Mở rộng Tiện ích Trình duyệt (P5 - Tham chiếu `browser-extension-builder`)
1. **Chrome / Edge Extension**: Cho phép giáo viên bôi đen đề toán trên các trang tài liệu (VnDoc, VietJack, OLM, Tuyensinh247...) $\rightarrow$ Chuột phải chọn "Vẽ hình với Trợ lý Phạm Hậu" để đưa thẳng vào ứng dụng.

---

## III. LỘ TRÌNH THỰC HIỆN ĐỀ XUẤT

| Giai đoạn | Hạng mục | Giá trị mang lại |
| :---: | :--- | :--- |
| **P1** | Ký hiệu góc vuông 3D & Cung đo góc phẳng nhị diện | Hình vẽ sinh động, chuẩn mực sư phạm tuyệt đối |
| **P2** | Công cụ click nối thêm đường phụ trên 3D | Hỗ trợ giáo viên biểu diễn giải toán từng bước trên lớp |
| **P3** | Xuất file Word (.docx) & Slide PowerPoint (.pptx) | Tiết kiệm 90% thời gian soạn bài và làm đề kiểm tra |
| **P4** | Mở rộng 50+ hình mẫu chuẩn SGK Kết nối tri thức | Có sẵn kho tư liệu giảng dạy toàn bộ chương trình 11-12 |
| **P5** | AI Geometry Validator & Tự động tránh trùng nét | Đảm bảo tính toán học giải tích chính xác tuyệt đối |
