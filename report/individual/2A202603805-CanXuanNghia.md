                                F1 test thường (SUB)  F1 50 case khó  
1. BoW + LogReg                                0.919           0.378   
2. BoW + MLP                                   0.919           0.378   
3a. Emb + kNN                                  0.974           0.691   
3b. Emb + LogReg                               0.974           0.667   
3c. Emb + MLP head                             0.947           0.667   
4a. LLM nhỏ zero-shot                          0.947           0.982   
4d. LLM nhỏ + prompt phòng thủ                 0.947           1.000   

                                acc 50 case khó  
1. BoW + LogReg                            0.54  
2. BoW + MLP                               0.54  
3a. Emb + kNN                              0.66  
3b. Emb + LogReg                           0.66  
3c. Emb + MLP head                         0.66  
4a. LLM nhỏ zero-shot                      0.98  
4d. LLM nhỏ + prompt phòng thủ             1.00
<img width="1077" height="237" alt="image" src="https://github.com/user-attachments/assets/69857639-516f-4362-8769-8213611bb807" />

SEED=9627 · thử thách #4
Bộ kiểm tra: 15/15 đạt
  ✅ 1.1 vectorize
  ✅ 1.2 sigmoid / predict_proba
  ✅ 1.3 train_logreg
  ✅ 1.4 metrics
  ✅ 2.1 build_mlp
  ✅ 2.2 train_mlp
  ✅ 3.1–3.2 cosine / top_k_similar
  ✅ 3.3 knn_predict
  ✅ 4.2–4.3 prompt / parse_label
  ✅ 4.1 + 4.4 call_openai / llm_classify_batch
  ✅ tính tay: baseline_accuracy
  ✅ tính tay: sigmoid_0
  ✅ tính tay: f1_example
  ✅ tính tay: cosine_example
  ✅ tính tay: llm_cost_per_day

Dự đoán đã ghi:
  [14:58:55] ml_f1: F1 trên test khoảng 0.90, precision sẽ cao hơn recall vì mô hình học trên tập dữ liệu bị mất cân bằng (ít spam hơn).
  [14:58:59] ml_lr: lr=0.001 thì loss giảm rất chậm và giảm thoải nhẹ nhàng , lr=50 thì loss sẽ dao động mạnh hình zigzag hoặc không hội tụ.
  [14:59:18] dl_curve: Val loss sẽ không giảm mãi mà sẽ tăng lên khi bắt đầu overfit. F1 của MLP có thể không khác biệt lớn so với logistic regression.
  [14:59:24] dl_relu: Nếu bỏ ReLU, mạng 2 lớp Linear liên tiếp sẽ bị gộp lại thành 1 phép biến đổi tuyến tính duy nhất, tương đương với mô hình Logistic Regression ở Phần 1. F1 sẽ giảm hoặc quay về mức của mô hình LogReg.
  [15:01:43] emb_search: Kết quả gần nhất sẽ là spam vì mô hình embedding có thể hiểu ngữ nghĩa của câu dù không có các từ khóa spam quen thuộc.
  [15:02:32] emb_tricky: Mô hình 3b. Encoder + LogReg sẽ đoán đúng nhiều hơn vì embedding hiểu được ngữ nghĩa và ngữ cảnh của câu, thay vì chỉ khớp từ khóa cứng nhắc như BoW.
  [15:06:24] llm_models: Model lớn (gpt-6.1-terra) sẽ có F1 cao hơn model nhỏ khoảng 0.02-0.05 nhưng chi phí đắt gấp ~10 lần. So với 3b (Embedding + LogReg), LLM zero-shot có F1 tương đương (~0.95) nhưng độ trễ và chi phí cao hơn rất nhiều.
  [15:35:46] llm_fewshot: F1 có thể tăng nhẹ hoặc giữ nguyên vì zero-shot đã làm rất tốt, nhưng chi phí mỗi tin sẽ tăng lên rất nhiều lần (khoảng 3-5 lần). Nguyên nhân là do phần prompt input bị phình to ra vì phải chứa thêm 4 tin nhắn ví dụ.
  [15:38:53] hard_eval: Accuracy của mọi model sẽ giảm mạnh. Nhóm khó nhất với BoW là 'Né từ khoá' và 'Tưởng spam nhưng không phải'. LLM sẽ xử lý tốt ngữ cảnh nhưng dễ bị lừa bởi nhóm 'Prompt injection'.
Thiếu dự đoán: ['tradeoff']

                                     f1  f1_SUB
1. BoW + LogReg (tự code)        0.919   0.919
2. BoW + MLP (deep learning)     0.945   0.919
3a. Encoder (MiniLM) + kNN       0.896   0.974
3b. Encoder (MiniLM) + LogReg    0.965   0.974
3c. Encoder (MiniLM) + MLP head  0.947   0.947
4a. LLM nhỏ zero-shot            0.947   0.947
4c. LLM nhỏ few-shot             0.947   0.947

