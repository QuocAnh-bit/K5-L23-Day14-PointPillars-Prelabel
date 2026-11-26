# Báo cáo Day 14 — Dương Quốc Anh — 2A202603286

- Mã học viên dùng với `--student` — `2A202603286`
- `seed_tag` trong `frames_A.txt` — `82ac3100fd`

## 1. Dự đoán trước sweep (bước 5b)

- Tham số tôi nghĩ giảm công sửa nhiều nhất là `min_points`.
- Khi rà ảnh BEV tập A, tôi thấy nhiều hộp thừa ở những vùng bị che khuất, rõ nhất ở frame thứ ba (`s05f19`). Tôi thấy một số hộp thừa chứa ít điểm LiDAR, nên dự đoán tăng `min_points` sẽ loại được các hộp như vậy và giảm số hộp cần xóa.

## 2. Tập A: sửa tay và tune

| Cấu hình | Xóa | Thêm | Sửa | Chi phí |
|---|---:|---:|---:|---:|
| Gốc (`score_thr=0.1`, `min_points=0`) | 40 | 10 | 3 | 23,5 |
| `best_config.json` | | | | |

- Riêng `s05f19`, cấu hình gốc cần xóa 22 hộp và thêm 2 hộp, tương ứng 8,6 điểm công sửa. Số điểm LiDAR trung vị là 59,5 ở các hộp thừa và 201,5 ở các hộp khớp nhãn tham chiếu. Trong 22 hộp thừa, có 1 hộp chứa dưới 10 điểm.
- Các mức sẽ thử gồm `score_thr` ở `0.1, 0.2, 0.3, 0.4, 0.5` và `min_points` ở `0, 5, 10`.
- Tham số đã đổi trong `best_config.json`: ...
- Kết quả leave-one-out (dán các dòng `scripts/pp_sweep.py` in ra): ...
- Cấu hình có ổn định trên từng frame không? Vì sao tôi vẫn chọn (hoặc không chọn) nó: ...

## 3. Trước/sau (bước 8)

![so sánh](../../d14_2A202603286/compare/<frame>.jpg)

- `scripts/pp_compare.py` báo giảm (hoặc tăng) ...% công sửa trên tập A.
- Dự đoán ở mục 1 đúng hay sai? Giải thích bằng số box xóa/thêm/sửa: ...

## 4. Tập B

Số đo từ `scripts/pp_prelabel.py --frames d14_2A202603286/frames_B.txt --config d14_2A202603286/best_config.json --gt d14_2A202603286/ref_B.json`:

| Xóa | Thêm | Sửa | Chi phí |
|---:|---:|---:|---:|
| | | | |

- Loại box tốn công sửa nhất ở tập B: ...

## 5. Giới hạn

- Nêu ít nhất 2 giới hạn (ví dụ: chỉ 3 frame tune; model KITTI không có Truck/Bus; chi phí là công thức, chưa phải thời gian sửa thật): ...
