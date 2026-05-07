# Nghiên cứu Chi tiết Dataset FEMTO-ST (PRONOSTIA) cho Bài toán RUL

Tài liệu này tổng hợp kết quả nghiên cứu toàn diện về bộ dữ liệu FEMTO-ST (PRONOSTIA) phục vụ cho dự báo tuổi thọ còn lại (RUL) của vòng bi, tập trung vào việc áp dụng các kiến trúc hiện đại như Mamba và Transformer.

---

## 1. Giới thiệu vai trò của dataset (Section 3.1)

### 1.1 Tầm quan trọng của FEMTO-ST trong PHM
Bộ dữ liệu FEMTO-ST, được giới thiệu trong cuộc thi **IEEE PHM 2012 Prognostic Challenge**, là một trong những bộ benchmark quan trọng nhất trong lĩnh vực Dự báo và Quản lý Sức khỏe (PHM). Nó cung cấp dữ liệu suy thoái tăng tốc (run-to-failure) dưới các điều kiện vận hành biến thiên, giúp đánh giá khả năng trích xuất đặc trưng và dự báo xu hướng của các mô hình AI.

### 1.2 Nguồn gốc và bối cảnh
- **Đơn vị xây dựng:** Viện nghiên cứu FEMTO-ST (Pháp).
- **Mục tiêu:** Mô phỏng quá trình hư hỏng tự nhiên của vòng bi trong thời gian ngắn thông qua việc tăng tải trọng và tốc độ quay.
- **Tính thực tế:** So với các bộ dữ liệu tĩnh, FEMTO-ST cung cấp 3 kịch bản vận hành khác nhau, giúp thử nghiệm tính thích ứng (generalization) của mô hình.

---

## 2. Tổng quan bộ dữ liệu (Section 2.2)

| Đặc điểm | Thông tin chi tiết |
| :--- | :--- |
| **Tên chính thức** | PRONOSTIA / IEEE PHM 2012 Data Challenge Dataset |
| **Link GitHub** | [Lucky-Loek/ieee-phm-2012-data-challenge-dataset](https://github.com/Lucky-Loek/ieee-phm-2012-data-challenge-dataset) |
| **Hình thức** | Accelerated life tests (Run-to-failure) |
| **Đối tượng** | Vòng bi NSK 6203 |
| **Số lượng mẫu** | 17 vòng bi (6 training, 11 test) |

---

## 3. Phân loại Nguồn dataset (Section 3.2)

### 3.1 Phân loại nguồn và môi trường
- **Loại nguồn:** Public Benchmark Dataset (DOI chính thức).
- **Môi trường thu thập:** Laboratory (Phòng thí nghiệm có kiểm soát).
- **Hình thức dữ liệu:** Multimodal (Vibration & Temperature).

### 3.2 Độ tin cậy và Khả năng tái lập
- **Độ tin cậy:** Cao, đã được sử dụng trong hàng nghìn nghiên cứu và cuộc thi toàn cầu.
- **Tài liệu:** Bài báo gốc của Nectoux et al. (2012) mô tả cực kỳ chi tiết về nền tảng PRONOSTIA.
- **Khả năng tái lập:** Việc chia sẻ dataset qua GitHub và các kho lưu trữ công cộng giúp các nghiên cứu dựa trên Mamba/Transformer dễ dàng so sánh hiệu năng (Benchmarking).

---

## 4. Đặc điểm kỹ thuật của dataset (Section 3.3)

### 4.1 Thông số kỹ thuật cốt lõi

| Thông số | Giá trị |
| :--- | :--- |
| **Tín hiệu rung động** | 2 cảm biến gia tốc (Ngang & Dọc) |
| **Tần số lấy mẫu (Vibration)** | 25.6 kHz |
| **Tín hiệu nhiệt độ** | 1 cảm biến RTD (PT100) |
| **Tần số lấy mẫu (Temp)** | 10 Hz |
| **Độ dài Snapshot** | 0.1 giây (2560 điểm) mỗi 10 giây |
| **Điều kiện vận hành (OC)** | **OC 1:** 1800 rpm / 4000 N<br>**OC 2:** 1650 rpm / 4200 N<br>**OC 3:** 1500 rpm / 5000 N |

### 4.2 Tình trạng dữ liệu và Gán nhãn
- **Tiêu chuẩn hư hỏng (EOL):** Quá trình dừng lại khi biên độ tín hiệu rung vượt quá **20g**.
- **Gán nhãn:** RUL được tính ngược từ thời điểm EOL về 0.
- **Đặc điểm tín hiệu:** Chứa nhiễu từ hệ thống truyền động cơ khí, yêu cầu các kỹ thuật lọc hoặc kiến trúc mạnh mẽ (như Mamba) để trích xuất tín hiệu suy thoái.

---

## 5. Phân tích chất lượng dataset (Section 3.4)

- **Tính đại diện (Representativeness):** Mô phỏng tốt quá trình mỏi của kim loại dẫn đến bong tróc (spalling) - lỗi phổ biến nhất của vòng bi công nghiệp.
- **Tính đa dạng (Diversity):** Có sự thay đổi về tải trọng và tốc độ giữa các OC, thách thức khả năng thích ứng của Transformer (Attention mechanism) khi phân phối dữ liệu dịch chuyển.
- **Chất lượng nhãn:** Nhãn "hard" dựa trên giới hạn vật lý (20g) rất khách quan, nhưng có sự mất cân bằng giữa giai đoạn ổn định (dài) và giai đoạn suy thoái nhanh (ngắn).

---

## 6. Review các nghiên cứu Mamba & Transformer (Section 4)

### 6.1 Mamba-SDP (2025)
- **Phương pháp:** Kết hợp **ICFFT** để xử lý tín hiệu không dừng và **Mamba** để trích xuất đặc trưng với độ phức tạp tuyến tính $O(N)$.
- **Ưu điểm:** Xử lý chuỗi dài tốt hơn Transformer truyền thống, giảm bộ nhớ khi làm việc với tần số 25.6 kHz.
- **Split:** Unit-wise split để tránh rò rỉ dữ liệu.

### 6.2 FEMamba (2025)
- **Phương pháp:** Sử dụng mô-đun **MFES** (tăng cường đặc trưng) và **DSGR** (điều chuẩn toàn cục theo giai đoạn suy thoái).
- **Kết quả:** Đạt $R^2 = 0.9601$ trên FEMTO-ST, chứng minh Mamba có thể nắm bắt tri thức vật lý tốt hơn khi có cơ chế điều chuẩn đúng đắn.

### 6.3 Frequency-Adaptive Framework (Transformer-based, 2026)
- **Phương pháp:** Mạng **SFEN** dựa trên Transformer để mô hình hóa tương tác chéo giữa các cảm biến (Horizontal vs Vertical).
- **Kết quả:** Giảm RMSE 57.8% nhờ khả năng "chú ý" (Attention) vào các dải tần số nhạy cảm với lỗi.

---

## 7. Literature Matrix cho FEMTO-ST (Section 5)

| ID | Paper | Kiến trúc | Dataset | Đặc điểm nổi bật | Kết quả |
| :--- | :--- | :--- | :--- | :--- | :--- |
| P01 | Mamba-SDP | Mamba | FEMTO-ST, XJTU-SY | ICFFT + Linear Complexity | MAE giảm 7-8% |
| P02 | FEMamba | Mamba | FEMTO-ST | DSGR Physical Knowledge | $R^2 = 0.9601$ |
| P03 | SFEN | Transformer | FEMTO-ST | Cross-sensor Interaction | RMSE giảm 57.8% |

---

## 8. Xác định Dataset Gap (Section 6)

- **Rò rỉ dữ liệu:** Nhiều nghiên cứu cũ sử dụng Random Split, dẫn đến kết quả ảo. FEMTO-ST yêu cầu **Independent Unit Split**.
- **Cross-condition Gap:** Hiếm có nghiên cứu huấn luyện trên OC1 và test trên OC3 để đánh giá tính bền vững thực sự của Mamba.
- **Multimodal Fusion:** Phần lớn nghiên cứu bỏ qua dữ liệu nhiệt độ (10 Hz), chỉ tập trung vào rung động.

---

## 9. Ý nghĩa đối với nghiên cứu hiện tại (Section 10)

1. **Lựa chọn kiến trúc:** Sử dụng **Mamba** làm xương sống (backbone) để xử lý chuỗi dài từ snapshots 0.1s, kết hợp **Attention** của Transformer ở lớp cuối để tổng hợp thông tin cảm biến.
2. **Chiến lược dữ liệu:** Áp dụng **Independent Unit Split** và kiểm chứng **Cross-condition** trên 3 OC của FEMTO-ST.
3. **Tiền xử lý:** Tận dụng thông tin tần số (FFT/STFT) làm đầu vào cho Mamba thay vì chỉ dùng tín hiệu thô.

---

## 10. Checklist đánh giá (Section 9)

- [x] **Hỗ trợ RUL:** Có (Run-to-failure).
- [x] **Nguồn uy tín:** Có (Viện FEMTO-ST).
- [x] **Sampling Rate:** Đạt chuẩn (25.6 kHz).
- [x] **Gán nhãn EOL:** Rõ ràng (> 20g).
- [x] **Điều kiện biến thiên:** 3 kịch bản OC.
