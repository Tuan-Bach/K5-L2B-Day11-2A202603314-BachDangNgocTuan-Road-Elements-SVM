# Báo cáo cá nhân — Ngày 11
Họ tên: Bạch Đăng Ngọc Tuấn               Mã học viên: 2A202603314  
Phiên bản CVAT (Help → About): Server 2.81.0, Core 17.5.0, UI 2.81.0  
Guideline: Road v1.0    Lần nộp (`revision` trong manifest): 1  
Thời điểm export (ngày giờ trên CVAT): 21/11/2026 08:45 UTC+7    Số lần nộp lại sau Rework: 0  

## 1. Kiểm project
| Mục | Đúng như guideline Road v1.0? | Ghi chú |
| --- | --- | --- |
| 6 label, đúng kiểu | Đúng | `lane` (polyline), `road_curb` (polyline), `crosswalk` (polygon), `drivable` (polygon), `traffic_light` (rectangle), `traffic_sign` (rectangle) |
| Thuộc tính và giá trị | Đúng | Đầy đủ `position` (L1, R1, L2, R2, other), `style`, `color`, `kind`; `area_type` (direct, alternative); `edge_zone`, `facing`, `group`, `color`, `type` |
| 4 tag ảnh | Đúng | Đủ 4 tag ảnh: `camera`, `timeofday`, `weather`, `source` |
Cách kết thúc polyline trên bản CVAT này: Nhấp đúp chuột trái (Double click) hoặc phím tắt `N` (hoặc bấm biểu tượng dấu tích xanh Done).  
Cách đặt tag ảnh trên bản CVAT này: Chọn tab Objects → Tags ở cột phải, chọn nhãn tag và giá trị tương ứng (hoặc nạp đồng loạt qua API/XML).  

## 2. Số lượng đã gán
| Task | Ảnh | lane | road_curb | crosswalk | drivable | traffic_light | traffic_sign |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| front | 12 | 28 | 14 | 5 | 27 | 20 | 33 |
| front-extra (đã làm 4 / 4) | 4 | 11 | 2 | 2 | 8 | 7 | 12 |
| fisheye | 8 | 7 | 13 | 7 | 7 | 4 | 2 |
| fisheye-extra (đã làm 4 / 4) | 4 | 3 | 4 | 4 | 2 | 0 | 0 |

## 3. Bảng ca khó
| Ảnh | Nhãn | Phân vân giữa | Đã chọn | Lý do |
| --- | --- | --- | --- | --- |
| A05 | `lane` | Có nên vẽ L1/R1 ước lượng hay bỏ trống | Bỏ trống vạch kẻ | Mặt đường ngã tư đường phố mòn hoàn toàn, không có vạch sơn thực tế. Tuân thủ QC1-01 (không bịa vạch). |
| B01 | `drivable` | Kéo hết đáy ảnh hay dừng ở cản xe | Dừng sát mép nắp ca-pô | Camera mắt cá góc rộng nhìn thấy phần kim loại của đầu xe, drivable chỉ tính phần mặt đường nhựa xe lăn bánh được. |
| B05 | `lane` | Gán `position=L1` hay `other` | `other` | Camera gắn ở gương chiếu hậu sườn xe (MVL) nhìn ngang, theo quy tắc bắt buộc của guideline camera hai bên phải gán `position=other`. |

## 4. Phiếu QC 1 nhận được
Bạn kiểm lô của tôi: Nguyễn Hữu Đăng (NguyenHuuDang)  Quyết định nhận được: Rework (đã sửa)  
| Mã lỗi | Số lỗi | Đồng ý? | Đã sửa? |
| --- | ---: | --- | --- |
| QC1-04 (Polyline ngược) | 2 | Đồng ý | Đã sửa đảo chiều từ dưới lên trên (y giảm dần) |
| QC1-02 (Thiếu tag A10) | 1 | Đồng ý | Đã bổ sung đủ 4 tag |
| QC1-03 (Lane sườn xe) | 5 | Đồng ý | Đã chuyển toàn bộ lane sườn sang position=other |
| Row-anchor A01 | 1 | Đồng ý | Đã kéo vạch R1 chạm đáy ảnh y=720.0 |

## 5. Kiểm file export
| File | Mở lại được? | Số shape ảnh 1 (job / file) | Số shape ảnh 2 (job / file) | Tag camera có trong XML? |
| --- | --- | --- | --- | --- |
| `BachDangNgocTuan-front.zip` | Có | 13 (job) / 13 (file) | 9 (job) / 9 (file) | Có (`front`) |
| `BachDangNgocTuan-fisheye.zip` | Có | 5 (job) / 5 (file) | 8 (job) / 8 (file) | Có (`fisheye_front`, `fisheye_rear`, ...) |

## 6. Ảnh chụp màn hình
1. **Tab Labels của project:**  
![alt text](image-4.png)
2. **Một ảnh camera trước đã gán đủ (làn, vùng lái, đèn/biển):**  
![alt text](image-3.png)
3. **Một ảnh fisheye đã gán, phóng to đoạn polyline cong:**  
![alt text](image-1.png)
1. **Một đoạn XML có `<polyline label="lane">`:**  
![alt text](image-2.png)
## 7. Tự đánh giá
- **Lỗi bạn mắc nhiều nhất hôm nay (theo mã QC1-xx), và cách tránh ở Ngày 20:**  
  Lỗi vẽ ngược hướng polyline (`QC1-04`) và gán nhầm position của camera sườn xe (`QC1-03`). Cách tránh: Luôn ghi nhớ quy tắc trục $y$ trong ảnh: điểm gần xe nhất ở dưới đáy ảnh ($y$ lớn nhất) phải vẽ trước, kéo dần ra xa ($y$ nhỏ dần); camera hai bên sườn chỉ gán `position=other`.
- **Nhãn của bạn đi vào model ở đâu? Chọn một lỗi đã sửa và nói nó làm model học sai thế nào:**  
  Nhãn `lane` đi vào module phát hiện làn đường (Lane Detection / Row-anchor). Nếu để lỗi polyline vẽ ngược hoặc dừng trước mép ảnh ($y=719.1$ thay vì chạm $y=720$), model sẽ dự đoán hàng pixel sát đầu xe là "không có làn" (`None`), dẫn đến tính năng Giữ làn đường khẩn cấp (LKA / Emergency Lane Keeping) hiểu nhầm rằng xe đã mất dấu vạch kẻ ở cự ly gần và ngắt hỗ trợ đánh lái đột ngột.

## 8. (Tùy chọn, buffer) Từ polyline đến đích row-anchor
| y | 720 | 680 | 640 | 600 | 560 |
| --- | ---: | ---: | ---: | ---: | ---: |
| x của chúng tôi | 712.0 | 654.9 | 597.8 | 540.7 | 485.0 |
| x của bạn kia | không có làn | 650.2 | 595.1 | 538.4 | 482.6 |

**Trả lời 3 câu hỏi:**
1. *Năm số x đó chính là đích mà một model row-anchor học cho vạch này. Nếu bạn dừng polyline sớm 40 px, hàng nào đổi thành "không có làn"?*  
   **Trả lời:** Nếu dừng sớm 40px (tức là polyline chỉ kéo xuống đến $y = 680$ thay vì $720$), thì hàng $y = 720$ sẽ đổi thành `"không có làn"`.
2. *So với bạn được kiểm (cùng ảnh): ở hàng 720 và hàng 560, hai bạn lệch nhau bao nhiêu pixel? Lệch ở hàng nào ảnh hưởng LKA nhiều hơn (slide 25)?*  
   **Trả lời:** Ở hàng 720 lệch nhau hoàn toàn (một bên có tọa độ 712.0, một bên bị thiếu `"không có làn"`). Ở hàng 560 lệch nhau $|485.0 - 482.6| = 2.4\text{ px}$. Lệch ở hàng 720 ảnh hưởng đến LKA nhiều hơn rất nhiều vì đây là vùng sát bánh xe và mũi xe nhất, quyết định trực tiếp đến việc tính sai số góc lái tức thời (lateral deviation error) của bộ điều khiển xe tự hành.
3. *Nếu polyline vẽ từ xa về gần (ngược quy tắc 2), cách tính trên có đổi không? Script nào sẽ gặp khó?*  
   **Trả lời:** Về mặt toán học tìm giao điểm đoạn thẳng thì giá trị $x$ không đổi, nhưng cấu trúc dữ liệu lưu trong mảng điểm bị đảo lộn. Các script huấn luyện mô hình tuần tự (RNN/LSTM/Transformer autoregressive hoặc nội suy spline đường cong) và script kiểm thử tuần tự sẽ gặp lỗi vì kỳ vọng thứ tự điểm đi từ gần ra xa.
