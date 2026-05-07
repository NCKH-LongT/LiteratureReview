# Literature Review về Dataset Vòng Bi (Bearing Datasets)

## 1. Giới thiệu vai trò của dataset (Section 3.1)

### 1.1 Tầm quan trọng của dataset trong bài toán nghiên cứu
Trong lĩnh vực Dự báo và Quản lý Sức khỏe (PHM) cho vòng bi, bộ dữ liệu đóng vai trò then chốt vì hiệu suất của các mô hình AI phụ thuộc trực tiếp vào chất lượng tín hiệu, chiến lược gán nhãn và sự đa dạng của các kịch bản suy thoái. Việc sử dụng các bộ dữ liệu công khai (Public Benchmark Datasets) có DOI và nguồn gốc rõ ràng giúp đảm bảo tính tin cậy, khả năng tái lập và tính tổng quát hóa của kết quả nghiên cứu.

### 1.2 Nguồn dữ liệu và nhu cầu đặc thù
Bài toán dự báo (Prognostics) và chẩn đoán (Diagnosis) lỗi vòng bi yêu cầu các loại dữ liệu đặc thù từ các nguồn uy tín:
- **Tín hiệu rung động (Vibration):** Nguồn dữ liệu chính (ví dụ: [NASA IMS](https://data.nasa.gov/dataset/ims-bearings) - 20 kHz, [XJTU-SY](https://github.com/WangBiaoXJTU/xjtu-sy-bearing-datasets) - 25.6 kHz).
- **Tín hiệu nhiệt độ (Temperature):** Thường xuất hiện trong các bài toán run-to-failure (ví dụ: [Paderborn University](https://doi.org/10.5281/zenodo.10805042)).
- **Dữ liệu đa cảm biến (Current, Torque):** Giúp tăng cường độ chính xác (ví dụ: [KAIST Bearing Datasets](https://www.sciencedirect.com/science/article/pii/S235234092400372X)).

### 1.3 Tính thực tế và Độ phản ánh hiện trạng
Đánh giá tính thực tế của các bộ dữ liệu hiện có:
- **Môi trường thí nghiệm (Constant Conditions):** Các bộ dữ liệu như [NASA IMS](https://data.nasa.gov/dataset/ims-bearings) cung cấp baseline chuẩn nhưng thiếu sự biến động của thực tế.
- **Điều kiện vận hành thay đổi (Time-Varying Conditions):** Các bộ dữ liệu hiện đại như [Paderborn University](https://doi.org/10.5281/zenodo.10805042) và [FEMTO-ST](https://github.com/Lucky-Loek/ieee-phm-2012-data-challenge-dataset) đã bắt đầu mô phỏng tải trọng và tốc độ biến thiên, sát với thực tế công nghiệp hơn.

---

## 2. Tổng quan các bộ dữ liệu Prognostics phổ biến (Section 2.2)

Dưới đây là danh sách 7 bộ dữ liệu run-to-failure trọng tâm được sử dụng trong bài review này:

| Tên Dataset | Link Chính Thức / DOI | Đặc điểm nổi bật |
| :--- | :--- | :--- |
| **Paderborn University** | [10.5281/zenodo.10805042](https://doi.org/10.5281/zenodo.10805042) | Điều kiện vận hành thay đổi (non-stationary), dữ liệu rung & nhiệt độ. |
| **NASA IMS** | [NASA Data Portal](https://data.nasa.gov/dataset/ims-bearings) | Bộ dữ liệu nền tảng, run-to-failure dưới tải trọng không đổi. |
| **FEMTO-ST (PRONOSTIA)** | [IEEE PHM 2012](https://github.com/Lucky-Loek/ieee-phm-2012-data-challenge-dataset) | Dữ liệu từ cuộc thi PHM 2012, kịch bản tải/tốc độ đa dạng. |
| **Xi'an Jiaotong (XJTU-SY)** | [XJTU-SY GitHub](https://github.com/WangBiaoXJTU/xjtu-sy-bearing-datasets) | Tần số lấy mẫu cao (25.6 kHz), 15 vòng bi chạy đến khi hỏng. |
| **KAIST Bearing** | [ScienceDirect](https://www.sciencedirect.com/science/article/pii/S235234092400372X) | Đa cảm biến: Dòng điện, Rung động, Mô-men xoắn. |
| **UNSW Bearing** | [Mendeley Data](https://data.mendeley.com/datasets/h4df4mgrfb/3) | Tập trung vào lỗi nhân tạo và phân tích phổ trong môi trường nhiễu. |
| **University of Ferrara** | [SFERA Repository](https://sfera.unife.it/handle/11392/2569668) | Phát hiện sớm lỗi bằng kỹ thuật xử lý tín hiệu tiên tiến. |

---

## 3. Phân loại Nguồn dataset (Section 3.2)

Dựa trên nguồn gốc và phương pháp thu thập, các bộ dữ liệu được phân loại như sau để đánh giá độ tin cậy và khả năng tái lập:

### 3.1 Phân loại theo nguồn gốc và môi trường thu thập
Tất cả 7 bộ dữ liệu được chọn đều là **Public benchmark datasets**, có tính công khai cao và được cộng đồng nghiên cứu thừa nhận rộng rãi.

| Tên Dataset | Loại Nguồn | Môi trường thu thập | Hình thức dữ liệu |
| :--- | :--- | :--- | :--- |
| **Paderborn University** | Public | Laboratory (Time-varying) | Multimodal (Vibration, Temp) |
| **NASA IMS** | Public | Laboratory | Single Modality (Vibration) |
| **FEMTO-ST (PRONOSTIA)** | Public | Laboratory | Multimodal (Vibration, Temp) |
| **Xi'an Jiaotong (XJTU-SY)** | Public | Laboratory | Single Modality (Vibration) |
| **KAIST Bearing** | Public | Laboratory | Multimodal (Current, Vib, Torque) |
| **UNSW Bearing** | Public | Laboratory | Single Modality (Vibration) |
| **University of Ferrara** | Public | Laboratory | Single Modality (Vibration) |

### 3.2 Đánh giá độ tin cậy và Khả năng tái lập
- **Tính công khai:** 100% các bộ dữ liệu đều có link chính thức hoặc DOI, cho phép tải xuống và sử dụng miễn phí cho mục đích nghiên cứu.
- **Tài liệu hướng dẫn:** Đa số đều đi kèm bài báo mô tả chi tiết (ví dụ: NASA IMS có bài báo gốc từ NASA Ames, XJTU-SY có tài liệu mô tả tần số lấy mẫu và thiết lập cảm biến).
- **Khả năng tái lập:** Việc cung cấp đầy đủ thông số kỹ thuật (sampling rate, load, speed profiles) giúp các nghiên cứu sau này dễ dàng thiết lập baseline để so sánh hiệu năng của các mô hình mới như Mamba hay Transformer.

---

## 4. Đặc điểm kỹ thuật của dataset (Section 3.3)

Phần này tổng hợp các thông số kỹ thuật cốt lõi của 7 bộ dữ liệu để hỗ trợ việc lựa chọn dữ liệu phù hợp với kiến trúc mô hình (ví dụ: các mô hình yêu cầu tần số cao hay dữ liệu đa biến).

### 4.1 Bảng so sánh thông số kỹ thuật

| Tên Dataset | Loại tín hiệu | Tần số lấy mẫu (Sampling Rate) | Điều kiện vận hành | Đặc điểm mẫu (Sample Size/Labels) |
| :--- | :--- | :--- | :--- | :--- |
| **Paderborn University** | Rung động, Nhiệt độ | Đa dạng (Fs variable) | 4 kịch bản (900-1500 RPM, 0.7-1.4 kN) | Run-to-failure trong điều kiện non-stationary. |
| **NASA IMS** | Rung động | 20 kHz | Cố định (2000 RPM, 6000 lbs) | Snapshots 1s mỗi 10 phút. 3 thí nghiệm chính. |
| **FEMTO-ST** | Rung động, Nhiệt độ | 25.6 kHz | 3 kịch bản (1800/1650/1500 RPM, 4-5 kN) | 17 bộ run-to-failure (NSK 6203). |
| **XJTU-SY** | Rung động | 25.6 kHz | 3 kịch bản (2100/2250/2400 RPM, 10-12 kN) | 15 vòng bi (LDK UER204), chất lượng cao. |
| **KAIST Bearing** | Dòng điện, Rung, Mô-men | 25.6 kHz & 100 kHz | 1770 RPM (0, 2, 4 Nm) hoặc biến thiên | Kết hợp đa cảm biến, mô phỏng nhiều lỗi cơ khí. |
| **UNSW Bearing** | Rung động | Đa dạng (Fs variable) | 4 tốc độ (360/720/900/1200 RPM) | Lỗi nhân tạo và run-to-failure tự nhiên. |
| **Univ. of Ferrara** | Rung động | 25.6 kHz | Cố định (2400 RPM, 3-5 kN) | Lỗi có kiểm soát, phù hợp kiểm chứng xử lý tín hiệu. |

### 4.2 Tình trạng dữ liệu và Gán nhãn
- **Annotation method:** Đa số các bộ dữ liệu run-to-failure (NASA, XJTU, FEMTO) gán nhãn dựa trên thời gian vận hành thực tế cho đến khi máy dừng hoặc hỏng hoàn toàn (End-of-life).
- **Noise & Imbalance:** Dữ liệu thực nghiệm thường chứa nhiễu từ hệ thống truyền động. Các bộ dữ liệu như UNSW và Ferrara được thiết kế để thử nghiệm khả năng kháng nhiễu.
- **Metadata:** Các bộ dữ liệu hiện đại (Paderborn, XJTU) cung cấp đầy đủ thông tin về thiết lập cảm biến và sơ đồ tải trọng, hỗ trợ tốt cho việc trích xuất đặc trưng vật lý.

---

## 5. Phân tích chất lượng dataset (Section 3.4)

Phần này đánh giá sâu hơn về chất lượng của các bộ dữ liệu để xác định mức độ phù hợp của chúng khi áp dụng vào các bài toán thực tế và khả năng huấn luyện các mô hình AI tiên tiến.

### 5.1 Tính đại diện (Representativeness)
Đa số các bộ dữ liệu (NASA IMS, XJTU-SY, FEMTO-ST) được thu thập trong môi trường phòng thí nghiệm có kiểm soát. Mặc dù giúp thiết lập các baseline thuật toán chính xác, nhưng chúng có thể chưa phản ánh hết sự khắc nghiệt của môi trường công nghiệp thực tế (nhiễu nền lớn, tải trọng biến thiên đột ngột). Bộ dữ liệu **Paderborn University** có tính đại diện cao nhất nhờ việc mô phỏng các profile vận hành không dừng (non-stationary).

### 5.2 Tính đa dạng (Diversity)
- **Điều kiện vận hành:** Các bộ dữ liệu hiện đại (Paderborn, XJTU-SY, FEMTO-ST) cung cấp nhiều kịch bản tốc độ và tải trọng khác nhau, hỗ trợ tốt cho việc nghiên cứu tính đa miền (Cross-domain).
- **Đa cảm biến (Multimodal):** **KAIST** và **Paderborn** nổi bật với sự kết hợp của dòng điện, mô-men xoắn và nhiệt độ bên cạnh rung động, giúp mô hình học được các đặc trưng bổ trợ cho nhau.

### 5.3 Chất lượng nhãn (Label quality)
Các bộ dữ liệu run-to-failure (NASA, XJTU, FEMTO) sử dụng nhãn dựa trên thời điểm hư hỏng thực tế (hard labels), đảm bảo tính khách quan cao. Tuy nhiên, ranh giới giữa giai đoạn "khỏe mạnh" và "bắt đầu suy thoái" thường không được gán nhãn chi tiết, đòi hỏi các thuật toán phát hiện điểm thay đổi (change point detection) để tối ưu hóa.

### 5.4 Phân phối dữ liệu (Data distribution)
- **Class Imbalance:** Đây là vấn đề chung vì thời gian vận hành khỏe mạnh thường chiếm đa số so với giai đoạn suy thoái nhanh cuối vòng đời.
- **Domain Shift:** Sự khác biệt giữa các kịch bản tải trọng (ví dụ: 1800 rpm vs 1500 rpm) tạo ra thách thức về dịch chuyển phân phối, yêu cầu các mô hình như Mamba hoặc Transformer phải có khả năng thích ứng cao.

### 5.5 Khả năng tái lập (Reproducibility)
Tất cả các bộ dữ liệu được chọn đều có tính tái lập cao:
- **Công khai:** 100% public với link truy cập rõ ràng.
- **Cấu trúc:** Có mô tả cấu trúc tệp tin và thông số cảm biến đi kèm.
- **Benchmark:** Đã được sử dụng làm chuẩn so sánh trong hàng trăm bài báo khoa học uy tín, giúp dễ dàng đối soát kết quả.

---

## 6. Review cách các bài báo trước sử dụng dataset (Section 4)

Phần này phân tích cách các nghiên cứu tiên tiến (đặc biệt là các mô hình dựa trên kiến trúc Mamba và Transformer) khai thác 7 bộ dữ liệu chuẩn để tối ưu hóa hiệu suất dự báo RUL và chẩn đoán lỗi.

### 6.1 Remaining useful life prediction method for rolling bearings based on Mamba-SDP (2025)
- **Dataset Used:** IEEE PHM 2012 (PRONOSTIA) và XJTU-SY. Cả hai đều là public run-to-failure datasets.
- **Methodology:** 
  - Sử dụng module **ICFFT** để phân tích các thành phần tần số của tín hiệu không dừng.
  - Áp dụng kiến trúc **Mamba** để trích xuất đặc trưng không gian-thời gian sâu.
  - Cơ chế chú ý **SDP** giúp tăng cường độ ổn định tính toán.
- **Split Strategy:** Chia theo đơn vị vòng bi (Unit-wise split). Dữ liệu từ một số vòng bi được dùng để huấn luyện, các vòng bi còn lại dùng để kiểm chứng (đảm bảo tính tổng quát hóa). Sử dụng kỹ thuật cửa sổ trượt (sliding window) để tạo các phân đoạn thời gian.
- **Evaluative:** Giảm sai số MAE và RMSE xuống 7-8% so với các mô hình SOTA hiện nay. Điểm mạnh là khả năng xử lý chuỗi dài hiệu quả của Mamba.

### 6.2 FEMamba: A Feature-Enhanced Mamba Framework with Degradation-Stage Global Regularization (2025)
- **Dataset Used:** IEEE PHM 2012 (PRONOSTIA).
- **Methodology:** 
  - Mô-đun **MFES** giúp chọn lọc đặc trưng đa nguồn thích ứng với dữ liệu không đồng nhất.
  - Chiến lược **DSGR** đưa các đặc điểm vật lý của từng giai đoạn suy thoái vào quá trình học.
- **Split Strategy:** Tập trung vào việc chia dữ liệu theo giai đoạn suy thoái (degradation stages) thay vì chia ngẫu nhiên, giúp mô hình nắm bắt được xu hướng vật lý.
- **Evaluative:** Đạt độ chính xác ấn tượng với chỉ số $R^2$ lên tới 0.9601 trên bộ dữ liệu PHM2012.

### 6.3 Mamba TFVisionChaos: A Mamba-based Multimodal Bearing Fault Diagnosis Model (2025)
- **Dataset Used:** XJTU-SY, CWRU, JNU, HIT.
- **Methodology:** 
  - Chuyển đổi tín hiệu 1D thành biểu diễn 2D (Time-Frequency Dual-Axis).
  - Sử dụng mô-đun tăng cường hỗn loạn (chaos-enhanced) để phát hiện sớm hư hỏng.
  - Kiến trúc Mamba hạng nhẹ giúp giảm độ phức tạp tính toán xuống $O(L)$.
- **Split Strategy:** Chia mẫu ngẫu nhiên (1024 điểm mỗi mẫu). Thực hiện các thí nghiệm **Cross-condition** (huấn luyện trên điều kiện tải này và test trên điều kiện tải khác) để kiểm tra tính thích ứng.
- **Evaluative:** Độ chính xác từ 97.4% đến 100% với kích thước mô hình siêu nhỏ (~1.28 MB), cực kỳ phù hợp cho thiết bị vùng biên (edge devices).

### 6.4 A Frequency-Adaptive Feature Extraction Framework (2026)
- **Dataset Used:** FEMTO-ST (PRONOSTIA) và bộ dữ liệu suy thoái tăng tốc.
- **Methodology:** 
  - Mạng **TFEN** sử dụng tích chập giãn (dilated convolution) thích ứng với các dải tần số (thấp, trung, cao).
  - Mạng **SFEN** dựa trên Transformer để mô hình hóa tương tác chéo giữa các cảm biến.
- **Split Strategy:** Train-test split dựa trên các đơn vị vòng bi độc lập.
- **Evaluative:** Chỉ số RMSE giảm tới 57.8% so với các phương pháp dải tần đơn, chứng minh hiệu quả của việc xử lý đa tần số thích ứng.

---

## 7. Literature Matrix cho Dataset Review (Section 5)

Bảng dưới đây tổng hợp cách các nghiên cứu tiêu biểu khai thác và xử lý dữ liệu, giúp định hình chiến lược lựa chọn dataset và phương pháp split cho nghiên cứu hiện tại.

| ID | Paper | Year | Dataset | Split Strategy | Dataset Strength | Dataset Limitation | Relevance |
|---|---|---|---|---|---|---|---|
| P01 | Mamba-SDP | 2025 | PHM 2012, XJTU-SY | Unit-wise split | Xử lý tốt tín hiệu không dừng (ICFFT) | Kiến trúc SDP khá phức tạp | Baseline mạnh cho Mamba |
| P02 | FEMamba | 2025 | IEEE PHM 2012 | Degradation stages | Điều chuẩn toàn cục theo đặc điểm vật lý | Phụ thuộc vào gán nhãn giai đoạn | Kỹ thuật tăng cường đặc trưng |
| P03 | Mamba TFVisionChaos | 2025 | XJTU-SY, CWRU, JNU | Random segment / Cross-condition | Siêu nhẹ, hỗ trợ đa phương thức | Nguy cơ leakage nếu split không kỹ | Tối ưu triển khai thực tế |
| P04 | Frequency-Adaptive Framework | 2026 | FEMTO-ST | Independent unit split | Thích ứng đa tần số (TFEN) | Chi phí tính toán của Transformer | Phân tích đa quy mô |

---
*Ghi chú:* 
- **Unit-wise split:** Chia theo đơn vị vòng bi độc lập để tránh rò rỉ dữ liệu (Data Leakage).
- **Cross-condition:** Kiểm tra khả năng tổng quát hóa trên các điều kiện vận hành khác nhau.

---

## 8. Xác định Dataset Gap (Section 6)

Thông qua việc review các nghiên cứu hiện tại và đặc điểm của 7 bộ dữ liệu chuẩn, các lỗ hổng nghiên cứu (Research Gaps) liên quan đến dữ liệu được xác định như sau:

### 8.1 Khoảng cách thực tế (Real-world Gap)
Mặc dù các bộ dữ liệu như Paderborn và XJTU-SY đã cải thiện tính thực tế bằng cách mô phỏng các điều kiện vận hành thay đổi, nhưng phần lớn dữ liệu vẫn được thu thập trong môi trường phòng thí nghiệm lý tưởng. Các yếu tố như nhiễu ngẫu nhiên từ các máy móc lân cận, sự thay đổi môi trường (nhiệt độ, độ ẩm) và các can thiệp bảo trì thực tế thường chưa được phản ánh đầy đủ.

### 8.2 Rò rỉ dữ liệu và Phân phối (Distribution & Leakage Gap)
Một lỗ hổng nghiêm trọng trong nhiều bài báo trước đây là việc sử dụng chiến lược **Random Split** trên dữ liệu chuỗi thời gian. Điều này dẫn đến việc các đoạn tín hiệu rất gần nhau trong cùng một quá trình suy thoái xuất hiện ở cả tập train và test, gây ra hiện tượng rò rỉ dữ liệu (Temporal Leakage) và dẫn đến kết quả độ chính xác bị thổi phồng. Việc thiếu các đánh giá **Subject-wise split** (chia theo đơn vị thiết bị) và **Cross-domain** (chia theo điều kiện tải) vẫn còn phổ biến.

### 8.3 Hạn chế về Nhãn và Đa phương thức (Quality & Multimodal Gap)
- **Nhãn thiếu chi tiết:** Đa số các bộ dữ liệu run-to-failure chỉ cung cấp nhãn "thời gian hỏng cuối cùng", thiếu sự phân định rõ ràng giữa giai đoạn khỏe mạnh, giai đoạn suy thoái sớm và giai đoạn hỏng hóc nghiêm trọng.
- **Thiếu tính đa nguồn:** Mặc dù rung động là tín hiệu quan trọng nhất, việc thiếu các bộ dữ liệu kết hợp đồng thời rung động, phát xạ âm thanh (AE) và các thông số vận hành thực tế (OC) khiến việc xây dựng các mô hình PHM toàn diện gặp khó khăn.

### 8.4 Lỗ hổng về tính tái lập (Reproducibility Gap)
Mặc dù các bộ dữ liệu là công khai (Public), nhưng các script tiền xử lý (preprocessing), phương pháp lọc nhiễu và danh sách cụ thể các mẫu được chọn cho tập train/test thường không được các tác giả công bố kèm theo bài báo. Điều này tạo ra rào cản lớn trong việc tái lập hoàn xác kết quả và thực hiện các so sánh công bằng (fair comparison).

---

## 9. Ý nghĩa đối với nghiên cứu hiện tại (Section 2.7 & Section 10)

Dựa trên quá trình review toàn diện, nghiên cứu này sẽ áp dụng các bài học kinh nghiệm sau để xây dựng mô hình dự báo RUL dựa trên kiến trúc Mamba:

- **Lựa chọn Dataset:** Ưu tiên sử dụng bộ dữ liệu **XJTU-SY** (độ phân giải cao) và **Paderborn University** (điều kiện vận hành thay đổi). Việc chọn Paderborn là nhằm trực tiếp giải quyết lỗ hổng "Real-world Gap" và kiểm chứng khả năng xử lý tín hiệu không dừng của Mamba.
- **Chiến lược Split:** Tuyệt đối không sử dụng Random Split. Nghiên cứu sẽ áp dụng **Independent Unit Split** (chia theo đơn vị vòng bi độc lập) để đảm bảo không có rò rỉ dữ liệu và kết quả đánh giá mang tính thực tiễn cao nhất.
- **Xử lý đặc trưng:** Tận dụng khả năng trích xuất đặc trưng đa quy mô (Multi-scale) để bắt được cả biến động ngắn hạn và xu hướng suy thoái dài hạn, khắc phục hạn chế về "Nhãn thiếu chi tiết" bằng cách tập trung vào việc mô hình hóa tiến trình suy thoái liên tục thay vì chỉ dự báo một mốc thời gian cố định.

---

## 10. Checklist đánh giá và lựa chọn dataset (Section 9)

Trước khi quyết định sử dụng một bộ dữ liệu cho mô hình, cần thực hiện rà soát theo các tiêu chí sau:

- [ ] **Tính phù hợp:** Dataset có hỗ trợ bài toán Run-to-failure (RUL) không?
- [ ] **Nguồn chính thống:** Có DOI hoặc link từ các trường đại học/tổ chức uy tín?
- [ ] **Tính công khai:** Có thể truy cập và tải xuống mà không bị hạn chế pháp lý?
- [ ] **Chất lượng tín hiệu:** Tần số lấy mẫu (sampling rate) có đủ cao để trích xuất đặc trưng lỗi?
- [ ] **Gán nhãn:** Có mốc thời gian hỏng (EOL) rõ ràng?
- [ ] **Chống rò rỉ:** Chiến lược chia dữ liệu có đảm bảo không bị Temporal Leakage?
- [ ] **Tính thực tế:** Có kịch bản tải trọng biến thiên để kiểm tra tính mạnh mẽ (Robustness)?

---

## 11. Kết luận (Section 11)

Tổng kết lại, các bộ dữ liệu vòng bi hiện nay đã tạo nền tảng vững chắc cho sự phát triển của các thuật toán PHM. Tuy nhiên, ranh giới giữa nghiên cứu trong phòng thí nghiệm và ứng dụng công nghiệp vẫn còn tồn tại do những hạn chế về tính đa dạng và nguy cơ rò rỉ dữ liệu trong quá trình huấn luyện. Nghiên cứu hiện tại sẽ tập trung vào việc khắc phục các lỗ hổng này bằng cách sử dụng kiến trúc Mamba mạnh mẽ kết hợp với chiến lược chia dữ liệu nghiêm ngặt, nhằm xây dựng một mô hình dự báo RUL có độ tin cậy cao và khả năng triển khai thực tế tốt hơn.
