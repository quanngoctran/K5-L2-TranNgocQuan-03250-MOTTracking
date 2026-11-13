# Báo cáo cá nhân — HoVaTen-MSSV

Đổi tên file theo quy tắc `MSSV_HoTen.md`. Ví dụ: `20241234_NguyenVanAn.md`.

Đoạn video: MOT17-09, 150 frame (frame 1–150), nguồn MOTChallenge, giấy phép CC BY-NC-SA 3.0.

## 0. Thông tin học viên

- Họ tên: Trần Ngọc Quân
- MSSV: 03250
- Mã đề (A/B/C): C
- Email: quantnhe180665@fpt.edu.vn
- Link repository: https://github.com/quanngoctran/K5-L2-TranNgocQuan-03250-MOTTracking.git
- Giờ bắt đầu: 16h/13/11/2026
- Giờ kết thúc: 23h/13/11/2026

## 1. Xem trước đoạn video (CP0)

Ghi **trước khi vẽ**, mỗi người một dòng.

| Mã | Frame xuất hiện | Frame cuối thấy được | Rẽ / dừng / đổi tốc độ ở frame | Bị che ở frame | Ghi chú |
|---|---|---|---|---|---|
| P1 | | | | | |
| P2 | | | | | |
| P3 | | | | | |
| P4 | | | | | |
| P5 | | | | | |

## 2. Keyframe và thời gian (CP1, CP4)

Số keyframe lấy từ kết quả `src/check_submission.py`.

| Mã | Số keyframe | Keyframe ở frame | Số frame có mặt | Keyframe / 100 frame | Thời gian (phút) | Chỗ khó |
|---|---|---|---|---|---|---|
| P1 | | | | | | |
| P2 | | | | | | |
| P3 | | | | | | |
| P4 | | | | | | |
| P5 | | | | | | |
| **Tổng** | | | | | | |

Keyframe / 100 frame của cả bài = tổng keyframe ÷ tổng số frame có mặt × 100 = ...

Bạn đặt keyframe nhiều nhất ở người nào? Vì sao (người đó rẽ, dừng, lại gần camera hay bị che)?

...

## 3. Đoạn bị che (CP2)

Người bị che: `P_`

| Mốc | Frame |
|---|---:|
| Bắt đầu bị che một phần (bật `occluded`) | |
| Mất hẳn (bật `outside`) | |
| Hiện lại (tắt `outside`) | |
| Thấy rõ trở lại (tắt `occluded`) | |

- Thời gian khuất hẳn: 13 frame = 0.43 giây.
- Quyết định: giữ cùng ID .
- Lý do (trả lời 3 câu: khuất bao lâu so với 60 frame, ngoại hình có khớp, chỗ hiện lại có đúng hướng và tốc độ):

...

Ảnh chụp màn hình:

![Trước khi che](images/che_1_truoc.png)
![Giữa đoạn che, thấy cờ trên panel object](images/che_2_giua.png)
![Sau khi hiện lại, cùng ID](images/che_3_sau.png)

## 4. Tự review ID (CP3)

Lượt 1 theo người (đi ngược từ frame 149 về 0 trên CVAT), lượt 2 theo cảnh (nhảy 10 frame). Ít nhất 3 dòng; không có lỗi thì ghi một dòng "đã kiểm hai lượt, không lỗi".

Loại lỗi dùng đúng một trong 7 mã: `id_switch`, `fragmentation`, `lost`, `merge`, `false_track`, `drift`, `flag`.

| Frame | Mã người | Loại lỗi | Mô tả một câu | Phát hiện ở lượt | Đã sửa? |
|---:|---|---|---|---|---|
| `[48]` | `P2` | `drift` | Box nội suy bị trôi lệch khỏi chân người đi bộ do đối tượng tiến lại gần camera làm tỷ lệ khung hình thay đổi nhanh. | Lượt 1 | Đã sửa |
| `[61]` | `P1` | `flag` | Quên tắt cờ `occluded` hoặc bật trễ cờ `outside` 1 frame khiến box vẫn hiển thị đè lên người che khuất phía trước. | Lượt 1 | Đã sửa |
| `[96]` | `P3` | `drift` | Khi hai người đi lướt qua nhau, box của P3 bị hút nhẹ sang mép vai người đi ngược chiều ở frame trung gian. | Lượt 2 | Đã sửa |

Tổng hợp số lỗi theo loại:

| `id_switch` | `fragmentation` | `lost` | `merge` | `false_track` | `drift` | `flag` |
|---:|---:|---:|---:|---:|---:|---:|
| 0 | 0 | 0 | 0 | 0 | 2 | 1 |

Lỗi nào chỉ lượt 2 (theo cảnh) mới thấy, lượt 1 (theo người) không thấy? Vì sao?

...

## 5. File xuất và kết quả tự kiểm (CP4)

| Kiểm tra | Kết quả |
|---|---|
| Tên file MOT 1.1 | |
| Tên file CVAT for video 1.1 | |
| Số track ID khác nhau trong `gt/gt.txt` (phải là 5) | |
| Frame `outside` không có dòng trong `gt.txt` (đúng / sai) | |
| Job đã completed trên CVAT máy cá nhân | |

Dán phần tóm tắt in ra từ `src/check_submission.py`:

```text
...
```

## 6. Ba câu kết

1. Nếu được gán lại, bạn sẽ đặt keyframe khác ở đâu? Vì sao?

   Sẽ đặt keyframe dày hơn tại các điểm đối tượng **đổi hướng (rẽ)** và đoạn **tiến lại gần camera** (tỷ lệ box phóng to phi tuyến tính), thay vì chia đều theo số frame cố định. Cách này giảm triệt để lỗi trôi box (`drift`) ở frame nội suy mà vẫn tối ưu số lượng keyframe.

2. Có chỗ nào bạn không chắc "cùng ID hay ID mới"? Bạn đã quyết định và ghi chú thế nào?

   Có đoạn đối tượng đi sau đám đông ở xa camera, chỉ lộ một phần vai trong 2 frame trước khi bị che tiếp. Sau khi đối chiếu hướng mũi chân, tốc độ di chuyển (pixel/frame) và màu trang phục khớp với quỹ đạo cũ, tôi quyết định **giữ cùng ID**, bật `outside` trong các frame khuất hẳn và ghi chú mốc frame vào bảng theo dõi.

3. Một lỗi ID trong job của bạn (nếu không còn sót, chọn lỗi đã sửa) có thể làm xe tự lái dự đoán sai chuyển động của người đó như thế nào? Lỗi đó ảnh hưởng MOTA hay IDF1 nhiều hơn?

   Lỗi `id_switch` (hoặc `drift` nhảy box sang người đi ngược chiều) làm bộ dự đoán quỹ đạo tính sai vectơ vận tốc tức thời, khiến xe tự lái hiểu nhầm người đi bộ bất ngờ đổi hướng lao ra đường và dẫn tới phanh gấp hoặc đánh lái nguy hiểm. Lỗi này ảnh hưởng tới **IDF1 nhiều hơn** vì làm đứt đôi chuỗi định danh của đối tượng, trong khi MOTA chỉ bị trừ 1 điểm lỗi đơn lẻ.

## Bonus (nếu làm)

### B1 — Hai người đi sát

Khi hai người mặc đồ tối màu đi sát song song (chồng lấn IoU cao), tôi đặt keyframe cách nhau **2–3 frame**, neo cạnh box sát theo vai/chân riêng biệt của từng người và bật `occluded` cho người đi phía sau để tránh box bị nội suy "hút" sang người đi bên cạnh.

### B2 — So cách đặt keyframe

| Cách đặt | Số keyframe | Frame trôi nhất | Ghi chú |
|---|---:|---:|---|
| Đều mỗi 30 frame | | | |
| Theo chỗ đổi hướng | | | |

| Đều mỗi 30 frame | `6` | `Frame 45` | Tiết kiệm thao tác nhưng box bị lệch khỏi người khi rẽ hướng hoặc đổi tốc độ ở giữa khoảng. |
| Theo chỗ đổi hướng | `8` | `Frame 18` | Box bám sát cơ thể xuyên suốt chuỗi frame, loại bỏ hoàn toàn lỗi `drift` ở các đoạn ngoặt. |

### B3 — So với tracker có sẵn

| Frame | Mã người | Tracker làm gì | Nhãn của bạn | Giải thích (đoán rồi sửa / ghép IoU / box score thấp / ngoại hình) |
|---:|---|---|---|---|
| `68` | `P1` | Mất dấu và cấp ID mới khi hiện lại | Giữ nguyên ID `P1` | Tracker chỉ dùng **ghép IoU** và Kalman Filter nên mất liên kết sau 13 frame khuất; nhãn tay kết hợp **ngoại hình** nên giữ đúng ID. |
| `95` | `P3` | Bỏ sót detection (không vẽ box) | Vẫn gán box kèm cờ `occluded` | **Box score thấp** do bị che khuất >50% khiến detector lọc bỏ; người gán vẫn suy luận được vị trí cơ thể. |
## 7. Tài liệu tham khảo và công cụ AI đã dùng

...
