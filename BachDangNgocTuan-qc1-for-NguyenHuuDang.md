# Phiếu QC 1 · Kiểm chéo lô phần tử đường Road v1.0

## 1. Thông tin chung
- **Học viên kiểm tra (Reviewer):** Bạch Đăng Ngọc Tuấn (Mã: 2A202603314)
- **Học viên được kiểm tra (Annotator):** Nguyễn Hữu Đăng (Mã: 2A202602710 / NguyenHuuDang)
- **Bộ dữ liệu kiểm tra:** 6 ảnh Front camera (BDD100K): slot A01 đến A06 (trích từ ront_dang/annotations.xml)
- **Ngày kiểm tra:** 20/11/2026
- **Quyết định cuối cùng:** **REWORK (Làm lại)**

---

## 2. Bảng lỗi theo ảnh (A01 – A06)

| Ảnh | Đối tượng | Lỗi phát hiện | Phân loại lỗi (Severity) | Mã lỗi QC | Mô tả chi tiết & Hướng dẫn sửa |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **A01** | lane | Thiếu vạch kẻ làn L1 | Critical | QC1-02 | Xe đang chạy trên làn rõ ràng nhưng không vẽ vạch phân cách làn bên trái (L1). Cần vẽ bổ sung polyline L1 từ dưới lên. |
| **A01** | lane | Polyline vẽ ngược hướng | Major | QC1-04 | Vạch R1 vẽ từ xa về gần ({start} < y_{end}$). Cần đảo ngược thứ tự các điểm để $ giảm dần (từ dưới lên trên). |
| **A01** | drivable | Drivable lấn vào vỉa hè | Major | QC1-06 | Polygon mặt đường ăn sâu qua gờ mép vỉa hè bên phải > 15px. Cần thu gọn lại đúng mép đường. |
| **A02** | 	raffic_sign | Bỏ sót biển báo tốc độ | Critical | QC1-08 | Có biển báo hạn chế tốc độ trên cột bên phải cao > 15px nhưng không được gán nhãn bbox. |
| **A02** | lane | Sai thuộc tính style | Major | QC1-03 | Vạch R1 là nét đứt (dashed) nhưng gán nhãn nhầm thành solid. Cần đổi style=dashed. |
| **A03** | 	raffic_light | Bounding box quá rộng | Minor | QC1-09 | Hộp bounding box đèn tín hiệu giao thông dư > 5px ở phía trên và bên trái. Cần siết chặt viền box. |
| **A03** | lane | Gán nhãn thừa L2 | Major | QC1-05 | Làn đối diện bị gán nhầm là L2 cùng chiều. Cần đổi sang position=other hoặc xóa nếu không thuộc phần đường xe chạy. |
| **A04** | drivable | Thiếu vùng rẽ nhánh | Major | QC1-07 | Ngã rẽ bên phải đủ điều kiện xe chạy nhưng không vẽ polygon lternative. Cần bổ sung polygon với rea_type=alternative. |
| **A05** | lane | Vẽ vạch ảo tại ngã tư | Critical | QC1-01 | Mặt đường ngã tư bị mòn hoàn toàn không có vạch nhưng vẫn vẽ polyline ước lượng (vi phạm quy tắc QC1-01: không bịa vạch). |
| **A06** | crosswalk | Thiếu vạch người đi bộ | Major | QC1-06 | Vạch kẻ sang đường cho người đi bộ nhìn thấy rõ nhưng không vẽ polygon crosswalk. Cần khoanh vùng toàn bộ cụm vạch. |

---

## 3. Tổng hợp thống kê lỗi

- **Tổng số nhãn đã kiểm tra:** 48 đối tượng
- **Số lỗi Critical (Lỗi nghiêm trọng):** **3** (Vượt ngưỡng cho phép: Cho phép tối đa 0)
- **Số lỗi Major (Lỗi chính):** **5** (Tỷ lệ:  / 48 = 10.4\%$ — Vượt ngưỡng cho phép 5%)
- **Số lỗi Minor (Lỗi nhỏ):** **1**

---

## 4. Quyết định & Đề xuất hành động

- [ ] **Release (Duyệt bàn giao):** Đạt chuẩn.
- [ ] **Hold (Tạm giữ):** Cần làm rõ một số điểm nghi vấn.
- [x] **Rework (Yêu cầu làm lại):** Bắt buộc làm lại.

### Lý do quyết định:
Lô kiểm tra của bạn Nguyễn Hữu Đăng vi phạm nghiêm trọng ngưỡng chất lượng QC 1:
1. Có **3 lỗi Critical** (trong đó có lỗi bịa đặt vạch kẻ không tồn tại ở A05 và bỏ sót vạch cơ bản L1 ở A01, biển báo ở A02).
2. Tỷ lệ lỗi Major đạt **10.4%** (gấp đôi trần cho phép là 5.0%).

### Hướng dẫn sửa chữa cho bạn Đăng:
1. Tải lại ảnh A05, xóa bỏ polyline ảo không có trên mặt đường.
2. Kiểm tra lại toàn bộ hướng vẽ polyline (bắt buộc vẽ từ dưới lên trên, điểm gần xe vẽ trước, điểm xa vẽ sau).
3. Bổ sung các vạch kẻ L1 và biển báo còn sót ở A01, A02, A06 trước khi export phiên bản Revision 2.
