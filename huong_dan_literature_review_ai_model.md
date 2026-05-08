# Hướng Dẫn Viết Literature Review Về AI Models / Methods

## 1. Mục tiêu của file này

File này dùng để hướng dẫn người viết hoặc AI Agent thực hiện **literature review tập trung vào mô hình AI, thuật toán, pipeline, hoặc phương pháp xử lý**.

Trọng tâm của file này là:

- Các nghiên cứu trước dùng mô hình AI nào?
- Mô hình đó giải quyết bài toán gì?
- Input/output của mô hình là gì?
- Mô hình có ưu điểm gì?
- Mô hình còn hạn chế gì?
- Các phương pháp đang phát triển theo xu hướng nào?
- Gap về phương pháp, kiến trúc, evaluation, explainability, deployment là gì?
- Nghiên cứu hiện tại sẽ định vị khác gì so với các bài trước?

---

## 2. Khi nào nên dùng file này?

Dùng file này khi mục tiêu review là:

- Review các mô hình AI đã được dùng trong lĩnh vực nghiên cứu.
- So sánh traditional machine learning, deep learning, Transformer, Mamba, LLM, RAG, AI Agent.
- Tìm method gap hoặc architecture gap.
- Viết phần “Related Work”, “AI Methods”, “Model Review”, “Existing Approaches”.
- Xây dựng hướng đề xuất mô hình mới.
- So sánh pipeline hiện tại với các phương pháp trước.

Ví dụ chủ đề phù hợp:

- CNN/LSTM/Transformer/Mamba for fault diagnosis.
- Deep learning for medical image classification.
- RAG systems for document question answering.
- AI Agent for software engineering.
- LLM-based research assistant.
- Computer vision models for agriculture.
- Time-series forecasting models.

---

## 3. Cấu trúc Literature Review về AI Models

### 3.1 Giới thiệu bài toán AI

Cần nói rõ:

- Bài toán AI là gì?
- Input là gì?
- Output là gì?
- Mục tiêu tối ưu là gì?
- Vì sao cần AI cho bài toán này?

Mẫu viết:

```text
Artificial intelligence has been widely applied to [research problem] due to its ability to learn complex patterns from high-dimensional data. Existing studies have explored different categories of models, ranging from traditional machine learning to deep neural networks and recent foundation models. This section reviews these methods in terms of input representation, model architecture, performance, limitations, and relevance to the current study.
```

---

### 3.2 Phân nhóm phương pháp AI

Không nên review từng bài rời rạc. Nên nhóm theo phương pháp.

Các nhóm thường gặp:

| Nhóm phương pháp | Ví dụ |
|---|---|
| Traditional Machine Learning | SVM, Random Forest, KNN, XGBoost |
| Deep Learning | CNN, RNN, LSTM, GRU, Autoencoder |
| Attention-based Models | Transformer, ViT, Informer |
| State Space Models | Mamba, S4 |
| Graph Models | GCN, GAT, GraphSAGE |
| Generative Models | GAN, VAE, Diffusion |
| Foundation Models | LLM, Vision-Language Model |
| RAG Systems | Retriever, Reranker, Generator |
| AI Agents | Planner, Tool Calling, Multi-agent systems |
| Hybrid Models | CNN-LSTM, CNN-Transformer, Mamba-Transformer |

---

## 4. Review Traditional Machine Learning

Phần này dùng khi các nghiên cứu ban đầu sử dụng ML cổ điển.

Cần phân tích:

- Feature đầu vào là gì?
- Có cần feature engineering không?
- Model nào được dùng?
- Vì sao model phù hợp?
- Hạn chế khi so với deep learning là gì?

Mẫu viết:

```text
Early studies often relied on traditional machine learning models such as SVM, Random Forest, and KNN. These methods usually require handcrafted features extracted from the original data, including statistical, frequency-domain, or domain-specific descriptors. Although traditional models are computationally efficient and easier to interpret, their performance depends heavily on feature engineering and may be limited when dealing with complex nonlinear patterns.
```

---

## 5. Review Deep Learning Models

Phần này dùng cho CNN, RNN, LSTM, Autoencoder, Transformer, v.v.

Cần phân tích:

- Model học đặc trưng như thế nào?
- Input representation là gì?
- Model mạnh ở điểm nào?
- Có cần nhiều dữ liệu không?
- Có dễ overfit không?
- Có giải thích được không?

### 5.1 CNN-based methods

Phù hợp với:

- Image.
- Spectrogram.
- Time-frequency representation.
- Spatial feature extraction.

Mẫu viết:

```text
CNN-based methods have been widely adopted because they can automatically learn local patterns from image-like or time-frequency representations. In vibration-based diagnosis, raw signals are often transformed into spectrograms before being fed into CNN architectures. These models usually achieve high classification accuracy, but their performance may depend on preprocessing choices and may not generalize well under domain shift.
```

### 5.2 RNN/LSTM/GRU-based methods

Phù hợp với:

- Sequential data.
- Time-series.
- Temporal dependency.
- Sensor sequences.

Mẫu viết:

```text
RNN-based models, especially LSTM and GRU, are commonly used to capture temporal dependencies in sequential data. They are suitable for time-series forecasting and degradation modeling. However, they may suffer from limited long-range dependency modeling and slower training compared with attention-based or state-space architectures.
```

### 5.3 Transformer-based methods

Phù hợp với:

- Long sequence modeling.
- Attention.
- Multimodal learning.
- NLP, time-series, vision.

Mẫu viết:

```text
Transformer-based models have attracted increasing attention due to their self-attention mechanism, which enables them to capture long-range dependencies. They have shown strong performance in NLP, computer vision, and time-series tasks. However, their computational cost can be high, especially for long input sequences, and they often require large datasets for stable training.
```

### 5.4 Mamba / State Space Models

Phù hợp với:

- Long sequence.
- Efficient sequence modeling.
- Time-series.
- Sensor data.
- Prognostics.

Mẫu viết:

```text
Recent state-space models such as Mamba have been proposed as efficient alternatives to Transformer architectures for long sequence modeling. By combining selective state-space mechanisms with linear-time sequence processing, these models can potentially handle long time-series data more efficiently. Nevertheless, their application in domain-specific tasks such as fault diagnosis and prognostics remains relatively underexplored.
```

---

## 6. Review RAG / LLM / AI Agent Methods

Dùng cho các bài liên quan đến document QA, AI Agent, scientific assistant, enterprise knowledge system.

### 6.1 RAG systems

Cần review:

- Document ingestion.
- Chunking.
- Embedding model.
- Vector database.
- Retriever.
- Reranker.
- Generator.
- Evaluation.

Mẫu viết:

```text
Retrieval-Augmented Generation has become a common approach for knowledge-intensive question answering. Instead of relying only on parametric knowledge, RAG systems retrieve relevant external documents and use them as context for generation. However, system performance is sensitive to chunking strategy, embedding quality, retrieval accuracy, context selection, and hallucination control.
```

### 6.2 LLM-based methods

Cần review:

- LLM dùng làm gì?
- Classification, summarization, reasoning, generation hay planning?
- Có fine-tune không?
- Có dùng prompt engineering không?
- Có kiểm soát hallucination không?

Mẫu viết:

```text
Large language models have demonstrated strong capabilities in reasoning, summarization, and natural language generation. In research-oriented systems, LLMs can assist in extracting information, generating hypotheses, and synthesizing literature. However, their outputs may suffer from hallucination, lack of grounding, and sensitivity to prompt design.
```

### 6.3 AI Agent methods

Cần review:

- Agent có planner không?
- Có tool calling không?
- Có memory không?
- Có multi-agent không?
- Có evaluation về task success không?

Mẫu viết:

```text
AI agent systems extend LLM-based approaches by incorporating planning, tool use, memory, and iterative decision-making. These systems are suitable for complex workflows that require multiple steps, such as document analysis, data retrieval, and experiment orchestration. However, evaluating agent reliability remains challenging because failures may occur at different stages of reasoning, tool selection, or execution.
```

---

## 7. Review Input Representation và Feature Learning

Mô hình AI không thể tách khỏi cách biểu diễn dữ liệu.

Cần phân tích:

| Data type | Input representation |
|---|---|
| Time-series | Raw waveform, statistical features, FFT, STFT, wavelet |
| Image | Raw image, patch embedding, segmentation mask |
| Text | Token, embedding, chunk, document graph |
| Sensor | Windowed sequence, feature vector, multimodal fusion |
| RAG | Chunks, embeddings, metadata, retrieved context |
| Multimodal | Concatenation, attention fusion, late fusion |

Mẫu viết:

```text
Input representation significantly affects model performance. Some studies use handcrafted features to reduce dimensionality, while others transform raw data into representations suitable for deep learning models. For example, time-series signals can be represented as raw sequences, frequency-domain features, or time-frequency spectrograms. Each representation introduces different trade-offs between information preservation, computational cost, and model complexity.
```

---

## 8. Review Experimental Design

Khi review AI methods, phải xem thí nghiệm có công bằng không.

Cần kiểm tra:

- Có baseline không?
- Có ablation study không?
- Có nhiều dataset không?
- Có kiểm tra generalization không?
- Có kiểm tra robustness không?
- Có so sánh cost/latency không?
- Có report hyperparameters không?
- Có public code không?

Bảng gợi ý:

```markdown
| Paper | Model | Baseline | Ablation | Dataset | Split | Metrics | Reproducibility | Main Risk |
|---|---|---|---|---|---|---|---|---|
| P01 | CNN | SVM | No | CWRU | Random | Accuracy | Medium | Overestimated result |
| P02 | Transformer | CNN/LSTM | Yes | XJTU-SY | Temporal | F1 | High | High computational cost |
```

---

## 9. Review Evaluation Metrics

Tuỳ bài toán mà metrics khác nhau.

### 9.1 Classification

- Accuracy.
- Precision.
- Recall.
- F1-score.
- Macro-F1.
- Confusion matrix.
- AUC.

### 9.2 Fault diagnosis / imbalanced data

- Macro-F1.
- Per-class F1.
- Recall for fault class.
- False alarm rate.
- Miss detection rate.

### 9.3 Forecasting / regression

- MAE.
- RMSE.
- MAPE.
- R².

### 9.4 RAG / LLM

- Answer correctness.
- Faithfulness.
- Context precision.
- Context recall.
- Hallucination rate.
- Latency.
- Token cost.
- Human evaluation.

### 9.5 AI Agent

- Task success rate.
- Tool-use accuracy.
- Planning correctness.
- Step efficiency.
- Error recovery rate.
- Cost.
- Safety violation rate.

---

## 10. Literature Matrix cho AI Method Review

```markdown
| ID | Paper | Year | Task | Model/Method | Input Representation | Dataset | Baseline | Metrics | Key Result | Method Limitation | Relevance |
|---|---|---|---|---|---|---|---|---|---|---|---|
| P01 | ... | 2024 | Classification | CNN | STFT spectrogram | ... | SVM | Accuracy | ... | Weak generalization | Baseline |
| P02 | ... | 2025 | Forecasting | Transformer | Time-series window | ... | LSTM | RMSE | ... | High cost | Compare method |
| P03 | ... | 2025 | QA | RAG | Chunk embedding | ... | BM25 | Faithfulness | ... | Retrieval errors | Related pipeline |
```

---

## 11. Các dạng AI/method gap thường gặp

### 11.1 Generalization gap

Mô hình tốt trên dataset đã thấy nhưng yếu khi đổi domain.

```text
Although existing models achieve high performance on benchmark datasets, their ability to generalize to unseen domains and operating conditions remains limited.
```

### 11.2 Robustness gap

Mô hình nhạy với noise, missing data, hoặc input không ổn định.

```text
Most existing methods are evaluated under relatively clean data conditions, while their robustness to noise, missing values, and sensor disturbances has not been sufficiently examined.
```

### 11.3 Architecture gap

Kiến trúc hiện tại chưa khai thác tốt đặc điểm dữ liệu.

```text
Existing architectures often fail to jointly capture local patterns and long-range dependencies, which are both important for complex sequential data.
```

### 11.4 Explainability gap

Mô hình dự đoán tốt nhưng khó giải thích.

```text
Despite achieving high accuracy, many deep learning models remain black-box systems, making it difficult to interpret the reasoning behind their predictions.
```

### 11.5 Evaluation gap

Cách đánh giá chưa phản ánh thực tế.

```text
Many studies rely mainly on accuracy under random splitting protocols, which may not reflect real-world deployment performance.
```

### 11.6 Deployment gap

Mô hình quá nặng hoặc khó triển khai.

```text
Although complex models improve predictive performance, their high computational cost may limit deployment in resource-constrained environments.
```

### 11.7 RAG/LLM reliability gap

Hệ thống sinh câu trả lời nhưng chưa kiểm soát hallucination tốt.

```text
Current RAG-based systems still face challenges related to retrieval errors, hallucination, context selection, and answer faithfulness.
```

### 11.8 Agent reliability gap

Agent làm được nhiều bước nhưng khó đảm bảo ổn định.

```text
AI agents can automate complex workflows, but their reliability is affected by planning errors, incorrect tool selection, and weak failure recovery mechanisms.
```

---

## 12. Cách viết đoạn tổng hợp AI Method Review

Không nên viết:

```text
Paper A used CNN. Paper B used LSTM. Paper C used Transformer.
```

Nên viết:

```text
Existing AI methods show a clear transition from handcrafted feature-based machine learning to deep learning architectures capable of automatic representation learning. CNN-based models are effective for extracting local patterns from image-like representations, while recurrent and attention-based models are more suitable for sequential dependencies. More recently, state-space models and foundation-model-based systems have been explored to improve long-sequence modeling and reasoning capabilities. However, challenges remain in terms of generalization, robustness, explainability, and deployment efficiency.
```

---

## 13. Cấu trúc đề xuất cho section AI Method Review

```markdown
## 2. Related Work

### 2.1 Traditional Machine Learning Approaches
- Review các phương pháp ML cổ điển.
- Nêu ưu điểm, hạn chế.

### 2.2 Deep Learning-based Approaches
- Review CNN, RNN, LSTM, Autoencoder.
- Phân tích input representation và kết quả.

### 2.3 Attention-based and Advanced Sequence Models
- Review Transformer, ViT, Mamba, S4.
- Phân tích khả năng học long-range dependency.

### 2.4 Hybrid and Multimodal Methods
- Review các mô hình kết hợp.
- Phân tích fusion strategy.

### 2.5 RAG, LLM, or AI Agent-based Methods
- Chỉ dùng mục này nếu bài có liên quan.
- Review retriever, generator, tool calling, memory, planning.

### 2.6 Comparative Analysis
- So sánh nhóm phương pháp theo performance, cost, robustness, explainability.

### 2.7 Method-related Research Gaps
- Tổng hợp gap về kiến trúc, robustness, explainability, deployment.

### 2.8 Positioning of This Study
- Nêu nghiên cứu hiện tại kế thừa gì và cải tiến gì.
```

---

## 14. Checklist đọc paper để review AI method

```markdown
- [ ] Bài báo giải quyết task gì?
- [ ] Input của model là gì?
- [ ] Output của model là gì?
- [ ] Model chính là gì?
- [ ] Vì sao tác giả chọn model đó?
- [ ] Có preprocessing hoặc feature engineering không?
- [ ] Có baseline không?
- [ ] Có ablation study không?
- [ ] Có so sánh với SOTA không?
- [ ] Có dùng dataset phù hợp không?
- [ ] Có split dữ liệu hợp lý không?
- [ ] Có metric phù hợp không?
- [ ] Có phân tích lỗi không?
- [ ] Có kiểm tra robustness không?
- [ ] Có kiểm tra explainability không?
- [ ] Có nói về computational cost không?
- [ ] Có public code không?
- [ ] Hạn chế chính của method là gì?
- [ ] Bài này liên quan gì đến nghiên cứu của mình?
```

---

## 15. Output mong muốn sau khi review AI method

Sau khi hoàn thành review AI method, cần tạo được:

1. Danh sách các nhóm phương pháp đã được dùng.
2. Bảng so sánh model/method.
3. Phân tích xu hướng phát triển của phương pháp.
4. Nhận xét ưu/nhược điểm của từng nhóm.
5. Các method gap chính.
6. Lý do chọn hoặc đề xuất mô hình hiện tại.
7. Baseline cần so sánh.
8. Metrics và evaluation protocol phù hợp.

---

## 16. Mẫu kết luận AI Method Review

```text
In summary, existing AI-based approaches have achieved significant progress in [research topic], evolving from handcrafted feature-based models to deep learning and advanced sequence architectures. However, several challenges remain, including limited generalization, weak robustness under noisy or shifted data distributions, insufficient explainability, and high computational cost. These limitations motivate the development of [proposed method], which aims to [main improvement] while maintaining [efficiency/reliability/interpretability].
```
