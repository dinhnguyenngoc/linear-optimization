# Linear Programming — Bài tập có lời giải (Tối ưu hóa & Quy hoạch tuyến tính)

> Tiểu luận môn **Tối ưu hóa và Quy hoạch tuyến tính** — Chương trình Thạc sĩ Công nghệ
> Thông tin, Trường Đại học Công nghệ TP.HCM (HUTECH), lớp 24SCT11, 10/2024.

Tập hợp lời giải chi tiết cho các dạng bài **Quy hoạch tuyến tính (Linear Programming)**:
từ lập mô hình toán học, các phương pháp giải (hình học, đơn hình, đơn hình mở rộng,
đối ngẫu), đến đánh giá tính tối ưu và bài toán chứa tham số.

## Nội dung

| # | Chủ đề | Mô tả |
|---|--------|-------|
| 1 | **Lập mô hình toán học** | Chuyển bài toán thực tế (lập kế hoạch sản xuất) → mô hình LP: biến quyết định, hệ ràng buộc, hàm mục tiêu |
| 2 | **Phương pháp hình học** (Graphical) | Giải LP 2 biến bằng miền phương án + vector pháp tuyến hàm mục tiêu (tìm cả min & max) |
| 3 | **Phương pháp đơn hình** (Simplex) | Thêm ẩn phụ → dạng chuẩn → lập bảng đơn hình, lặp đến khi tối ưu |
| 4 | **Đơn hình mở rộng** (Big-M) | Thêm ẩn giả với hệ số `M` để xử lý ràng buộc `=` / `≥` |
| 5 | **Đánh giá tính tối ưu** | Kiểm tra một phương án cho trước có khả thi / tối ưu hay không |
| 6 | **Phương pháp đối ngẫu** (Duality / Dual Simplex) | Xây bài toán đối ngẫu (D), giải bằng định lý độ lệch bù yếu (complementary slackness) |
| 7 | **Bài toán chứa tham số** (Parametric LP) | Giải & biện luận theo tham số `t` |

## Các phương pháp giải

- **Hình học (Graphical):** vẽ miền phương án khả thi, dịch chuyển đường mức theo
  vector pháp tuyến `n_d` của hàm mục tiêu để tìm đỉnh tối ưu (min/max).
- **Đơn hình (Simplex):** đưa về dạng chuẩn bằng ẩn phụ; lặp bảng đơn hình, chọn cột
  xoay theo dấu hàng `Δⱼ`, dừng khi đạt điều kiện tối ưu.
- **Đơn hình mở rộng (Big-M):** dùng ẩn giả + hệ số phạt `M` cho ràng buộc đẳng thức
  hoặc `≥`; phương án gốc tối ưu khi mọi ẩn giả về 0.
- **Đối ngẫu (Duality):** mỗi bài toán gốc (P) có bài toán đối ngẫu (D); dùng cặp ràng
  buộc đối ngẫu + định lý độ lệch bù yếu để suy ra nghiệm (D) từ nghiệm (P).
- **Đánh giá tính tối ưu:** thay phương án vào ràng buộc để kiểm khả thi; đối chiếu điều
  kiện tối ưu của bảng đơn hình.

## Tóm tắt kết quả các bài

| Bài | Phương pháp | Kết quả |
|-----|-------------|---------|
| 1 | Lập mô hình | Mô hình LP lập kế hoạch sản xuất máy biến thế 5 tháng (min tổng chi phí: sản xuất giờ thường + phụ trội + lưu kho) |
| 2 | Hình học | `f = -4x₁ + 3x₂`: `f_max = 6` tại `(0, 2)`; `f_min = -42/5` tại `(12/5, 2/5)` |
| 3 | Đơn hình | `f_max = 36` tại `x⁰ = (0, 4/5, 0, 3)` |
| 4 | Đơn hình mở rộng (Big-M) | `f_min = -5` tại `x⁰ = (2, 3, 0, 6, 0)` |
| 5 | Đánh giá tối ưu | `x⁰ = (0,0,1,2)` là phương án khả thi nhưng **không** tối ưu (bài toán không có PA tối ưu) |
| 6 | Đối ngẫu | (P): `f_min = 960` tại `(0, 16, 32)`; (D): `g_max = 1440` tại `(3, 15, 0)` |
| 7 | Tham số `t ∈ [1; 8]` | (chưa thực hiện) |

## Kiểm chứng bằng Python (tùy chọn)

Có thể đối chiếu nghiệm bằng `scipy` hoặc `PuLP`:

```python
from scipy.optimize import linprog
# Ví dụ bài 3: max 2x1+15x2-5x3+8x4  →  linprog tối thiểu hóa -c
c = [-2, -15, 5, -8]
A_ub = [[3, 10, 1, -1], [1, 5, 1, 2], [2, -5, 2, 10]]
b_ub = [25, 10, 26]
res = linprog(c, A_ub=A_ub, b_ub=b_ub, bounds=(0, None))
print(-res.fun, res.x)   # kỳ vọng ≈ 36 tại (0, 0.8, 0, 3)
```

## Tài liệu tham khảo

- Tài liệu môn học *Tối ưu hóa và Quy hoạch tuyến tính* — TS. Hồ Đắc Nghĩa.

## Tác giả

Nguyễn Ngọc Đỉnh — 2440861001 · GVHD: TS. Hồ Đắc Nghĩa
