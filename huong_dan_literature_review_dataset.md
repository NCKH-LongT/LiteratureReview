# Hướng Dẫn Viết Literature Review Về Dataset

## 1. Mục tiêu của file này

File này dùng để hướng dẫn người viết hoặc AI Agent thực hiện **literature review tập trung vào dataset** trong các bài báo nghiên cứu AI.

Khi sử dụng file này, trọng tâm không phải là mô hình AI nào tốt nhất, mà là:

- Dataset được dùng là gì?
- Dataset đến từ nguồn nào?
- Dataset có đáng tin cậy không?
- Dataset có đủ phù hợp với bài toán nghiên cứu không?
- Dataset có hạn chế gì?
- Các bài báo trước đã dùng dataset như thế nào?
- Dataset có gây ra bias, data leakage, domain shift hoặc thiếu tính thực tế không?
- Có cần đề xuất dataset mới, benchmark mới, hoặc cách đánh giá mới không?

---

## 2. Khi nào nên dùng file này?

Dùng file này khi mục tiêu review là:

- Tìm dataset phù hợp cho bài báo.
- So sánh các dataset đã được dùng trong lĩnh vực nghiên cứu.
- Phân tích điểm mạnh/yếu của dataset.
- Đánh giá độ tin cậy của dataset.
- Tìm research gap liên quan đến dữ liệu.
- Viết phần “Dataset Review”, “Data Sources”, “Benchmark Datasets” hoặc “Data-related Limitations”.

Ví dụ chủ đề phù hợp:

- Bearing fault diagnosis datasets.
- Medical image datasets.
- Agricultural disease image datasets.
- IoT sensor datasets.
- RAG document datasets.
- Time-series forecasting datasets.
- Human activity recognition datasets.
- Multimodal datasets.

---

## 3. Cấu trúc Literature Review về Dataset

### 3.1 Giới thiệu vai trò của dataset

Phần này giải thích vì sao dataset quan trọng trong bài toán nghiên cứu.

Cần trả lời:

- Bài toán nghiên cứu cần loại dữ liệu nào?
- Dataset ảnh hưởng thế nào đến hiệu quả mô hình?
- Vì sao cần review dataset trước khi chọn phương pháp?
- Dataset hiện có đã đủ phản ánh thực tế chưa?

Mẫu viết:

```text
Datasets play a critical role in the development and evaluation of AI-based systems because model performance strongly depends on data quality, labeling strategy, diversity, and distribution. In the context of [research domain], existing studies have used different datasets to train and evaluate their models. Therefore, reviewing dataset characteristics is necessary to understand the reliability, reproducibility, and generalizability of previous findings.
```

---

### 3.2 Nguồn dataset

Phân loại dataset theo nguồn gốc.

Có thể chia thành:

| Loại dataset | Mô tả |
|---|---|
| Public benchmark dataset | Dataset công khai, thường dùng để so sánh mô hình |
| Private dataset | Dataset tự thu thập, không công khai |
| Industrial dataset | Dataset từ môi trường sản xuất/thực tế |
| Laboratory dataset | Dataset thu trong phòng thí nghiệm |
| Simulated dataset | Dataset mô phỏng |
| Synthetic dataset | Dataset sinh nhân tạo |
| Multimodal dataset | Dataset gồm nhiều loại dữ liệu, ví dụ vibration + temperature |

Cần đánh giá:

- Dataset có public không?
- Có DOI, paper mô tả, hoặc link chính thức không?
- Có đủ thông tin thu thập dữ liệu không?
- Có thể tái lập nghiên cứu không?

---

### 3.3 Đặc điểm kỹ thuật của dataset

Mỗi dataset cần được mô tả theo các tiêu chí sau:

| Tiêu chí | Câu hỏi cần trả lời |
|---|---|
| Domain | Dataset thuộc lĩnh vực nào? |
| Data type | Ảnh, text, time-series, âm thanh, bảng, sensor, multimodal? |
| Sample size | Có bao nhiêu mẫu? |
| Classes/labels | Có bao nhiêu nhãn? Nhãn là gì? |
| Sampling rate | Nếu là tín hiệu, tần số lấy mẫu là bao nhiêu? |
| Duration | Nếu là chuỗi thời gian, mỗi mẫu dài bao lâu? |
| Collection condition | Dữ liệu thu trong lab hay thực tế? |
| Annotation method | Ai/cách nào gán nhãn? |
| Missing data | Có thiếu dữ liệu không? |
| Noise | Có nhiễu không? |
| Imbalance | Có mất cân bằng class không? |
| Metadata | Có metadata hỗ trợ không? |

---

### 3.4 Phân tích chất lượng dataset

Không chỉ mô tả dataset, cần đánh giá chất lượng.

Các yếu tố cần xem:

#### 3.4.1 Representativeness

Dataset có đại diện cho bài toán thực tế không?

Ví dụ:

- Dataset chỉ thu trong phòng lab có thể không đại diện cho môi trường công nghiệp thật.
- Dataset ảnh bệnh cây có nền sạch có thể không đại diện cho ảnh chụp ngoài đồng.
- Dataset RAG chỉ gồm tài liệu sạch có thể không đại diện cho tài liệu doanh nghiệp lộn xộn.

#### 3.4.2 Diversity

Dataset có đa dạng không?

Cần xem:

- Có nhiều điều kiện vận hành không?
- Có nhiều loại lỗi không?
- Có nhiều domain không?
- Có nhiều thiết bị/cảm biến không?
- Có nhiều nhóm người/đối tượng không?
- Có nhiều ngôn ngữ không?

#### 3.4.3 Label quality

Nhãn có đáng tin cậy không?

Cần xem:

- Nhãn do chuyên gia hay tự động?
- Có mô tả quy trình gán nhãn không?
- Có inter-annotator agreement không?
- Có nhãn mơ hồ không?
- Có class bị thiếu không?

#### 3.4.4 Data distribution

Phân phối dữ liệu có vấn đề không?

Cần xem:

- Class imbalance.
- Domain shift.
- Covariate shift.
- Temporal drift.
- Sensor drift.
- Distribution mismatch giữa train và test.

#### 3.4.5 Reproducibility

Dataset có hỗ trợ tái lập nghiên cứu không?

Cần xem:

- Public dataset không?
- Có license không?
- Có mô tả cấu trúc file không?
- Có script xử lý dữ liệu không?
- Có train/test split chuẩn không?

---

## 4. Review cách các bài báo trước sử dụng dataset

Khi đọc từng bài báo, cần ghi lại:

```markdown
## Paper ID / Title

### Dataset Used
- Tên dataset:
- Public/private:
- Link/DOI:
- Domain:
- Data type:
- Size:
- Labels/classes:
- Collection condition:

### How the Dataset Was Used
- Dùng để train, validation hay test?
- Có chia window/chunk/sample không?
- Có augmentation không?
- Có lọc dữ liệu không?
- Có kết hợp với dataset khác không?

### Split Strategy
- Random split?
- Cross-validation?
- File-wise split?
- Subject-wise split?
- Temporal split?
- Cross-domain split?

### Dataset-related Strength
- Dataset phù hợp điểm nào?
- Có điểm gì tốt hơn các dataset khác?

### Dataset-related Limitation
- Dataset nhỏ?
- Thiếu class?
- Lab-only?
- Không thực tế?
- Có nguy cơ leakage?
- Không public?
- Không có metadata?
- Không có benchmark split?

### Relevance to My Study
- Dataset này có thể dùng không?
- Có thể làm baseline không?
- Có thể dùng để so sánh không?
- Có cần bổ sung dataset khác không?
```

---

## 5. Literature Matrix cho Dataset Review

Dùng bảng này để tổng hợp các bài báo.

```markdown
| ID | Paper | Year | Dataset | Public/Private | Data Type | Size | Labels | Collection Condition | Split Strategy | Dataset Strength | Dataset Limitation | Relevance |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| P01 | ... | 2024 | ... | Public | Time-series | ... | ... | Lab | Random | Easy benchmark | Leakage risk | Baseline |
| P02 | ... | 2025 | ... | Private | Sensor | ... | ... | Real-world | Temporal | Practical data | Not reproducible | Compare limitation |
```

---

## 6. Các dạng dataset gap thường gặp

### 6.1 Dataset size gap

Dataset quá nhỏ, không đủ để mô hình học tốt.

Mẫu viết:

```text
Although previous studies have reported promising results, most of them rely on relatively small datasets. This limits the robustness of the findings and increases the risk of overfitting.
```

### 6.2 Real-world gap

Dataset chủ yếu thu trong môi trường lý tưởng.

```text
Most existing datasets are collected under controlled laboratory conditions, while real-world environments contain noise, variable operating conditions, and unpredictable disturbances.
```

### 6.3 Domain shift gap

Train và test khác phân phối.

```text
Existing datasets often lack cross-domain evaluation settings, making it difficult to assess whether models can generalize to unseen operating conditions or new environments.
```

### 6.4 Label limitation gap

Nhãn chưa đủ chi tiết hoặc chưa đáng tin cậy.

```text
The reliability of model evaluation is affected by limited or coarse-grained labels, especially when the transition between normal, degrading, and faulty states is not clearly annotated.
```

### 6.5 Reproducibility gap

Dataset không public hoặc thiếu mô tả.

```text
Several studies use private datasets without releasing raw data or preprocessing scripts, which reduces reproducibility and makes fair comparison difficult.
```

### 6.6 Temporal evaluation gap

Dataset có tính thời gian nhưng lại bị chia random.

```text
For time-series and run-to-failure datasets, random splitting may introduce data leakage because adjacent windows from the same sequence can appear in both training and testing sets.
```

### 6.7 Multimodal gap

Chưa tận dụng nhiều nguồn dữ liệu.

```text
Although many real-world systems generate multiple sensor signals, most datasets and studies rely on a single modality, limiting the ability to capture complementary information.
```

---

## 7. Cách viết đoạn tổng hợp dataset review

Không nên viết:

```text
Paper A used dataset X. Paper B used dataset Y. Paper C used dataset Z.
```

Nên viết theo nhóm phân tích:

```text
Existing studies commonly rely on benchmark datasets because they provide accessible and standardized data for model evaluation. However, these datasets are often collected under controlled conditions and may not fully represent real-world operational variability. In contrast, private industrial datasets provide more practical scenarios but usually lack public availability, making reproducibility and fair comparison difficult. This indicates a need for more transparent, diverse, and leakage-aware datasets in future research.
```

---

## 8. Cấu trúc đề xuất cho section Dataset Review

```markdown
## 2. Dataset Review

### 2.1 Role of Dataset in the Research Problem
- Giải thích vai trò của dataset đối với bài toán.

### 2.2 Overview of Existing Datasets
- Liệt kê và mô tả các dataset chính.

### 2.3 Dataset Characteristics
- Phân tích data type, size, labels, collection condition, metadata.

### 2.4 Dataset Usage in Previous Studies
- Các bài trước dùng dataset để train/test như thế nào.

### 2.5 Dataset Quality and Limitations
- Phân tích noise, imbalance, domain shift, label quality, reproducibility.

### 2.6 Dataset-related Research Gaps
- Chỉ ra các gap liên quan đến dữ liệu.

### 2.7 Implications for This Study
- Nêu dataset nào sẽ dùng, vì sao chọn, và cách khắc phục hạn chế.
```

---

## 9. Checklist đánh giá dataset

Trước khi chọn dataset cho bài báo, cần kiểm tra:

```markdown
- [ ] Dataset có phù hợp trực tiếp với bài toán nghiên cứu không?
- [ ] Dataset có nguồn chính thức không?
- [ ] Dataset có public không?
- [ ] Dataset có license rõ ràng không?
- [ ] Dataset có paper mô tả không?
- [ ] Dataset có đủ số lượng mẫu không?
- [ ] Dataset có nhãn rõ ràng không?
- [ ] Dataset có metadata không?
- [ ] Dataset có class imbalance không?
- [ ] Dataset có noise/missing values không?
- [ ] Dataset có phản ánh môi trường thực tế không?
- [ ] Dataset có nguy cơ data leakage không?
- [ ] Dataset có benchmark split chuẩn không?
- [ ] Dataset có thể dùng để so sánh với các bài trước không?
- [ ] Dataset có hỗ trợ kiểm tra domain shift hoặc temporal split không?
```

---

## 10. Output mong muốn sau khi review dataset

Sau khi hoàn thành review dataset, cần tạo được:

1. Danh sách dataset liên quan.
2. Bảng so sánh dataset.
3. Phân tích điểm mạnh/yếu của từng dataset.
4. Nhận xét dataset nào phù hợp nhất cho nghiên cứu.
5. Các dataset gap chính.
6. Lý do chọn dataset cho bài hiện tại.
7. Rủi ro khi sử dụng dataset.
8. Kế hoạch xử lý dữ liệu và split dữ liệu.

---

## 11. Mẫu kết luận Dataset Review

```text
In summary, existing datasets have enabled significant progress in [research topic]. However, many commonly used datasets still suffer from limitations such as controlled collection environments, limited diversity, unclear labeling strategies, and potential data leakage caused by inappropriate splitting protocols. These limitations suggest that dataset selection and evaluation design should be carefully considered. Therefore, this study selects [dataset name] because [reason], and adopts [split/evaluation strategy] to improve reliability and reduce the risk of overestimated performance.
```
