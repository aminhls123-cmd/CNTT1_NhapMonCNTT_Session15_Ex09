# Bài 9: Tự Thiết Kế Hệ Thống Lưu Trữ và Phân Quyền Cho Dự Án CampusPay

## Phần 1: Phân tích & Cấu trúc Thư mục (I/O)
- **Đầu vào:** 4 nhóm vai trò (Kỹ thuật, Thiết kế, Kinh doanh, Nhà đầu tư) và 5 nhóm tài liệu (Mã nguồn, UI/UX, Business Plan, Slide Pitch, Dữ liệu nhạy cảm).
- **Đầu ra:** Cấu trúc thư mục Google Drive 2 cấp và bảng phân quyền tối thiểu.
- **Cấu trúc thư mục Google Drive:**
   - 📁 `00_CampusPay_Master`
   - ├── 📁 `01_Ban_Ky_Thuat` (Source code, API Keys)
   - ├── 📁 `02_Ban_Thiet_Ke` (UI/UX, Assets đồ họa)
   - ├── 📁 `03_Ban_Kinh_Doanh` (Business Plan, Dữ liệu khách hàng)
   - ├── 📁 `04_Cross_Functional_Shared` (Slide Pitch chính dùng chung)
   - └── 📁 `05_External_Investors` (Tài liệu gửi nhà đầu tư)

---

## Phần 2: Phân quyền & Xử lý Bẫy dữ liệu
- **Tóm tắt phân quyền cốt lõi:**
  - *Mã nguồn & API Keys:* Ban Kỹ thuật (**Editor**), các ban khác (**No Access**).
  - *Tài sản UI/UX:* Ban Thiết kế (**Editor**), Kỹ thuật/Kinh doanh (**Viewer**).
  - *Business Plan:* Ban Kinh doanh (**Editor**), Kỹ thuật & Nhà đầu tư (**Viewer**).
  - *Slide Pitch:* Ban Kinh doanh (**Editor**), các ban khác & Nhà đầu tư (**Viewer**).
- **Cách xử lý 3 bẫy dữ liệu:**
  - **Bẫy 1 (Kỹ thuật xem Business Plan):** Cấp quyền **Viewer**, tuyệt đối không cấp Editor để bảo mật thông tin.
  - **Bẫy 2 (Nhà đầu tư xem Slide offline):** Cấp quyền **Viewer**, giữ nguyên tính năng tải xuống bản PDF, cài đặt **Expiration Date** (tự hủy quyền sau 14 ngày).
  - **Bẫy 3 (Nhân sự nghỉ việc):** Thực hiện **Remove Access** ngay lập tức và **Transfer Ownership** nếu họ đang sở hữu file quan trọng.
