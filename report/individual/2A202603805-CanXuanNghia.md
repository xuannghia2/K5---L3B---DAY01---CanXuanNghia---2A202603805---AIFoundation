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
