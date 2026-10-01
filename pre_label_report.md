# Pre-Label & PointPillars Practice Report (Day 13)

## 1. Thông tin nhóm và thành viên
- **Tên nhóm:** Cá nhân (Lê Vĩnh Hưng)
- **Danh sách thành viên & Vai trò:**
  1. Lê Vĩnh Hưng - Vai trò: Thực hiện độc lập toàn bộ các bước (Cài đặt môi trường Windows 11 / WSL2/Docker, Chạy PointPillars Pretrained, Rà soát và gán nhãn 3D trên CVAT).
- **Kênh làm việc riêng / Nơi thu báo cáo:** Theo chỉ định của Lab Coach (LC)

---

## 2. Kết quả Chạy Thử nghiệm Môi trường A/B/C (PointPillars Pretrained)
- **Môi trường / Thiết bị chạy:** Windows 11 (thông qua WSL2 và Docker Desktop)
- **Image / Docker Architecture:** `student-prelabel-amd64.zip`
- **Thông số cấu hình / Input:** Cấu hình PointPillars mặc định theo bộ Student KITTI của lab.
- **Kết quả A/B/C (Số lượng hộp phát hiện):**
  - Chạy lần 1: Hoàn thành khởi tạo thành công, trích xuất tự động các bounding box 3D cho các đối tượng tĩnh và động xung quanh.
- **Thời gian chạy (Wall time):** ~19.15s trên nền tảng WSL2 (amd64).

---

## 3. Nhật ký Kiểm tra và Sửa Pre-Label (Source Job)
- **Job ID CVAT:** [Điền ID công việc trên CVAT của bạn]
- **Nhận xét tổng quan về Pre-label từ Model:** 
  - Mô hình PointPillars tạo các hộp gợi ý khá tốt cho các xe ở cự ly gần và trung bình. Tuy nhiên, tại các vùng điểm LiDAR thưa hoặc khuất, kích thước và góc xoay (orientation) chưa hoàn toàn chính xác, cần tinh chỉnh thủ công để khớp với point cloud và ảnh camera.
- **Chi tiết các lỗi đã phát hiện và sửa đổi:**
  - **Class Car / Vehicle:** Điều chỉnh lại góc quay hướng (orientation) và kéo giãn/thu hẹp kích thước bounding box cho sát thực tế.
  - **Class Pedestrian / Cyclist / Others:** Kiểm tra và căn chỉnh lại các đối tượng nhỏ, người đi bộ ở tầm nhìn xa.
  - **Hộp thiếu (False Negative):** Đã bổ sung thủ công các đối tượng bị model bỏ sót.
  - **Hộp thừa (False Positive):** Đã xóa bỏ các hộp nhiễu do điểm phản xạ mặt đường tạo ra.

---

## 4. Kết quả Review / QC Bài của Thành viên khác
- **Job QC được giao:** [Điền ID job được phân công review hoặc ghi "Không áp dụng do làm độc lập"]
- **Các loại lỗi ghi nhận trên bài của tác giả (nếu có):**
  - Không có (thực hiện theo hình thức cá nhân/đơn lẻ).

---

## 5. Đánh giá và Nhận xét Cá nhân
- **Lê Vĩnh Hưng:** Quá trình vận hành mô hình trên Windows 11 (qua WSL2/Docker) diễn ra ổn định. Việc rà soát và sửa pre-label giúp hiểu rõ hơn về cách PointPillars tạo dự đoán 3D và các điểm mù thường gặp của mô hình LiDAR. Tuân thủ tuyệt đối quy định bảo mật, không lưu trữ hay phát tán dữ liệu thô ra ngoài phạm vi quy định của bài lab.