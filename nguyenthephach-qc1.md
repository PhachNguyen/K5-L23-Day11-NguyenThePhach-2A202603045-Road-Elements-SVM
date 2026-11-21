# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): Nguyen Thế Phách  
Người kiểm (học viên): Nguyễn Thế Phách
Ngày: 2026-11-21  
Phiên bản guideline: Road v1.0  
File được kiểm: `nguyenthephach-front.zip`, `nguyenthephach-fisheye.zip` (revision 1)  
Phạm vi lint: 28 ảnh; không phải lấy mẫu thủ công. Lint không xác nhận hình học/nhãn đúng với ảnh.

## Tổng hợp cảnh báo lint theo mã

| Mã                                   | Loại lỗi                              | Số cảnh báo | Mức                 | Ghi chú                                                                                                                                   |
| ------------------------------------ | ------------------------------------- | ----------: | ------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| QC1-01 tag camera                    | sai thuộc tính / bỏ sót               |           0 | nặng                | Không có cảnh báo lint.                                                                                                                   |
| QC1-02 đủ L1, R1                     | bỏ sót                                |           6 | nặng                | A05 thiếu L1/R1; A06 thiếu R1; A09 thiếu L1; A13 và A14 thiếu R1. Coach cần xác nhận nếu vạch không thấy được.                            |
| QC1-03 position                      | sai thuộc tính / thừa                 |           9 | nặng                | B05 (2), B06 (2), B07 (3), B08 (1), B10 (1): lane camera bên trái/phải cần `position=other`.                                              |
| QC1-04 tâm vạch, chiều, điểm dừng    | sai phạm vi / bỏ sót                  |           1 | chính               | A10 có polyline lane bị cảnh báo hướng điểm đầu/cuối.                                                                                     |
| QC1-05 vạch đứt, che                 | sai phạm vi / sai thuộc tính          |           9 | chính               | A06 (1), A08 (1), A11 (1), A12 (2), A13 (1), B03 (1), B06 (1), B07 (1): kiểm tra các polyline cùng position có phải một vạch đứt bị tách. |
| QC1-06 style, color, kind            | sai thuộc tính                        |           0 | chính               | Không có cảnh báo lint.                                                                                                                   |
| QC1-07 vùng lái                      | sai phạm vi / bỏ sót / thừa           |           0 | chính               | Không có cảnh báo lint.                                                                                                                   |
| QC1-08 đèn, màu                      | bỏ sót / sai phạm vi / sai thuộc tính |           1 | nhẹ theo gợi ý lint | A15 box đèn thấp hơn 8 px; tự kiểm, không bắt buộc sửa.                                                                                   |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính                        |           0 | chính               | Không có cảnh báo lint.                                                                                                                   |
| QC1-10 hình in, đủ biển              | bỏ sót / sai phạm vi                  |           0 | chính               | Không có cảnh báo lint.                                                                                                                   |
| QC1-11 fisheye                       | sai phạm vi / sai thuộc tính          |          22 | chính               | B02 (5), B03 (7), B04 (2), B05 (1), B06 (1), B07 (2), B09 (3), B10 (1): xem lại polyline theo cung và edge_zone của đèn/biển.             |
| QC1-12 file                          | lỗi file                              |           1 | nhẹ                 | Một điểm lặp liền trên lane A08; kiểm tra và xóa nếu đúng là click lặp.                                                                   |

## Danh sách cảnh báo nặng cần kiểm tra

|   # | Mã     | Ảnh | Nhãn (label, id) | Mức  | Mô tả lint                                                      |
| --: | ------ | --- | ---------------- | ---- | --------------------------------------------------------------- |
|   1 | QC1-02 | A05 | lane             | nặng | Thiếu L1 và R1; xác nhận trực quan nếu thực sự không thấy vạch. |
|   2 | QC1-02 | A06 | lane             | nặng | Thiếu R1; xác nhận trực quan nếu thực sự không thấy vạch.       |
|   3 | QC1-02 | A09 | lane             | nặng | Thiếu L1; xác nhận trực quan nếu thực sự không thấy vạch.       |
|   4 | QC1-02 | A13 | lane             | nặng | Thiếu R1; xác nhận trực quan nếu thực sự không thấy vạch.       |
|   5 | QC1-02 | A14 | lane             | nặng | Thiếu R1; xác nhận trực quan nếu thực sự không thấy vạch.       |
|   6 | QC1-03 | B05 | lane #3, #4      | nặng | Hai lane camera bên cần `position=other`.                       |
|   7 | QC1-03 | B06 | lane #0, #1      | nặng | Hai lane camera bên cần `position=other`.                       |
|   8 | QC1-03 | B07 | lane #3, #4, #5  | nặng | Ba lane camera bên cần `position=other`.                        |
|   9 | QC1-03 | B08 | lane #1          | nặng | Lane camera bên cần `position=other`.                           |
|  10 | QC1-03 | B10 | lane #2          | nặng | Lane camera bên cần `position=other`.                           |

## Ca mơ hồ cần người kiểm/coach xác nhận

| Ảnh                                    | Câu hỏi cho lead                                                                     | Lời đáp  |
| -------------------------------------- | ------------------------------------------------------------------------------------ | -------- |
| A05, A06, A09, A13, A14                | Các vạch L1/R1 lint báo thiếu có thật sự không nhìn thấy trong ảnh không?            | Chưa có. |
| A06, A08, A11, A12, A13; B03, B06, B07 | Các lane cùng position là các đoạn vạch đứt riêng biệt hay một polyline bị chia nhỏ? | Chưa có. |
| B02–B10                                | Các đường fisheye đã bám cung đủ sát chưa; đèn/biển ở rìa có cần `edge_zone` không?  | Chưa có. |

## Quyết định

Lint ghi nhận 15 cảnh báo nặng, 32 cảnh báo chính và 2 cảnh báo nhẹ. Đây là cảnh báo máy, chưa được xác nhận thành số lỗi QC thủ công. Theo luật của phiếu, nếu người kiểm xác nhận còn lỗi nặng thì quyết định là **Rework**; riêng QC1-02 chỉ được miễn khi coach xác nhận ảnh thật sự không thấy vạch và ghi rõ lý do.

Số lỗi thủ công: Chưa xác định.  
Tỉ lệ lỗi chính / số nhãn đã kiểm: Chưa xác định (chưa thực hiện kiểm chéo mẫu).  
Ca chờ lead: 3 nhóm câu hỏi ở trên.  
Quyết định chính thức (Release / Hold / Rework): Hold
