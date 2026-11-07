# Báo cáo cá nhân — Day 01: Lọc tin nhắn rác bằng ML, DL, Embedding và LLM

> Đổi tên file này thành `MSSV_HoTen.md` của bạn, ví dụ `2A20260000_NguyenVanAn.md`, rồi điền từng mục. Xoá các dòng hướng dẫn in nghiêng khi xong.

- **MSSV:** 2A202603537
- **Họ và tên:** Nguyễn Thị Hồng Hạnh 
- **SEED** (in ở ô đầu notebook): 4354

## 1. Bằng chứng

| Tệp | Có? |
| --- | --- |
| [`day01_lab.ipynb`](day01_lab.ipynb) — notebook đã chạy, còn output | ☐ |
| [`lab1_report.json`](lab1_report.json) — do ô "Báo cáo cuối" sinh ra | ☐ |
| [`hand_calc.jpg`](hand_calc.jpg) — ảnh tính tay có các bước | ☐ |

## 2. Kết quả chính

1. BoW + LogReg (tự code)            1.000   0.815      0.898        0.919   
2. BoW + MLP (deep learning)         0.979   0.852      0.911        0.919   
3a. Encoder (MiniLM) + kNN           0.866   0.954      0.907        0.895   
3b. Encoder (MiniLM) + LogReg        1.000   0.926      0.962        0.947   
3c. Encoder (MiniLM) + MLP head      0.981   0.935      0.957        0.947   
4a. LLM nhỏ zero-shot                0.000   0.000      0.000        0.000   
4b. LLM lớn zero-shot                0.000   0.000      0.000        0.000   
4c. LLM nhỏ few-shot                 0.000   0.000      0.000        0.000   

                                 train (s)  tin/s (cả lô)  p50 ms/tin  \
1. BoW + LogReg (tự code)            2.959      23046.006       0.054   
2. BoW + MLP (deep learning)         7.813      12119.465       0.234   
3a. Encoder (MiniLM) + kNN          82.549         31.411      34.685   
3b. Encoder (MiniLM) + LogReg       82.978         34.268      21.461   
3c. Encoder (MiniLM) + MLP head     83.427         34.895      29.657   
4a. LLM nhỏ zero-shot                0.000          1.526     583.912   
4b. LLM lớn zero-shot                0.000          1.289     772.029   
4c. LLM nhỏ few-shot                 0.000          1.551     627.247   

                                 p95 ms/tin  USD / 1k tin  
1. BoW + LogReg (tự code)             0.079         0.000  
2. BoW + MLP (deep learning)          2.260         0.000  
3a. Encoder (MiniLM) + kNN           50.444         0.000  
3b. Encoder (MiniLM) + LogReg        30.152         0.000  
3c. Encoder (MiniLM) + MLP head      47.475         0.000  
4a. LLM nhỏ zero-shot              1070.585         0.010  
4b. LLM lớn zero-shot               937.325         0.105  
4c. LLM nhỏ few-shot                858.313         0.027  
• Hàng LLM chỉ đo trên SUB (40 tin) → so sánh chất lượng công bằng bằng cột 'F1 (SUB 40)'.
• SUB chỉ 40 tin: 1 tin sai đổi F1 vài điểm. Chênh < ~0.05 F1 coi như HOÀ — đừng xếp hạng theo số lẻ.
• Inference đo TỪ VĂN BẢN THÔ → NHÃN (gồm cả vectorize / encode). p50/p95 = gọi từng tin một, như một request thật.
• train (s) của 3a/3b/3c = thời gian encoder MiniLM encode tập train (+ train đầu LogReg / MLP); LLM = 0 vì không train. Số đo phụ thuộc CPU/GPU của Colab.

## 3. Dự đoán và thực tế

*Chọn 3 dự đoán `predict(...)` lệch nhiều nhất so với kết quả. Mỗi cái: bạn đoán gì, ra gì, vì sao lệch.*

## 4. Phân tích 50 case khó

*Model nào tụt nhiều nhất, ở nhóm case nào? Nêu 2 case cụ thể và cơ chế khiến model sai.*
So sánh "F1 50 case khó" với "F1 test thường". Model BoW + LogReg tụt nhiều nhất. Vì trên test thường model có thể nhận diện các từ khoá quen thuộc của tin spam. Bộ stress test lại đưa né từ khoá, viết như hội thoại và tin hợp lệ nên dấu hiệu kém tin cậy hơn.

## 5. Thử thách cá nhân

*Đề theo SEED của bạn, cách làm, kết quả, giải thích.*

## 6. Phương án cho sản phẩm thật

*Với yêu cầu p95 < 50 ms/tin cho 10 triệu SMS/ngày: chọn phương án nào, dẫn số liệu nào, chấp nhận đánh đổi gì.*

## 7. AI log và điều đã học

*Mỗi lần dùng AI: hỏi gì, nhận gì, bạn sửa gì. Sau đó 2–3 câu: điều bạn hiểu ra hôm nay mà trước đó chưa hiểu.*
