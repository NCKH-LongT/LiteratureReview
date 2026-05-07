# Nghiên cứu Chi tiết Dataset Paderborn University cho Bài toán RUL & Diagnosis

Tài liệu này tổng hợp kết quả nghiên cứu toàn diện về bộ dữ liệu của Đại học Paderborn (PU) phục vụ cho dự báo tuổi thọ còn lại (RUL) và chẩn đoán lỗi vòng bi, tập trung vào các kiến trúc lai Mamba-Transformer.

---

## 1. Giới thiệu vai trò của dataset (Section 3.1)

### 1.1 Tầm quan trọng của PU Dataset
Bộ dữ liệu Paderborn University nổi bật trong cộng đồng PHM nhờ tính thực tế cực cao. Không giống như nhiều bộ dữ liệu chỉ tập trung vào lỗi nhân tạo (artificial damage), PU cung cấp dữ liệu từ các vòng bi bị hư hỏng tự nhiên thông qua các bài thử nghiệm tuổi thọ tăng tốc, giúp mô hình học được các đặc điểm suy thoái sát với thực tế công nghiệp.

### 1.2 Nguồn gốc và bối cảnh
- **Đơn vị xây dựng:** Nhóm Thiết kế Máy và Truyền động (KAt), Đại học Paderborn, Đức.
- **Tính thực tế:** Được coi là một trong những bộ dữ liệu khó nhất và "thực" nhất do sự kết hợp giữa các điều kiện vận hành không dừng (non-stationary) và các loại hư hỏng đa dạng (bong tróc, rỗ, vết nứt).

---

## 2. Tổng quan bộ dữ liệu (Section 2.2)

| Đặc điểm | Thông tin chi tiết |
| :--- | :--- |
| **Tên chính thức** | Paderborn University Bearing Dataset |
| **Link DOI** | [10.5281/zenodo.10805042](https://doi.org/10.5281/zenodo.10805042) |
| **Hình thức** | Experimental measurements (Healthy & Damaged) |
| **Đối tượng** | Vòng bi cầu rãnh sâu (Deep groove ball bearings) |
| **Số lượng trạng thái** | 6 khỏe mạnh, 26 hư hỏng (12 lỗi nhân tạo, 14 lỗi tự nhiên) |

---

## 3. Phân loại Nguồn dataset (Section 3.2)

### 3.1 Phân loại nguồn và môi trường
- **Loại nguồn:** Public Benchmark Dataset.
- **Môi trường thu thập:** Laboratory (Time-varying conditions).
- **Hình thức dữ liệu:** Multimodal (Vibration & Motor Current).

### 3.2 Độ tin cậy và Khả năng tái lập
- **Độ tin cậy:** Tuyệt đối, là tiêu chuẩn vàng để kiểm chứng khả năng chống nhiễu và tính tổng quát hóa.
- **Tài liệu:** Bài báo của Lessmeier et al. (2016) cung cấp mô tả kỹ thuật đầy đủ về hệ thống thu thập.

---

## 4. Đặc điểm kỹ thuật của dataset (Section 3.3)

### 4.1 Thông số kỹ thuật cốt lõi

| Thông số | Giá trị |
| :--- | :--- |
| **Tín hiệu rung động** | Cảm biến piezo (64 kHz) |
| **Tín hiệu dòng điện** | Dòng điện pha động cơ (64 kHz) |
| **Tần số lấy mẫu** | 64,000 Hz |
| **Điều kiện vận hành** | **4 Kịch bản:** Kết hợp của:<br>- Tốc độ: 900 / 1500 RPM<br>- Tải trọng: 0.7 / 1.4 kN<br>- Mô-men: 0.3 / 0.7 Nm |

### 4.2 Tình trạng dữ liệu và Gán nhãn
- **Labels:** Phân loại theo loại lỗi (Inner race, Outer race) và mức độ suy thoái.
- **Tính multimodal:** Việc đồng bộ hóa giữa dòng điện và rung động cho phép xây dựng các mô hình **Sensor Fusion** (như Transformer-based fusion) cực kỳ hiệu quả.

---

## 5. Phân tích chất lượng dataset (Section 3.4)

- **Tính đại diện (Representativeness):** Cao nhất trong các bộ dữ liệu công khai nhờ các mẫu "Real damages".
- **Tính đa dạng (Diversity):** Cực kỳ đa dạng về kịch bản lỗi, rất phù hợp cho bài toán **Few-shot learning** hoặc **Domain Adaptation**.
- **Chất lượng nhãn:** Nhãn được kiểm chứng qua phân tích vật lý sau khi vòng bi hỏng hoàn toàn.

---

## 6. Review các nghiên cứu Mamba & Transformer (Section 4)

### 6.1 SDMT-Net (2025)
- **Phương pháp:** Hybrid Spiral Dual Mamba and Transformer.
- **Cơ chế:** Mamba trích xuất đặc trưng cục bộ kháng nhiễu, Transformer xử lý quan hệ toàn cục.
- **Kết quả:** Đạt độ chính xác vượt trội trên tập dữ liệu PU ngay cả trong môi trường có nhiễu nền cực lớn (SNR thấp).

### 6.2 PG-TMT (Physics-Guided, 2026)
- **Phương pháp:** Physics-Guided Tiny-Mamba Transformer.
- **Cơ chế:** Tích hợp tri thức vật lý về các dải tần số lỗi (Fault-order bands) vào kiến trúc Mamba-Transformer hạng nhẹ.
- **Ưu điểm:** Khả năng phát hiện sớm lỗi (Early fault warning) với độ tin cậy cao trên dữ liệu PU.

### 6.3 BMTM-Net (2025)
- **Phương pháp:** Bidirectional Multi-granularity Transformer-Mamba.
- **Cơ chế:** Sử dụng 2D-1D fusion để kết hợp tín hiệu dòng điện và rung động của PU dataset.

---

## 7. Literature Matrix cho PU Dataset (Section 5)

| ID | Paper | Kiến trúc | Dataset | Đặc điểm nổi bật | Kết quả |
| :--- | :--- | :--- | :--- | :--- | :--- |
| P05 | SDMT-Net | Mamba + Transformer | PU, CWRU | Spiral Dual Architecture | Robust với nhiễu |
| P06 | PG-TMT | Tiny Mamba-Transformer | PU | Physics-Guided (Fault bands) | Early warning chuẩn xác |
| P07 | BMTM-Net | Bidirectional Mamba-Transformer | PU | 2D-1D Sensor Fusion | Tối ưu đa cảm biến |

---

## 8. Xác định Dataset Gap (Section 6)

- **Độ phức tạp tính toán:** Với sampling rate 64 kHz, các mô hình Transformer thuần túy gặp vấn đề về bộ nhớ. Sự xuất hiện của **Mamba** giúp giải quyết lỗ hổng này.
- **Cross-sensor Leakage:** Việc sử dụng cả dòng điện và rung động đòi hỏi các chiến lược split cẩn thận để không bị rò rỉ thông tin giữa các kênh cảm biến.

---

## 9. Ý nghĩa đối với nghiên cứu hiện tại (Section 10)

1. **Kiểm chứng tính mạnh mẽ:** Sử dụng PU dataset để chứng minh khả năng của Mamba trong việc xử lý tín hiệu không dừng (non-stationary).
2. **Sensor Fusion:** Tận dụng dữ liệu dòng điện của PU để thử nghiệm các module **Cross-attention** của Transformer kết hợp với **Linear Scan** của Mamba.
3. **Phát hiện sớm:** Tập trung vào các mẫu "Real damage" để huấn luyện khả năng nhận diện dấu hiệu suy thoái từ sớm.

---

## 10. Checklist đánh giá (Section 9)

- [x] **Hỗ trợ Diagnosis/RUL:** Có.
- [x] **Nguồn uy tín:** Đại học Paderborn.
- [x] **Sampling Rate:** Rất cao (64 kHz).
- [x] **Tính thực tế:** Cao nhất (Real damages).
- [x] **Đa cảm biến:** Rung động + Dòng điện.
