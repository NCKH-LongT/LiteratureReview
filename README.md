# Model LiteratureReview Repository
## 1. Giới thiệu về bài toán dự đoán độ hư hỏng hoặc giá trị cho vòng bi

### 1.1 Bối cảnh kỹ thuật và tầm quan trọng
Vòng bi lăn (Rolling element bearings) là thành phần cốt lõi trong các hệ thống máy móc quay như động cơ điện, tuabin gió và máy công cụ công nghiệp. Do điều kiện vận hành khắc nghiệt bao gồm tải trọng cao, tốc độ biến thiên và môi trường nhiễu, vòng bi được xác định là bộ phận dễ hư hỏng nhất, chiếm khoảng 45% đến 55% tổng số các trường hợp sự cố máy móc. Việc vòng bi hỏng đột ngột không chỉ gây dừng máy ngoài kế hoạch mà còn dẫn đến các thảm họa về an toàn và thiệt hại kinh tế nghiêm trọng.

Trong bối cảnh đó, hai bài toán then chốt trong Quản lý Sức khỏe và Dự báo (PHM) bao gồm:
* **Chẩn đoán lỗi (Fault Diagnosis)**: Xác định sự hiện diện, vị trí cụ thể (vòng trong, vòng ngoài, con lăn) và mức độ nghiêm trọng của hư hỏng.
* **Dự đoán tuổi thọ hữu dụng còn lại (Remaining Useful Life - RUL)**: Ước tính khoảng thời gian hoặc số chu kỳ còn lại trước khi thiết bị không còn khả năng thực hiện chức năng mục tiêu và cần thực hiện bảo trì.

### 1.2 Tại sao cần ứng dụng trí tuệ nhân tạo?
Các phương pháp truyền thống dựa trên mô hình vật lý, như mô hình Paris-Erdogan, thường đòi hỏi kiến thức chuyên gia sâu và gặp khó khăn trong việc thiết lập tham số chính xác cho các hệ thống phức tạp. Ngược lại, các phương pháp AI, đặc biệt là Học sâu (Deep Learning), mang lại các ưu thế vượt trội:
* **Tự động trích xuất đặc trưng**: Loại bỏ việc phải thiết kế thủ công các chỉ số đặc trưng (feature engineering) vốn dễ bị sai lệch trong môi trường thực tế.
* **Xử lý các mẫu phi tuyến tính**: Tín hiệu rung động từ vòng bi thường có tính chất không dừng (non-stationary) và phi tuyến tính mạnh; AI có khả năng học các mối quan hệ ẩn sâu giữa dữ liệu cảm biến và trạng thái suy thoái.
* **Xử lý dữ liệu đa chiều**: Khả năng kết hợp và xử lý thông tin đồng thời từ nhiều nguồn cảm biến để tăng độ tin cậy cho các dự báo.

### 1.3 Cấu trúc dữ liệu và Mục tiêu tối ưu
Nghiên cứu tập trung vào việc chuyển đổi dữ liệu thô từ cảm biến thành các quyết định bảo trì thông minh thông qua các thành phần sau:

**Dữ liệu đầu vào (Input):**
* Chủ yếu là tín hiệu rung động (Vibration signals) thu thập từ cảm biến gia tốc.
* Có thể kết hợp tín hiệu dòng điện (MCSA) hoặc nhiệt độ để tăng cường độ chính xác cho mô hình.
* Dữ liệu thường được tiền xử lý thành dạng hình ảnh (Spectrogram/CWT) cho các mô hình tích chập (CNN) hoặc giữ dạng chuỗi 1D cho các mô hình tuần tự như Mamba hoặc LSTM.

**Dữ liệu đầu ra (Output):**
* Giá trị thời gian thực của RUL, ví dụ như số giờ hoặc số vòng quay còn lại.
* Phân loại trạng thái sức khỏe của thiết bị (Bình thường, Lỗi vòng trong, Lỗi vòng ngoài, v.v.).

**Mục tiêu tối ưu (Optimization Goals):**
* **Đối với bài toán dự đoán (Regression)**: Giảm thiểu sai số dự báo thông qua các chỉ số như Sai số bình phương trung bình căn (RMSE) và Sai số tuyệt đối trung bình (MAE).
* **Đối với bài toán chẩn đoán (Classification)**: Tối đa hóa Độ chính xác (Accuracy), chỉ số F1-score, và khả năng nhận diện lỗi sớm trong điều kiện môi trường có độ nhiễu cao.

# 2. Phân nhóm phương pháp AI trong dự đoán sức khỏe thiết bị

Sự phát triển của các phương pháp AI trong lĩnh vực Quản lý Sức khỏe và Dự đoán (PHM) cho vòng bi đã trải qua lộ trình từ các mô hình học máy truyền thống (cần can thiệp thủ công) đến các kiến trúc học sâu tiên tiến (tự động hóa hoàn toàn). Việc phân nhóm dưới đây giúp xác định vị trí của mô hình đề xuất so với các phương pháp hiện hành.

---

## 2.1 Bảng tổng hợp các nhóm phương pháp

| Nhóm phương pháp | Mô hình tiêu biểu | Cách tiếp cận chính | Phức tạp tính toán |
| :--- | :--- | :--- | :--- |
| **Traditional ML** | SVM, Random Forest, XGBoost | Trích xuất đặc trưng thủ công (RMS, Kurtosis) | $O(1)$ |
| **Sequential DL** | LSTM, TCN, CNN-LSTM | Học phụ thuộc thời gian qua cơ chế cổng/tích chập | $O(L)$ |
| **Attention-based** | Transformer, TCN-Transformer | Cơ chế tự chú ý (Self-Attention) toàn cục | $O(L^2)$ |
| **State Space (SSM)** | Mamba, Hybrid Mamba-CNN | Quét chọn lọc (Selective Scan), độ phức tạp tuyến tính | $O(L)$ |

---

## 2.2 Nhóm Học máy truyền thống (Traditional Machine Learning)

Nhóm này dựa trên việc sử dụng các thuật toán phân loại và hồi quy cổ điển sau khi đã thực hiện xử lý tín hiệu.

* **Mô hình tiêu biểu**:
    * **SVM & Random Forest**: Đạt độ chính xác từ 97.5% - 99.2% trong các điều kiện tải trọng ổn định.
    * **XGBoost**: Thể hiện ưu thế vượt trội so với cây quyết định thông thường trong việc xử lý các đặc trưng miền thời gian.
* **Hạn chế**: Hiệu suất giảm mạnh khi tín hiệu bị nhiễu hoặc khi điều kiện vận hành thay đổi (tốc độ quay biến thiên).
* **Tài liệu tham khảo**:
    * [A Bearing Fault Diagnosis Model Based on a Simplified Wide Convolutional Neural Network and Random Forest (Sensors, 2025)](https://www.mdpi.com/1424-8220/25/3/752)
    * [Application of machine learning techniques for bearing fault diagnosis (Journal of Applied and Computational Mechanics, 2025)](https://jacm.scu.ac.ir/article_19459_16e58d932f3bf986116b9802a7bfeb19.pdf)

---

## 2.3 Nhóm Học sâu chuỗi thời gian (Sequential Deep Learning)

Sử dụng các mạng nơ-ron có khả năng lưu trữ thông tin lịch sử để dự đoán xu hướng suy thoái (RUL).

* **Mô hình tiêu biểu**:
    * **CNN-LSTM**: Kết hợp CNN trích xuất đặc trưng không gian và LSTM học phụ thuộc thời gian.
    * **TCN (Temporal Convolutional Network)**: Sử dụng tích chập giãn để mở rộng trường thụ cảm, vượt qua hạn chế tính toán tuần tự của RNN.
* **Ưu điểm**: Tự động hóa việc học đặc trưng, hiệu quả hơn ML truyền thống trong các bài toán dự báo dài hạn.
* **Tài liệu tham khảo**:
    * [RUL Prediction of Rolling Bearings Based on Fruit Fly Optimization Algorithm Optimized CNN-LSTM Neural Network (Machines, 2025)](https://www.mdpi.com/2075-4442/13/2/81)
    * [A novel RUL prediction method for rolling bearing: TcLstmNet-CBAM (PMC12019386, 2025)](https://pmc.ncbi.nlm.nih.gov/articles/PMC12019386/)

---

## 2.4 Nhóm mô hình dựa trên Attention (Transformer)

Sử dụng cơ chế Self-Attention để nắm bắt mối quan hệ giữa mọi điểm dữ liệu trong chuỗi.

* **Mô hình tiêu biểu**:
    * **TCN-Transformer**: Kết hợp đặc trưng cục bộ của TCN và bối cảnh toàn cầu của Transformer.
    * **Transformer-LSTM**: Tận dụng khả năng mô hình hóa dài hạn của Transformer cho bài toán RUL.
* **Hạn chế**: Phụ thuộc vào dữ liệu lớn để tránh overfit và chi phí bộ nhớ cực cao $O(L^2)$ khi xử lý dữ liệu rung động tần suất cao.
* **Tài liệu tham khảo**:
    * [Remaining Useful Life Prediction for Rolling Bearings Based on TCN-Transformer Networks Using Vibration Signals (PMC12158285, 2025)](https://pmc.ncbi.nlm.nih.gov/articles/PMC12158285/)
    * [Remaining Useful Life Prediction of Rolling Bearings Based on Empirical Mode Decomposition and Transformer Bi-LSTM Network (Applied Sciences, 2025)](https://www.mdpi.com/2076-3417/15/17/9529)

---

## 2.5 Nhóm mô hình Mamba và Hybrid Mamba-CNN (Proposed)

Đây là thế hệ kiến trúc mới nhất (**SOTA - State of the Art**) nhằm thay thế Transformer trong việc xử lý chuỗi cực dài.

* **Mô hình tiêu biểu**:
    * **MASA-LSTM**: Mô hình LSTM tăng cường Mamba và Self-Attention, đạt độ chính xác chẩn đoán 99.9% ngay cả ở mức nhiễu -6dB.
    * **LDGM (Mamba-based)**: Kiến trúc Mamba cho phép triển khai trên thiết bị biên (edge deployment) với độ phức tạp tuyến tính.
    * **MOM-Conv Mamba**: Kết hợp Mixture of Experts (MoE) với Mamba để trích xuất đa quy mô đặc trưng.
* **Lý do lựa chọn**: Mamba cung cấp khả năng mô hình hóa toàn cầu tương đương Transformer nhưng tiêu tốn ít hơn 80% bộ nhớ GPU và tốc độ suy luận nhanh hơn gấp nhiều lần nhờ độ phức tạp tuyến tính $O(L)$.
* **Tài liệu tham khảo**:
    * [Fault Diagnosis of Rolling Bearings Using Denoising Multi-Channel Mixture of CNN and Mamba-Enhanced Adaptive Self-Attention LSTM (Sensors, 2025)](https://www.mdpi.com/1424-8220/25/21/6652)
    * [LDGM: Domain-invariant bearing fault diagnosis via Mamba-based linear complexity modeling and feature perturbation for edge deployment (ResearchGate, 2024)](https://www.researchgate.net/publication/400785154_LDGM_Domain-invariant_bearing_fault_diagnosis_via_Mamba-based_linear_complexity_modeling_and_feature_perturbation_for_edge_deployment)

---

## 3. Đánh giá các mô hình Deep Learning (Baselines)

Trong các hệ thống giám sát sức khỏe thiết bị hiện đại, học sâu (Deep Learning) đã thay thế các phương pháp truyền thống nhờ khả năng tự động trích xuất các đặc trưng phi tuyến tính từ tín hiệu rung động phức tạp. Tuy nhiên, mỗi kiến trúc baseline (LSTM, TCN, Transformer) đều có những ưu điểm và hạn chế riêng về mặt kiến trúc khi xử lý dữ liệu chuỗi thời gian của vòng bi.

### 3.1 Mạng nơ-ron tích chập (CNN-based methods)
CNN thường được sử dụng như một bộ trích xuất đặc trưng không gian mạnh mẽ, đặc biệt khi tín hiệu 1D được chuyển đổi thành hình ảnh 2D như spectrogram hoặc hình ảnh thời-tần CWT.

* **Đặc điểm**: Sử dụng các hạt nhân tích chập (kernels) để quét qua dữ liệu nhằm phát hiện các mẫu xung va chạm cục bộ gây ra bởi vết nứt trên vòng bi. Một kiến trúc tiêu biểu là **WDCNN (Wide Deep CNN)** sử dụng hạt nhân rộng ở lớp đầu tiên để chống nhiễu hiệu quả hơn.
* **Hạn chế**: CNN thuần túy thiếu khả năng mô hình hóa các phụ thuộc thời gian dài hạn (long-range temporal dependencies) - yếu tố sống còn để dự đoán quỹ đạo suy thoái RUL.
* **Tham khảo**: [Bearing Fault Diagnosis Using Lightweight and Robust One-Dimensional Convolution Neural Network in the Frequency Domain (Sensors, 2022)](https://www.mdpi.com/1424-8220/22/15/5793).

---

### 3.2 Mạng nơ-ron tái phát (RNN/LSTM-based methods)
**LSTM** là kiến trúc phổ biến nhất cho bài toán RUL nhờ cơ chế cổng giúp kiểm soát dòng thông tin qua thời gian.

* **Cơ chế**: LSTM giải quyết vấn đề biến mất đạo hàm của RNN truyền thống thông qua ba cổng: cổng quên ($f_t$), cổng vào ($i_t$), và cổng ra ($o_t$).
* **Công thức cổng quên**: $$f_t = \sigma(W_f \cdot [h_{t-1}, x_t] + b_f)$$.
* **Ưu điểm**: Cực kỳ hiệu quả trong việc nắm bắt xu hướng suy thoái liên tục và các tương tác phức tạp trong chuỗi thời gian.
* **Hạn chế**: Do tính chất tính toán tuần tự (sequential), LSTM không thể song song hóa, dẫn đến thời gian huấn luyện rất lâu đối với dữ liệu cảm biến tần suất cao và gặp khó khăn khi độ dài chuỗi vượt quá một ngưỡng nhất định.
* **Tham khảo**: [Research on Bearing Remaining Useful Life Prediction Method Based on Double Bidirectional Long Short-Term Memory (Applied Sciences, 2025)](https://www.mdpi.com/2076-3417/15/8/4441).

---

### 3.3 Mạng tích chập thời gian (TCN-based methods)
**TCN** xuất hiện như một giải pháp thay thế mạnh mẽ cho RNN bằng cách kết hợp ưu điểm của CNN và khả năng xử lý chuỗi.

* **Cơ chế**: Sử dụng tích chập giãn (**Dilated Convolution**) và tích chập nhân quả (**Causal Convolution**) để mở rộng trường thụ cảm mà không cần tăng số lượng tham số quá mức.
* **Trường thụ cảm (Receptive Field)**: Tăng theo cấp số nhân với độ giãn $d$, cho phép mô hình "nhìn" thấy lịch sử dữ liệu xa hơn nhiều so với CNN thông thường.
* **Ưu điểm**: Cho phép tính toán song song hoàn toàn trên GPU, giúp tốc độ huấn luyện nhanh hơn đáng kể so với LSTM.
* **Tham khảo**: [Prediction of Residual Life of Rolling Bearings Based on Multi-Scale Improved Temporal Convolutional Network (MITCN) Model (Machines, 2025)](https://www.mdpi.com/2075-1702/13/2/137).

---

### 3.4 Mô hình dựa trên Attention (Transformer-based methods)
**Transformer** đã thiết lập tiêu chuẩn mới trong việc học các mối quan hệ toàn cầu thông qua cơ chế tự chú ý (**Self-Attention**).

* **Cơ chế**: Thay vì quét tuần tự, cơ chế **Multi-Head Attention (MHA)** cho phép mỗi điểm thời gian trong chuỗi rung động "quan sát" tất cả các điểm khác để tính toán trọng số quan trọng.
* **Ưu điểm**: Khả năng nắm bắt các phụ thuộc dài hạn (long-range correlations) vượt trội so với LSTM và TCN, giảm thiểu sai số tích lũy trong quá trình dự báo RUL.
* **Hạn chế**: Độ phức tạp tính toán và bộ nhớ tăng theo hàm bình phương $O(L^2)$ so với chiều dài chuỗi $L$. Đây là rào cản lớn nhất khi xử lý dữ liệu vòng bi thực tế với hàng nghìn bước thời gian.
* **Tham khảo**: [Remaining Useful Life Prediction of Rolling Bearings Based on Empirical Mode Decomposition and Transformer Bi-LSTM Network (Applied Sciences, 2025)](https://www.mdpi.com/2076-3417/15/17/9529).

---

### 3.5 Bảng so sánh đặc tính các mô hình Baseline

| Tiêu chí | CNN | LSTM | TCN | Transformer |
| :--- | :--- | :--- | :--- | :--- |
| **Khả năng học thời gian** | Thấp | Rất tốt | Tốt | Xuất sắc |
| **Tính toán song song** | Có | Không | Có | Có |
| **Độ phức tạp tính toán** | $O(L)$ | $O(L)$ | $O(L)$ | $O(L^2)$ |
| **Phụ thuộc dài hạn** | Cục bộ | Trung bình | Tốt | Rất tốt |
| **Ứng dụng chính** | Trích xuất đặc trưng | Dự báo xu hướng | Dự báo chuỗi dài | Quan hệ toàn cục |

# 4. Review mô hình Mamba và kiến trúc Hybrid Mamba-CNN

Mô hình Mamba, đại diện cho thế hệ mô hình không gian trạng thái chọn lọc (**Selective State Space Models - SSM**), đang nổi lên như một giải pháp đột phá để thay thế kiến trúc Transformer trong việc xử lý các chuỗi thời gian dài của thiết bị công nghiệp.

---

## 4.1 Cơ chế chọn lọc (Selective SSM) và Độ phức tạp tuyến tính

Điểm cốt lõi của Mamba là cơ chế **Quét chọn lọc (Selective Scan)**. Khác với các mô hình SSM truyền thống có các tham số cố định, Mamba cho phép các ma trận hệ thống ($B, C$) và bước thời gian ($\Delta$) thay đổi phụ thuộc vào dữ liệu đầu vào ($x$).

*   **Khả năng chọn lọc thông tin**: Cơ chế này cho phép mô hình quyết định một cách thông minh thông tin nào cần nén vào trạng thái ẩn (hidden state) và thông tin nào cần loại bỏ dựa trên ngữ cảnh hiện tại. Điều này đặc biệt quan trọng đối với vòng bi, nơi mô hình cần bỏ qua nhiễu môi trường và chỉ tập trung vào các tín hiệu suy thoái.
*   **Độ phức tạp tuyến tính $O(L)$**: Mamba giải quyết triệt để "nỗi đau" về chi phí tính toán của Transformer. Trong khi Transformer có độ phức tạp tăng theo hàm bình phương $O(L^2)$, Mamba duy trì độ phức tạp tuyến tính $O(L)$ đối với chiều dài chuỗi. Điều này cho phép mô hình xử lý các chuỗi dữ liệu rung động siêu dài (ultra-long time series) mà không gây quá tải bộ nhớ GPU.

---

## 4.2 Tại sao cần kiến trúc Hybrid Mamba-CNN?

Nghiên cứu hiện tại đề xuất sự kết hợp giữa **CNN (Convolutional Neural Networks)** và **Mamba** để tận dụng thế mạnh bổ trợ của cả hai kiến trúc:

1.  **CNN - Trích xuất đặc trưng cục bộ (Local Feature Extraction)**:
    *   Tín hiệu rung động của vòng bi chứa các xung va chạm cực ngắn khi có vết nứt.
    *   CNN với các hạt nhân tích chập (kernels) và các lớp như **MOM-Conv** (Mixture of Multi-view Convolution) rất hiệu quả trong việc phát hiện các đặc trưng không gian cục bộ từ hình ảnh thời-tần (Spectrogram/CWT).
    *   CNN đóng vai trò là "mắt thần" nhận diện các biến đổi tinh vi ở giai đoạn đầu hỏng hóc.

2.  **Mamba - Mô hình hóa suy thoái dài hạn (Global Dependency Modeling)**:
    *   Quá trình suy thoái của vòng bi diễn ra xuyên suốt vòng đời. Mamba đóng vai trò bộ nhớ toàn cầu, liên kết các đặc trưng cục bộ mà CNN trích xuất được để xây dựng một lộ trình suy thoái (**degradation trajectory**) nhất quán.
    *   Khả năng nén trạng thái hiệu quả giúp Mamba nắm bắt các phụ thuộc dài hạn tốt hơn so với LSTM mà không bị mất dấu bối cảnh như TCN.

---

## 4.3 Các nghiên cứu tiêu biểu và Hiệu năng

Các kiến trúc Hybrid Mamba-CNN đã chứng minh được sự vượt trội trong các báo cáo gần đây:

*   **Mô hình MASA-LSTM**: Một biến thể tăng cường Mamba cho LSTM giúp đạt độ chính xác chẩn đoán lỗi vòng bi lên đến **99.9%** trên bộ dữ liệu CWRU, ngay cả trong điều kiện nhiễu nặng -6dB.
*   **Tốc độ và Bộ nhớ**: Các thử nghiệm cho thấy kiến trúc dựa trên Mamba có thể nhanh hơn Transformer gấp **2.8 lần** và tiết kiệm tới **86.8%** bộ nhớ GPU khi xử lý các dữ liệu đầu vào độ phân giải cao.

---

## 4.4 Đường link tham khảo

| Tên bài báo / Tài liệu | Nguồn | Link truy cập |
| :--- | :---: | :--- |
| **Mamba: Linear-Time Sequence Modeling with Selective State Spaces** (Bản gốc) | arXiv | [Truy cập](https://arxiv.org/abs/2312.00752) |
| **Fault Diagnosis of Rolling Bearings Using Denoising Multi-Channel Mixture of CNN and Mamba-Enhanced Adaptive Self-Attention LSTM** (2025) | MDPI Sensors | [Truy cập](https://www.mdpi.com/1424-8220/25/21/6652) |
| **Vision Mamba: Efficient Visual Representation Learning with State Space Model** | arXiv | [Truy cập](https://arxiv.org/abs/2401.09417) |
| **A Systematic Review of RUL Prediction in Roller Bearings using AI Techniques** | ResearchGate | [Truy cập](https://www.researchgate.net/publication/382163983_A_Systematic_Review_of_Remaining_Useful_Life_Prediction_in_Roller_Bearings_using_Artificial_Intelligence_Techniques) |

# 5. Review cách biểu diễn dữ liệu (Input Representation)

Hiệu suất của các mô hình AI trong dự đoán sức khỏe vòng bi phụ thuộc rất lớn vào cách biểu diễn dữ liệu đầu vào. Do tín hiệu rung động thu thập được thường bị nhiễu nặng và có tính chất không dừng (**non-stationary**), việc lựa chọn giữa tín hiệu thô, các đặc trưng thống kê hay biến đổi miền thời-tần là một bước tiền xử lý then chốt.

---

## 5.1 Tín hiệu thô (Raw waveform) vs. Biến đổi Thời-tần (STFT, CWT)

*   **Tín hiệu thô (Raw Waveform)**: Mặc dù một số nghiên cứu sử dụng tín hiệu 1D thô để làm đầu vào trực tiếp cho các mạng như 1D-CNN hoặc LSTM nhằm mục đích **"end-to-end learning"**, cách tiếp cận này thường gặp khó khăn trong việc phân biệt các xung lỗi nhỏ bị che lấp bởi nhiễu môi trường.
*   **Biến đổi miền Thời-tần (Time-Frequency Representation)**: Đây là xu hướng chủ đạo trong các nghiên cứu **SOTA** (2024-2025).
    *   **STFT (Short-Time Fourier Transform)**: Cung cấp cái nhìn về sự thay đổi tần số theo thời gian, nhưng bị giới hạn bởi độ phân giải cố định do nguyên lý bất định Heisenberg.
    *   **CWT (Continuous Wavelet Transform)**: Được đánh giá cao hơn STFT vì khả năng đa độ phân giải. CWT sử dụng các hàm wavelet (như Morlet) để trích xuất các thành phần tần số khác nhau, tạo ra các **Scalograms** (hình ảnh thời-tần). Scalogram giúp CNN dễ dàng nhận diện các mẫu không tuần tự và các xung va chạm tức thời – dấu hiệu đặc trưng của hỏng hóc vòng bi.

**Công thức CWT cơ bản**:
$$C(a, b) = \int_{-\infty}^{\infty} x(t) \frac{1}{\sqrt{a}} \psi^* \left( \frac{t-b}{a} \right) dt$$
Trong đó:
*   $a$: Hệ số quy mô (tần số).
*   $b$: Hệ số dịch (thời gian).

---

## 5.2 Chỉ số Sức khỏe (Health Indicator - HI) và Đặc trưng Thống kê

Trong bài toán dự đoán RUL, việc xây dựng một **Chỉ số Sức khỏe (HI)** phản ánh đúng lộ trình suy thoái là rất quan trọng.

*   **Đặc trưng miền thời gian**: Các chỉ số như **RMS** (Root Mean Square), **Kurtosis** (Độ nhọn), **Skewness**, và **Peak-to-Peak** thường được trích xuất để làm giàu thông tin đầu vào.
    *   **RMS**: Phản ánh mức năng lượng tổng thể của rung động, thường tăng dần khi vòng bi bị mòn.
    *   **Kurtosis**: Cực kỳ nhạy bén với các xung va chạm đột ngột ở giai đoạn đầu của hư hỏng.
*   **Xây dựng HI**: Các nghiên cứu hiện đại sử dụng kỹ thuật trích xuất đa miền (**Multi-domain features**), sau đó áp dụng **PCA** (Principal Component Analysis) hoặc **KPCA** để nén dữ liệu thành một chỉ số HI duy nhất có tính đơn điệu (**monotonicity**) và tính xu hướng (**trendability**) cao. Chỉ số này sau đó được đưa vào mô hình Mamba hoặc LSTM để dự báo thời điểm vượt ngưỡng hỏng hóc.

---

## 5.3 Đường link tham khảo (Truy cập miễn phí toàn văn)

| Tên bài báo / Tài liệu | Nguồn | Link truy cập |
| :--- | :---: | :--- |
| **Optimal Source Selection for Bearing Classification using Wavelet & ML (2025)** | MDPI Sensors | [Truy cập](https://www.mdpi.com/1424-8220/25/4/1105) |
| **Ball bearing fault detection using an acoustic based machine learning approach (2025)** | PMC/Nature | [Truy cập](https://pmc.ncbi.nlm.nih.gov/articles/PMC11535456/) |
| **Remaining useful life prediction of rolling element bearings based on advanced degradation model (2024)** | ResearchGate | [Truy cập](https://www.researchgate.net/publication/380436531_Remaining_useful_life_prediction_of_rolling_element_bearings_based_on_advanced_degradation_model) |
| **A Multi-Scale Temporal Convolutional Network approach for RUL prediction (2025)** | Acadlore | [Truy cập](https://www.acadlore.com/journals/MSSP/2025/1/1/10.56578/mssp030102) |

# 6. Ma trận tổng hợp tài liệu (Literature Matrix)

Ma trận dưới đây tổng hợp các nghiên cứu quan trọng nhất trong giai đoạn 2024-2025 về chẩn đoán lỗi và dự đoán RUL vòng bi. Các nghiên cứu được lựa chọn đại diện cho từng nhóm kiến trúc khác nhau để so sánh hiệu năng và hạn chế.

| ID | Tác giả / Năm | Bài toán (Task) | Mô hình / Phương pháp | Dữ liệu (Dataset) | Chỉ số chính (Metrics) | Hạn chế của phương pháp |
| :-- | :--- | :--- | :--- | :--- | :--- | :--- |
| **P01** | [Lai et al. (2025)](https://www.mdpi.com/1424-8220/25/21/6652) | Chẩn đoán lỗi | Hybrid MOM-CNN + MASA-LSTM (Mamba) | CWRU & Paderborn | **Accuracy: 99.9%** (ngay cả khi nhiễu -6dB) | Độ phức tạp trong việc thiết kế các khối hybrid và tinh chỉnh tham số Mamba. |
| **P02** | [Wang et al. (2025)](https://pmc.ncbi.nlm.nih.gov/articles/PMC12158285/) | Dự đoán RUL | TCN–Transformer | IEEE PHM 2012 | **RMSE giảm 14.62%**, Score tăng 13.04% | Độ phức tạp tính toán bình phương $O(L^2)$ gây nghẽn bộ nhớ khi chuỗi dài. |
| **P03** | [Sun et al. (2025)](https://www.mdpi.com/2075-4442/13/2/81) | Dự đoán RUL | FOA-CNN-LSTM | PHM2012 & XJTU-SY | Cải thiện **Score 10.2%** so với CNN-LSTM gốc | Tính tuần tự của LSTM làm hạn chế tốc độ huấn luyện trên tập dữ liệu lớn. |
| **P04** | [Du et al. (2025)](https://www.mdpi.com/2075-1702/13/2/137) | Dự đoán RUL | HTCN-FA (Hybrid TCN) | XJTU-SY | **MAE: 2.287**, **RMSE: 3.123** | Khó khăn trong việc nắm bắt các phụ thuộc toàn cầu cực xa của cả vòng đời. |
| **P05** | [Zhang et al. (2025)](https://www.mdpi.com/1424-8220/25/3/752) | Chẩn đoán lỗi | SWDCNN-RF (CNN + Random Forest) | CWRU | **Accuracy: 99.6%**, Tốc độ tăng 38.5% | Thiếu cơ chế chú ý (Attention) để tập trung vào các vùng tín hiệu quan trọng nhất. |
| **P06** | [Wang & Wu (2025)](https://jacm.scu.ac.ir/article_19459_16e58d932f3bf986116b9802a7bfeb19.pdf) | Chẩn đoán lỗi | XGBoost + SHAP | CWRU | **Accuracy: 91.0%**, Recall: 100% | Phụ thuộc vào trích xuất đặc trưng thủ công (15 đặc trưng multi-domain). |
| **P07** | [Liu et al. (2024)](https://arxiv.org/abs/2401.09417) | Thị giác máy tính | VMamba (Visual State Space) | ImageNet/COCO | Nhanh hơn Transformer **2.8 lần**, tiết kiệm **86.8% RAM** | Chưa được tối ưu hóa sâu cho dữ liệu rung động 1D đặc thù của công nghiệp. |

---

### Ghi chú các ký hiệu:
*   **RMSE**: Root Mean Square Error (Sai số bình phương trung bình gốc).
*   **MAE**: Mean Absolute Error (Sai số tuyệt đối trung bình).
*   **$O(L)$ / $O(L^2)$**: Độ phức tạp thuật toán theo chiều dài chuỗi dữ liệu.
*   **-6dB**: Tỷ lệ tín hiệu trên nhiễu (SNR) mức độ cao.

# 7. Các chỉ số đánh giá (Evaluation Metrics)

Việc đánh giá hiệu suất của mô hình AI trong bài toán vòng bi cần được xem xét đa chiều: từ độ chính xác của giá trị dự báo (RUL) đến khả năng phát hiện sớm và độ tin cậy của hệ thống cảnh báo.

---

## 7.1 Chỉ số cho bài toán dự đoán RUL (Regression Metrics)

Các chỉ số này đo lường sai số giữa giá trị RUL dự đoán ($\hat{y}_i$) và giá trị RUL thực tế ($y_i$).

*   **Sai số tuyệt đối trung bình (MAE)**: Phản ánh sai lệch trung bình của dự báo.
    $$MAE = \frac{1}{n} \sum_{i=1}^{n} |y_i - \hat{y}_i|$$
    *   **Cách nhìn**: Càng thấp càng tốt. Giá trị tiến về 0 biểu thị dự báo cực kỳ sát với thực tế.

*   **Sai số bình phương trung bình căn (RMSE)**: Nhạy cảm với các sai số lớn (outliers), giúp đánh giá độ ổn định của mô hình.
    $$RMSE = \sqrt{\frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2}$$
    *   **Cách nhìn**: Càng thấp càng tốt. Nếu RMSE cao hơn nhiều so với MAE, mô hình đang gặp vấn đề với các mẫu dữ liệu khó (sai số lớn ở một vài thời điểm).

*   **Hàm điểm số PHM (Score)**: Sử dụng trọng số bất đối xứng để phạt nặng hơn các dự đoán "trễ" (RUL dự đoán > RUL thực tế) nhằm đảm bảo an toàn vận hành.
    *   **Cách nhìn**: Càng cao càng tốt. Một Score cao cho thấy mô hình không chỉ chính xác mà còn đảm bảo tính an toàn (ưu tiên báo hỏng sớm hơn là muộn).

---

## 7.2 Chỉ số chẩn đoán và giám sát bất thường (Anomaly & Monitoring Metrics)

Trong môi trường thực tế, việc xác định thời điểm bắt đầu suy thoái (onset of degradation) là tối quan trọng để kích hoạt quy trình dự báo RUL.

*   **Anomaly Score over TTF% (Điểm bất thường theo % thời gian đến khi hỏng)**:
    Theo dõi mức độ bất thường của tín hiệu dựa trên phần trăm tuổi thọ đã trôi qua. Điểm bất thường thường được tính từ lỗi tái cấu trúc của Autoencoder hoặc khoảng cách thống kê.
    *   **Cách nhìn**: Thấp ở giai đoạn đầu, tăng mạnh khi tiến gần đến 100% TTF (Time To Failure). Nếu điểm cao ngay từ đầu, mô hình đang nhầm nhiễu là lỗi.

*   **Threshold Chart (Biểu đồ ngưỡng)**:
    Công cụ trực quan hóa so sánh Chỉ số Sức khỏe (HI) hoặc Anomaly Score với một ngưỡng giới hạn an toàn (ví dụ: ngưỡng $3\sigma$ hoặc ngưỡng động).
    *   **Cách nhìn**: Vượt ngưỡng là có lỗi. Nếu đường tín hiệu "phẳng" và nằm xa dưới ngưỡng trong giai đoạn máy khỏe, mô hình có độ ổn định tốt.

*   **Detection Delay (Độ trễ phát hiện)**:
    Khoảng chênh lệch giữa thời điểm lỗi thực sự xảy ra ($t_{onset}$) và thời điểm mô hình AI đưa ra cảnh báo ($t_{alarm}$).
    $$Detection Delay = t_{alarm} - t_{onset}$$
    *   **Cách nhìn**: Càng thấp càng tốt. Trễ thấp giúp tối đa hóa thời gian chuẩn bị bảo trì và thay thế linh kiện.

*   **False Alarm Rate (Tỷ lệ báo động giả)**:
    Tỷ lệ máy bình thường bị báo hỏng nhầm (tương ứng với False Positive Rate).
    $$FAR = \frac{FP}{FP + TN}$$
    *   **Cách nhìn**: Càng thấp càng tốt (Lý tưởng < 1%). Tỷ lệ này cao gây lãng phí chi phí dừng máy và làm mất niềm tin của người vận hành.

---

## 7.3 Bảng tổng hợp và hướng dẫn diễn giải nhanh

Bảng dưới đây tóm tắt các chỉ số lựa chọn theo mục tiêu giám sát và cách diễn giải kết quả thực nghiệm:

| Nhóm mục tiêu | Chỉ số tiêu biểu | Giá trị mong muốn | Ý nghĩa trong PHM |
| :--- | :--- | :---: | :--- |
| **Độ chính xác RUL** | RMSE, MAE, Score | RMSE/MAE thấp, Score cao | Dự báo tuổi thọ chính xác từng giờ/vòng quay; đảm bảo an toàn. |
| **Phân loại lỗi** | F1-Score, Accuracy | Cao (tiến về 100%) | Phân loại đúng loại lỗi (vòng trong, vòng ngoài, con lăn). |
| **Độ nhạy phát hiện** | Detection Delay, Recall | Thấp (càng ngắn càng tốt) | Cảnh báo hỏng hóc ngay khi vết nứt vừa chớm nở. |
| **Độ tin cậy hệ thống** | False Alarm Rate, Precision | Cực thấp (lý tưởng < 5%) | Không gây dừng máy "oan", giảm lãng phí nguồn lực. |
| **Theo dõi xu hướng** | Anomaly Score, Threshold Chart | Tăng dần theo suy thoái | Giám sát trực quan lộ trình vết mòn đang lớn dần theo thời gian. |

# 8. Xác định lỗ hổng nghiên cứu (Research Gaps)

Mặc dù các phương pháp học sâu đã đạt được những bước tiến đáng kể trong việc giám sát sức khỏe vòng bi, việc triển khai chúng trong môi trường công nghiệp thực tế vẫn đối mặt với ba rào cản lớn về kiến trúc, tính bền vững và khả năng thích ứng.

---

## 8.1 Lỗ hổng về kiến trúc (Architecture Gap)

Các kiến trúc hiện tại thường gặp khó khăn trong việc cân bằng giữa khả năng biểu diễn và chi phí tính toán khi xử lý dữ liệu cảm biến tần suất cao:

*   **Transformer**: Mặc dù mạnh mẽ trong việc nắm bắt bối cảnh toàn cầu, nhưng cơ chế tự chú ý (Self-Attention) có độ phức tạp tính toán và bộ nhớ tăng theo hàm bình phương $O(L^2)$ so với chiều dài chuỗi $L$. Điều này tạo ra một "trần kinh tế" và kỹ thuật, khiến việc triển khai cho các chuỗi thời gian siêu dài (như dữ liệu rung động liên tục) trở nên cực kỳ tốn kém và khó khả thi trên các thiết bị biên (edge devices).
*   **LSTM & TCN**: 
    *   **LSTM** bị hạn chế bởi tính toán tuần tự, không thể song song hóa hiệu quả và dễ bị hiện tượng bão hòa thông tin trong chuỗi cực dài. 
    *   **TCN** dù có thể song song hóa nhưng trường thụ cảm vẫn mang tính cục bộ, khó có thể "hiểu" được toàn bộ quỹ đạo suy thoái phức tạp của vòng bi xuyên suốt vòng đời.
*   **Tiềm năng của Mamba**: Các mô hình không gian trạng thái chọn lọc (**Selective SSM**) như Mamba cung cấp độ phức tạp tuyến tính $O(L)$. Tuy nhiên, việc thiết kế các khối hybrid để kết hợp khả năng trích xuất đặc trưng không gian của CNN và khả năng lọc thông tin chọn lọc của Mamba vẫn còn là một hướng nghiên cứu mới, chưa được khai phá sâu trong lĩnh vực PHM (Prognostics and Health Management).

---

## 8.2 Lỗ hổng về tính bền vững (Robustness Gap)

Hiệu suất mô hình thường giảm mạnh khi chuyển từ phòng thí nghiệm ra môi trường thực tế:

*   **Nhiễu công nghiệp**: Các tín hiệu hỏng hóc sớm thường rất yếu và dễ bị che lấp bởi nhiễu điện từ hoặc rung động từ các máy móc lân cận. Các mô hình hiện tại thiếu khả năng "lọc chọn lọc" để tách biệt tín hiệu suy thoái thực sự khỏi các thành phần nhiễu không dừng.
*   **Báo động giả (False Alarms)**: Việc tránh báo động giả gây ra bởi quá trình chạy rà (running-in) hoặc thay đổi chế độ bôi trơn là một thách thức lớn. Các phương pháp dựa trên ngưỡng cố định truyền thống thường dẫn đến tỷ lệ báo động giả cao hoặc bỏ lỡ các dấu hiệu hỏng hóc sớm quan trọng.

---

## 8.3 Lỗ hổng về khả năng tổng quát hóa (Generalization Gap)

Đây là rào cản lớn nhất cho việc thương mại hóa các mô hình bảo trì dự đoán:

*   **Sự dịch chuyển miền (Domain Shift)**: Trong thực tế, sự thay đổi về tải trọng, tốc độ quay và đặc tính riêng biệt của từng máy khiến mô hình mất độ chính xác khi áp dụng vào một thiết bị mới (**unseen machine**) có phân phối dữ liệu khác với tập huấn luyện.
*   **Thiếu dữ liệu lỗi**: Dữ liệu "chạy đến khi hỏng" (**run-to-failure**) cực kỳ khan hiếm và khó thu thập. Điều này dẫn đến việc các mô hình dễ bị quá khớp (**overfitting**) trên các kịch bản lỗi hạn chế trong khi máy móc thực tế chủ yếu hoạt động ở trạng thái bình thường.

# 9. Định vị nghiên cứu (Positioning)

Dựa trên việc phân tích các phương pháp hiện hữu, nghiên cứu này kế thừa khả năng tự động học đặc trưng từ dữ liệu rung động của các mô hình học sâu, đồng thời trực tiếp giải quyết các rào cản kỹ thuật về chi phí tính toán và khả năng mô hình hóa chuỗi thời gian siêu dài.

Nghiên cứu này đề xuất mô hình **Hybrid Mamba-CNN** với các định vị chiến lược như sau:

*   **Tận dụng ưu thế bổ trợ**: Nghiên cứu tận dụng khả năng của **CNN** trong việc trích xuất các đặc trưng không gian cục bộ từ hình ảnh phổ thời-tần (**Scalogram qua CWT**), giúp nhận diện chính xác các xung va chạm nhỏ do vết nứt gây ra. Đồng thời, tích hợp khối **Mamba (Selective State Space Model)** để đóng vai trò "bộ nhớ toàn cầu", liên kết các đặc trưng này thành một lộ trình suy thoái nhất quán xuyên suốt vòng đời của thiết bị.
*   **Đột phá về hiệu năng tính toán**: Khác với các kiến trúc Transformer truyền thống gặp hiện tượng nghẽn bộ nhớ do độ phức tạp $O(L^2)$, mô hình đề xuất sử dụng cơ chế quét chọn lọc (**Selective Scan**) của Mamba để đạt được độ phức tạp tuyến tính $O(L)$. Cải tiến này cho phép xử lý dữ liệu cảm biến tần suất cao với tốc độ suy luận nhanh hơn và tiết kiệm tài nguyên GPU hơn đáng kể so với các baseline hiện nay.
*   **Cân bằng giữa độ chính xác và tính ứng dụng**: Nghiên cứu hướng tới việc phá vỡ sự đánh đổi giữa hiệu suất dự báo và chi phí tài nguyên. Bằng cách kết hợp CNN và Mamba, mô hình không chỉ đạt được độ chính xác **SOTA (State-of-the-Art)** trong dự đoán RUL mà còn mở ra khả năng triển khai thực tế trên các thiết bị giám sát biên (**Edge Deployment**) – nơi có tài nguyên tính toán hạn chế mà các mô hình Transformer hay LSTM nặng nề chưa làm tốt.

# 10. Kết luận

Tóm lại, các phương pháp tiếp cận dựa trên AI hiện nay đã đạt được những tiến bộ đáng kể trong bài toán giám sát sức khỏe vòng bi, trải qua quá trình tiến hóa từ các mô hình học máy dựa trên đặc trưng thủ công (**handcrafted features**) sang các kiến trúc học sâu (**Deep Learning**) và mô hình hóa chuỗi tiên tiến. 

Tuy nhiên, một số thách thức cốt lõi vẫn còn tồn tại, bao gồm:
*   **Khả năng tổng quát hóa**: Còn hạn chế đối với các thiết bị chưa từng xuất hiện trong tập huấn luyện.
*   **Tính bền vững**: Hiệu suất giảm trong môi trường nhiễu công nghiệp phức tạp.
*   **Tính diễn giải (Explainability)**: Khó khăn trong việc giải thích các quyết định của mô hình "hộp đen".
*   **Chi phí tính toán**: Sự nghẽn cổ chai khi xử lý dữ liệu cảm biến siêu dài bằng kiến trúc Transformer với độ phức tạp $O(L^2)$.

Những hạn chế này là động lực chính cho việc phát triển mô hình **Hybrid Mamba-CNN** trong nghiên cứu này. Mô hình đề xuất nhằm mục tiêu tối ưu hóa đồng thời khả năng trích xuất đặc trưng không gian cục bộ và mô hình hóa các phụ thuộc thời gian dài hạn với độ phức tạp tính toán tuyến tính $O(L)$. Qua đó, giải pháp này hướng tới việc đảm bảo hiệu suất tính toán vượt trội, độ tin cậy cao trong chẩn đoán và khả năng ứng dụng thực tế trên các thiết bị giám sát tại hiện trường (**field-level monitoring**).
