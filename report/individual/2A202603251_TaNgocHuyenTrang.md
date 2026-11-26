# Báo cáo Day 14 — Tạ Ngọc Huyền Trang — 2A202603251

- Mã học viên dùng với `--student`: `251`
- `seed_tag` trong `frames_A.txt`: `393590736f`

## 1. Dự đoán trước sweep (bước 5b)

- Tham số tôi nghĩ giảm công sửa nhiều nhất: Tăng `score_thr` (từ 0.1 lên 0.3 hoặc 0.4) kết hợp tăng `min_points` (từ 0 lên 5 hoặc 10).
- Vì sao (nhìn ảnh BEV tập A: box thừa nhiều hay box sót nhiều?): Khi quan sát ảnh BEV tập A và số đo thực tế từ cấu hình gốc, model sinh ra rất nhiều box thừa ở các vùng nhiễu (xóa tới 54 box trên tổng số 83 box dự đoán, chỉ có 29 box khớp thật, chiếm tới 16.2 điểm chi phí sửa). Trong khi đó, số box thật bị bỏ sót rất ít (chỉ thêm 3 box). Các box thừa này chủ yếu có điểm tin cậy thấp hoặc chứa rất ít điểm LiDAR. Do đó, việc tăng `score_thr` và lọc `min_points` sẽ loại bỏ được phần lớn các box thừa điểm thấp này mà hầu như không làm mất vật thể thật, giúp giảm chi phí công sửa nhiều nhất.

## 2. Tập A: sửa tay và tune

| Cấu hình | Xóa | Thêm | Sửa | Chi phí |
|---|---:|---:|---:|---:|
| Gốc | 54 | 3 | 7 | 22.7 |
| `best_config.json` | | | | |

- Tham số đã đổi trong `best_config.json`: ...
- Kết quả leave-one-out (dán các dòng `scripts/pp_sweep.py` in ra): ...
- Cấu hình có ổn định trên từng frame không? Vì sao tôi vẫn chọn (hoặc không chọn) nó: ...

## 3. Trước/sau (bước 8)

![so sánh](../../d14_251/compare/<frame>.jpg)

- `scripts/pp_compare.py` báo giảm (hoặc tăng) ...% công sửa trên tập A.
- Dự đoán ở mục 1 đúng hay sai? Giải thích bằng số box xóa/thêm/sửa: ...

## 4. Tập B

Số đo từ `scripts/pp_prelabel.py --frames d14_251/frames_B.txt --config d14_251/best_config.json --gt d14_251/ref_B.json`:

| Xóa | Thêm | Sửa | Chi phí |
|---:|---:|---:|---:|
| | | | |

- Loại box tốn công sửa nhất ở tập B: ...

## 5. Giới hạn

- Nêu ít nhất 2 giới hạn (ví dụ: chỉ 3 frame tune; model KITTI không có Truck/Bus; chi phí là công thức, chưa phải thời gian sửa thật): ...
