# Báo cáo cá nhân — Ngày 11

Họ tên: Nguyen The Phach  
Mã học viên: 2A202603045  
Phiên bản CVAT: Chưa xác minh trên Help → About  
Guideline: Road v1.0  
Lần export trong manifest (`revision`): 1  
Thời điểm tạo manifest: 2026-11-21 04:32:04 UTC  
Số lần nộp lại sau Rework: Chưa xác nhận đã nộp/Rework

> Số liệu bên dưới được đối chiếu với hai ZIP hiện có và manifest revision 1. Lint kiểm tra định dạng và các quy tắc tự động, không xác nhận chất lượng hình học bằng cách so với ảnh/ground truth. Các mục cần kiểm tra trực tiếp hoặc thông tin từ người kiểm được đánh dấu chưa xác minh.

## 1. Kiểm project

| Mục                   | Đúng guideline Road v1.0?                                       | Ghi chú                                                                                       |
| --------------------- | --------------------------------------------------------------- | --------------------------------------------------------------------------------------------- |
| 6 label và kiểu hình  | Đúng trong XML export; project CVAT chưa xem trực tiếp          | lane/road_curb: polyline; crosswalk/drivable: polygon; traffic_light/traffic_sign: rectangle. |
| Thuộc tính và giá trị | Taxonomy trong XML khớp cấu hình repo; chưa xác minh UI project | Thuộc tính gồm position/style/color/kind, area_type, thuộc tính đèn và biển theo Road v1.0.   |
| 4 tag ảnh             | Đủ trong cả 28 ảnh                                              | camera, timeofday, weather, source; mỗi tag có thuộc tính `value`.                            |

Cách kết thúc polyline trên phiên bản CVAT này: Chưa xác minh trực tiếp; guide minh họa phím **N**.  
Cách đặt tag ảnh trên phiên bản CVAT này: Chưa xác minh trực tiếp; XML export có đủ bốn tag trên mỗi ảnh.

## 2. Số lượng đã gán

| Task                       | Số ảnh | lane | road_curb | crosswalk | drivable | traffic_light | traffic_sign |
| -------------------------- | -----: | ---: | --------: | --------: | -------: | ------------: | -----------: |
| front bắt buộc (A01–A12)   |     12 |   37 |        12 |         5 |       31 |            13 |           12 |
| front-extra (A13–A16)      |      4 |   12 |         2 |         6 |       11 |             6 |           10 |
| fisheye bắt buộc (B01–B08) |      8 |   14 |        15 |        14 |       18 |             3 |            1 |
| fisheye-extra (B09–B12)    |      4 |    2 |         6 |         6 |        7 |             0 |            1 |

Số shape được đếm từ hai ZIP. Tổng: 28 ảnh; front 16 ảnh, fisheye 12 ảnh. Manifest ghi đủ bốn tag cho mọi ảnh và `contains_images: false` cho cả hai ZIP.

## 3. Bảng ca khó cần tự kiểm

| Ảnh                              | Nhãn                    | Phân vân giữa                                              | Kết quả lint / việc cần làm                                                                |
| -------------------------------- | ----------------------- | ---------------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| A05, A06, A09, A13, A14          | lane                    | Thiếu L1/R1 hay ảnh thật sự không có vạch                  | Lint báo thiếu 6 vị trí L1/R1; xem ảnh và nhờ coach xác nhận trường hợp không thấy vạch.   |
| B05–B08, B10                     | lane                    | position theo làn hay `other`                              | 9 lane ở camera fisheye bên trái/phải bị báo cần `position=other`; kiểm và sửa thuộc tính. |
| A06, A08, A11–A13; B03, B06, B07 | lane                    | Vạch đứt bị tách thành nhiều polyline hay nhiều vạch riêng | Lint có 9 cảnh báo trùng position; đối chiếu ảnh để quyết định nối/tách đúng.              |
| B02–B10                          | lane/road_curb/đèn/biển | Polyline có bám cung; vật thể có thuộc vùng rìa            | Có 22 cảnh báo fisheye; kiểm đường cong và `edge_zone` bằng mắt.                           |

## 4. Phiếu QC 1 nhận được

Chưa có thông tin người kiểm hoặc Phiếu QC 1 kiểm chéo. Bản tổng hợp tự kiểm từ lint nằm ở [nguyenthephach-qc1-draft.md](nguyenthephach-qc1-draft.md); bản đó chưa thay thế phiếu kiểm chéo chính thức.

Lint hiện báo **15 nặng, 32 chính, 2 nhẹ**. Các mã: QC1-02 (6), QC1-03 (9), QC1-04 (1), QC1-05 (9), QC1-11 (22), QC1-08 (1 nhẹ), QC1-12 (1 nhẹ). Cảnh báo lint cần được kiểm trực quan trước khi ghi thành lỗi đã xác nhận.

## 5. Kiểm file export

| File                         | Mở lại được? | Số shape ảnh đầu / ảnh thứ hai trong ZIP | Tag camera có trong XML? |
| ---------------------------- | ------------ | ---------------------------------------: | ------------------------ |
| `nguyenthephach-front.zip`   | Có; 16 ảnh   |                                    8 / 6 | Có                       |
| `nguyenthephach-fisheye.zip` | Có; 12 ảnh   |                                   4 / 10 | Có                       |

Số shape trong CVAT job chưa đối chiếu trực tiếp; các số trên là số shape đọc từ XML trong file ZIP. Hai ZIP đang khớp manifest revision 1. Manifest ghi `contains_images: false` cho cả hai.

## 6. Ảnh chụp màn hình

Đã tạo hình minh họa bằng cách chồng nhãn trong XML export lên ảnh gốc. Đây là hình kiểm tra từ export, không phải ảnh chụp giao diện CVAT.

1. **Tab Labels của project:** chưa có ảnh chụp CVAT; cần chụp trực tiếp trong giao diện project.
2. **Ảnh front A01 có overlay nhãn:** [mở hình](report_evidence/02-front-A01-overlay.jpg).
3. **Ảnh fisheye B03 có overlay nhãn:** [mở hình](report_evidence/03-fisheye-B03-overlay.jpg).
4. **Đoạn XML lane lấy từ export thật:** [mở file](report_evidence/04-lane-polyline.xml).

## 7. Tự đánh giá

Các điểm cần ưu tiên tự kiểm theo lint là thuộc tính `position=other` cho lane ở camera hai bên và các polyline fisheye cần đi theo cung. Các trường hợp thiếu L1/R1 chỉ được miễn khi coach xác nhận ảnh thật sự không thấy vạch và ghi mã ảnh/lý do vào Phiếu QC 1.

Nếu lane thiếu hoặc sai thuộc tính/vị trí đi vào dữ liệu huấn luyện, model có thể học sai vị trí ranh giới làn và dự đoán không ổn định. Chưa có Phiếu QC kiểm chéo nên chưa thể kết luận lỗi thực tế nào xuất hiện nhiều nhất hoặc ra quyết định Release/Hold/Rework.

## 8. Buffer: row-anchor

Đã chạy `road_lab.rowanchor` trên `nguyenthephach-front.zip`, ảnh **A01**, polyline **L1** (`lane#3`). Tọa độ x nội suy từ polyline của tôi:

| y                        |             720 |             680 |             640 |             600 |             560 |
| ------------------------ | --------------: | --------------: | --------------: | --------------: | --------------: |
| x của tôi (px)           |           112.2 |           158.2 |           204.3 |           250.3 |           297.5 |
| x của bạn được kiểm (px) | Chưa có dữ liệu | Chưa có dữ liệu | Chưa có dữ liệu | Chưa có dữ liệu | Chưa có dữ liệu |

1. Nếu polyline kết thúc sớm hơn 40 px theo trục y, đầu gần xe sẽ dừng tại khoảng y=680 thay vì y=720. Khi đó hàng **y=720** không còn giao với polyline và kết quả sẽ là “không có làn”; các hàng 680–560 vẫn có thể được nội suy. Đây là hàng gần xe nhất nên việc mất tín hiệu tại đây ảnh hưởng đáng kể hơn tới ước lượng làn ở vùng gần xe.
2. Chưa có tọa độ của bạn được kiểm nên chưa thể tính độ lệch pixel tại y=720 và y=560. Sau khi có hai tọa độ đó, độ lệch lần lượt là `|x_tôi − x_bạn|` ở từng hàng. Thông thường sai lệch ở y=720 ảnh hưởng trực tiếp hơn đến điều khiển gần xe; đây là nhận định định tính, chưa phải phép đo trên cặp nhãn.
3. Đảo thứ tự các điểm không làm đổi giao điểm x-y của cùng một polyline: phép nội suy kiểm tra từng đoạn theo cả hai chiều. Tuy vậy, vẽ từ xa về gần vi phạm quy tắc gán nhãn của lab; checker có thể báo QC1-04 và pipeline/model phụ thuộc thứ tự điểm có thể học sai chiều.
