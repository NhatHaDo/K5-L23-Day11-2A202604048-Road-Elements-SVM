# Báo cáo cá nhân — Ngày 11
Họ tên: Đỗ Thị Huyền               Mã học viên: 2A202604048  
Phiên bản CVAT (Help → About): CVAT self-hosted chạy local bằng Docker (`localhost:8080`), phiên bản: __ *(điền theo Help → About)*  
Guideline: Road v1.0    Lần nộp (`revision` trong manifest): 1  
Thời điểm export (ngày giờ trên CVAT): 21/11/2026, khoảng 08:03    Số lần nộp lại sau Rework: 0  

Ghi chú: tài khoản trên CVAT của lớp chưa được gán project, và app.cvat.ai không được dùng cho dữ liệu lớp, nên tôi tạo project `d11-road-dohuyen` trên CVAT chạy local (ảnh không rời máy). Bốn task được export riêng rồi gộp front + front-extra và fisheye + fisheye-extra thành hai file nộp.

## 1. Kiểm project
| Mục | Đúng như guideline Road v1.0? | Ghi chú |
| --- | --- | --- |
| 6 label, đúng kiểu | Có | lane, road_curb (polyline); crosswalk, drivable (polygon); traffic_light, traffic_sign (rectangle) |
| Thuộc tính và giá trị | Có | Dán tab Raw từ `configs/road_v1_labels.json` (sinh bởi `road_lab.taxonomy`) |
| 4 tag ảnh | Có | camera, timeofday, weather, source; mỗi label Tag có thuộc tính select `value` |
Cách kết thúc polyline trên bản CVAT này: bấm phím **N** (Esc để hủy đường đang vẽ).  
Cách đặt tag ảnh trên bản CVAT này: công cụ **Tag** ở thanh trái → chọn label → bấm nút **+** → mở Details của tag trong bảng Objects và sửa `value` (CVAT tự điền giá trị đầu danh sách).  

## 2. Số lượng đã gán
| Task | Ảnh | lane | road_curb | crosswalk | drivable | traffic_light | traffic_sign |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| front | 12 | 28 | 12 | 7 | 20 | 30 | 29 |
| front-extra (đã làm 4 / 4) | 4 | 8 | 4 | 6 | 8 | 17 | 14 |
| fisheye | 8 | 10 | 7 | 12 | 5 | 0 | 6 |
| fisheye-extra (đã làm 4 / 4) | 4 | 0 | 4 | 4 | 1 | 0 | 1 |

## 3. Bảng ca khó
| Ảnh | Nhãn | Phân vân giữa | Đã chọn | Lý do |
| --- | --- | --- | --- | --- |
| A02 | tag timeofday | day / dusk | day | Nắng chiều thấp, bóng dài nhưng trời còn sáng rõ |
| A03 | lane R1 | dừng ở vệt đầu tiên thấy được / nối xuống đầu xe | Nối xuống, bật occluded | Đoạn gần sơn mờ không thấy; checkpoint nêu A03 có ca occluded |
| A03 | lane L1 (vàng) | kind single / double | single, vẽ trên nét trong | Gần đầu xe có 2 nét vàng nhưng nét ngoài tách ra làm viền vùng kẻ sọc, không phải vạch đôi song song suốt |
| A04 | lane R2 | single / double | double | Sát làn xe đạp có 2 vạch trắng liền song song làm vùng đệm |
| A04 | road_curb | không vẽ / vẽ | Vẽ hai bên | Mép đường thật là bó vỉa sau làn xe đạp (phải) và vỉa hè trái; chỗ đó không có sơn |
| A05, A07 (L1), A09 (R1), A14 (R1) | lane | vẽ thêm vạch / để trống | Để trống, chờ coach xác nhận miễn QC1-02 | A05 đường không kẻ vạch; A07 bên trái là dải bê tông; A09, A14 bên phải là bó vỉa, không có sơn |
| A06 | lane R1, drivable | vẽ R1 theo hàng cột / không vẽ | Không vẽ R1; ranh direct / alternative theo hàng cột cầu | Dưới cầu cạn, bên phải làn là cột, không có sơn; vùng sau cột không tính vùng lái |
| A08 | lane | gán vạch nằm ngang bên trái (y≈360) / bỏ | Bỏ | Vạch gần như nằm ngang, thuộc đường cắt ngang ở ngã tư, không phải làn của mình |
| A10 | lane R1 | dừng trước hình dán / nối qua | Nối qua, bật occluded | Đoạn giữa bị hình dán và xe che, vạch tiếp tục ở hai đầu |
| A13 | tag weather | overcast / rain | rain | Có giọt mưa trên kính lái, đang mưa |
| B02 | road_curb | mép trên / mép dưới của dải tối giữa vỉa hè và vạch ngựa vằn | Mép dưới (giáp mặt đường), 7 điểm theo cung | Dải tối là đá bó vỉa; mép đường là chỗ đá bó gặp mặt nhựa |
| Nhiều ảnh | traffic_light / traffic_sign < 8 px | xóa / giữ | Giữ | Guideline không bắt buộc box dưới 8 px; lint chỉ báo mức nhẹ |

## 4. Phiếu QC 1 nhận được
Bạn kiểm lô của tôi: __   Quyết định nhận được: __  
| Mã lỗi | Số lỗi | Đồng ý? | Đã sửa? |
| --- | ---: | --- | --- |
|  |  |  |  |

## 5. Kiểm file export
| File | Mở lại được? | Số shape ảnh 1 (job / file) | Số shape ảnh 2 (job / file) | Tag camera có trong XML? |
| --- | --- | --- | --- | --- |
| dohuyen-front.zip (16 ảnh, sha256 f5c8e1c7…) | Có, `road_check lint` đọc được | A01: __ / 9 | A02: __ / 6 | Có, 16/16 ảnh đủ 4 tag |
| dohuyen-fisheye.zip (12 ảnh, sha256 95648ed6…) | Có, `road_check lint` đọc được | B01: __ / 3 | B02: __ / 4 | Có, 12/12 ảnh đủ 4 tag |

Manifest `dohuyen-manifest.json`: `revision = 1`, `contains_images = false` cho cả hai file; lint lúc tạo: nặng 6, chính 0, nhẹ 11 (6 nặng là QC1-02 ở các ảnh không có vạch, chờ coach xác nhận; 11 nhẹ là box dưới 8 px).

## 6. Ảnh chụp màn hình
1. Tab Labels của project. *(chèn ảnh)*
2. Một ảnh camera trước đã gán đủ (làn, vùng lái, đèn/biển). *(chèn ảnh, ví dụ A01)*
3. Một ảnh fisheye đã gán, phóng to đoạn polyline cong. *(chèn ảnh)*
4. Một đoạn XML có <polyline label="lane">. *(chèn ảnh)*

## 7. Tự đánh giá
Lỗi bạn mắc nhiều nhất hôm nay (theo mã QC1-xx), và cách tránh ở Ngày 20:  
Nhiều nhất là **QC1-01** (cả 12 ảnh fisheye để tag `camera = front`) và **QC1-03** (lane giữ giá trị mặc định `L1` của CVAT: hai vạch cùng L1 ở A04, A14, A16; lane camera hai bên ở B06–B08 không phải `other`). Tiếp theo là QC1-04 (A08 vẽ từ xa về gần) và vạch vàng đôi vẽ thành hai polyline (A04, A14). Tất cả đã sửa trước khi nộp sau khi chạy `lint`. Cách tránh ở Ngày 20: vẽ xong mỗi nhãn thì mở Details sửa ngay, không để giá trị mặc định; với ảnh fisheye đọc hậu tố tên file (FV/RV/MVL/MVR) trước khi đặt tag; chạy `lint` sau mỗi vài ảnh thay vì đợi cuối buổi.  

Nhãn của bạn đi vào model ở đâu? Chọn một lỗi đã sửa và nói nó làm model học sai thế nào:  
Polyline `lane` kèm `position` là đích cho model phát hiện làn (ví dụ dạng row-anchor) và cho phần xác định làn của xe mình, đầu vào của LKA. Lỗi đã sửa ở A16 (vạch đứt bên phải gán `L1` thay vì `R1`) dạy model rằng vạch bên phải xe là biên trái của làn: model sẽ ghép sai biên làn, tâm làn tính ra lệch hẳn sang phải, LKA có thể đánh lái về sai vị trí. Lỗi tag camera ở ảnh fisheye còn làm ảnh rơi vào sai nhóm dữ liệu: ảnh méo của camera fisheye bị đưa vào tập huấn luyện của camera trước, model học hình dạng vạch cong như vạch thẳng của camera trước.  

## 8. (Tùy chọn, buffer) Từ polyline đến đích row-anchor
*(Không làm.)*
