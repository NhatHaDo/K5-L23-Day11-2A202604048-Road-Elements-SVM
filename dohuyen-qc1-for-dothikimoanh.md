# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): Đỗ Thị Kim Oanh        Người kiểm (học viên): Đỗ Huyền (dohuyen)  
Ngày: 21/11/2026                          Phiên bản guideline: Road v1.0  
File được kiểm (tên + `revision` trong manifest): `label.zip` (một zip gồm `task1/annotations.xml` = front A01–A12 và `task2/annotations.xml` = fisheye B01–B08); không kèm manifest nên không có `revision`  
Số ảnh kiểm: 6 (+ 0 ảnh thêm, lô không có ảnh thêm)   Số nhãn đã kiểm (shape + tag): 72  

Ảnh được kiểm: A01, A04, A08, A12 (front) · B01, B07 (fisheye). Ngoài 6 ảnh mẫu, đã chạy `road_check lint` trên cả 20 ảnh để tham khảo (55 cảnh báo).

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 6 | 3 nặng + 3 nhẹ | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 10 | 0 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 19 | 6 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 27 | 6 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 19 | 1 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 19 | 4 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 21 | 3 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 8 | 0 | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 12 | 1 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 4 | 1 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 13 | 3 | chính |
| QC1-12 file | lỗi file | 2 | 1 nặng + 1 nhẹ | nhẹ / nặng |

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-03 | A01 | lane, điểm đầu (2,599) | nặng | Vạch trắng liền sát dải phân cách trái là L2, đang gán L1 (nhầm L1/L2) |
| 2 | QC1-06 | A01 | lane, điểm đầu (105,720) | chính | Vạch đứt bên trái xe (đúng là L1) nhưng `style = solid`, phải là `dashed` |
| 3 | QC1-04 | A01 | lane R1, điểm đầu (408,506) | chính | Vẽ từ xa về gần (điểm đầu ở xa) |
| 4 | QC1-06 | A01 | lane R1, điểm đầu (408,506) | chính | Vạch đứt bên phải xe nhưng `style = solid`, phải là `dashed` |
| 5 | QC1-04 | A01 | thiếu lane R2 | chính | Bỏ sót vạch vàng liền mép phải (R2 / solid / yellow) |
| 6 | QC1-07 | A01 | drivable direct, điểm đầu (0,563) | chính | Polygon `direct` nằm ở làn bên trái (giữa L2 và L1), không phải làn đang đi |
| 7 | QC1-07 | A01 | thiếu drivable | chính | Thiếu `direct` cho làn giữa (L1–R1) và `alternative` cho làn bên phải |
| 8 | QC1-09 | A01 | traffic_sign (553,409)-(605,479) | chính | Biển xanh chỉ hướng gán `group = prohibitory`, phải là `information` |
| 9 | QC1-10 | A01 | thiếu traffic_sign | chính | Bỏ sót biển xanh nhỏ ở xa (khoảng (431,462)-(453,489), cao ~27 px ≥ 8 px) |
| 10 | QC1-05 | A04 | lane, điểm đầu (19,556) | chính | Vạch vàng đôi vẽ thành 2 polyline riêng; phải là 1 polyline ở giữa, `kind = double` |
| 11 | QC1-06 | A04 | lane, điểm đầu (19,556) | chính | Nét vàng ngoài gán `color = white`; cả nét kia `kind = single` thay vì `double` |
| 12 | QC1-04 | A04 | lane R1, điểm đầu (602,321) | chính | Vẽ từ xa về gần |
| 13 | QC1-06 | A04 | lane R1, điểm đầu (602,321) | chính | Vạch trắng đứt bên phải xe gán `solid / yellow`, phải là `dashed / white` |
| 14 | QC1-04 | A04 | thiếu lane R2 | chính | Bỏ sót vạch trắng liền sát làn xe đạp (R2) |
| 15 | QC1-07 | A04 | thiếu drivable alternative | chính | Thiếu `alternative` cho làn cùng chiều giữa R1 và R2 (checkpoint A04) |
| 16 | QC1-03 | A08 | lane, điểm đầu (647,310) | nặng | Vạch đứt bên phải xe là R1, đang gán L1 (lint báo thiếu R1) |
| 17 | QC1-04 | A08 | lane, điểm đầu (647,310) | chính | Vẽ từ xa về gần |
| 18 | QC1-04 | A08 | lane R2, điểm đầu (762,314) | chính | Vẽ từ xa về gần |
| 19 | QC1-01 | A12 | tag camera | nặng | Ảnh không có tag nào; thiếu tag camera |
| 20 | QC1-01 | A12 | tag timeofday, weather, source | nhẹ | Thiếu 3 tag còn lại (tính 3 lỗi nhẹ) |
| 21 | QC1-01 | B01 | tag camera | nặng | `camera = front`, tên file `_FV` → phải là `fisheye_front` |
| 22 | QC1-12 | B01 | lane, điểm đầu (42,552) | nhẹ | Lane lưu dạng polygon 1387 điểm, phải là polyline |
| 23 | QC1-01 | B07 | tag camera | nặng | `camera = front`, tên file `_MVR` → phải là `fisheye_right` |
| 24 | QC1-03 | B07 | lane (66,674) | nặng | Camera hai bên: lane phải có `position = other`, đang là L1 |
| 25 | QC1-03 | B07 | lane (699,135) | nặng | Như trên |
| 26 | QC1-03 | B07 | lane (947,275) | nặng | Như trên |
| 27 | QC1-03 | B07 | lane (75,756) | nặng | Như trên |
| 28 | QC1-11 | B07 | lane (66,674), (947,275), (75,756) | chính | 3 lane chỉ có 2 điểm, nối thẳng; trên fisheye phải đặt điểm theo cung (tính 3 lỗi) |
| 29 | QC1-12 | toàn lô | label.zip | nặng | Không đúng đặc tả bàn giao: gửi 1 zip gộp thay vì `<tên>-front.zip` và `<tên>-fisheye.zip`; script chấm của coach tìm đúng tên file nên sẽ không thấy; thiếu manifest |

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| A08 | Hai vạch trắng bên trái gần như nằm ngang (L1 (51,354)→(478,279), L2 (0,320)→(436,275)) có phải vạch của đường cắt ngang ở ngã tư không? Nếu đúng thì không nên gán lane. Chưa tính lỗi. | |
| A12 | Có 2 lane cùng `L2` (một solid, một dashed ở mép trái); cần xem vạch dashed (0,537)→(175,484) có thuộc làn của mình không. Chưa tính lỗi. | |

## Quyết định
Lỗi nặng: 10   Lỗi chính: 19 / 72 nhãn = 26,4 %   Lỗi nhẹ: 4   Ca chờ lead: 2  
Quyết định (Release / Hold / Rework): **Rework**  
Lý do (theo luật của phiếu): còn 10 lỗi nặng (tag camera sai/thiếu ở A12, B01, B07; nhầm position ở A01, A08 và 4 lane camera hai bên ở B07; file bàn giao sai đặc tả), và tỉ lệ lỗi chính 26,4 % vượt ngưỡng 5 %. Một trong hai điều kiện đã đủ để Rework; 2 ca mơ hồ không đổi được quyết định nên không chọn Hold.

Gợi ý sửa nhanh: sửa tag camera cho toàn bộ ảnh B theo tên file (lint còn báo B02, B04, B05, B06, B08 cùng lỗi), đổi mọi lane ở B05–B08 thành `other`, kiểm lại chiều vẽ (lint báo 10 vạch vẽ từ xa về gần), rồi export đúng 2 file `<tên>-front.zip`, `<tên>-fisheye.zip` kèm manifest.

Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng. Ba loại này theo cách chia lỗi gán nhãn của ISO/IEC 5259-4 (mục 8.4.2); "sai thuộc tính" và "lỗi file" là khóa học thêm. Cách xếp mức: [thang mức lỗi](docs/qc_severity_road_v1.0.md).
