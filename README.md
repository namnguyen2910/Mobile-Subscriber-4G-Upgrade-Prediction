# 📱 Mobile Subscriber 4G Upgrade Prediction

Dự án phân tích và xây dựng mô hình Machine Learning dự đoán khả năng thuê bao di động chuyển sang sử dụng 4G, dựa trên dữ liệu hành vi sử dụng dịch vụ.

---

## 🛠️ Công nghệ sử dụng

![Python](https://img.shields.io/badge/Python-3.x-3776AB?style=flat&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat&logo=pandas&logoColor=white)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-F7931E?style=flat&logo=scikit-learn&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-11557C?style=flat)
![Seaborn](https://img.shields.io/badge/Seaborn-4C72B0?style=flat)

**Python Libraries:** Pandas | Matplotlib | Seaborn | Scikit-learn  
**Data Processing:** Xử lý NULL | Label Encoding | MinMaxScaler | Feature Engineering  
**Machine Learning:** Logistic Regression | SVM | Decision Tree | Random Forest  
**Evaluation:** Confusion Matrix | Precision | Recall | F1-Score | AUC

---

## 🗂️ Cấu trúc dự án

```
├── DA_TEST_NAMNT.ipynb       # Notebook chính
├── data_test_uv.CSV          # Dữ liệu đầu vào
└── README.md
```

---

## 📦 Tập dữ liệu

- **Kích thước:** 200.000 dòng × 182 cột
- **Biến danh mục:** `thiet_bi`, `ha_tang`, `tuoi_khach_hang_cut_level`
- **Biến nhị phân:** `thuc_4g`, `is_dcom`, `is_sim_4g`
- **Biến số:** `cuoc_goc_gprs`, `nod_psll_thoai`, `so_lan_nap_the`, `nod_psll_data`, `so_lan_nap_topup`... (17 biến, mỗi biến có 10 giá trị tương ứng 10 tháng gần nhất)
- **Giá trị NULL:** 12.262 giá trị
- **Biến mục tiêu:** `thuc_4g` — `1` = chuyển sang 4G, `0` = không chuyển

---

## 🔍 Phương pháp thực hiện

### B1 – Xử lý tiền dữ liệu
- Thay thế giá trị NULL của biến số bằng `0`
- Label Encoding cho biến `ha_tang`, `thiet_bi`
- One-Hot Encoding cho biến `tuoi_khach_hang`
- Xây dựng tập dữ liệu theo chuỗi thời gian 5 tháng liên tiếp, chuẩn hóa tên feature theo từng kỳ
- Gán nhãn target và lọc các thuê bao trùng lặp giữa nhóm 0 và 1

### B2 – Chuẩn bị dữ liệu đầu vào
- Tách features (X) / target (y)
- Chuẩn hóa toàn bộ features về [0, 1] bằng MinMaxScaler
- Chia tập train/test theo tỷ lệ 80/20 (`random_state=42`)

### B3 – Huấn luyện mô hình
So sánh 4 mô hình phân loại:

| Mô hình | Tham số |
|---|---|
| Logistic Regression | max_iter=250 |
| LinearSVC | default |
| Decision Tree | max_depth=16, min_samples_split=7, max_leaf_nodes=30 |
| Random Forest | n_estimators=100, max_depth=10, min_samples_split=6 |

### B4 – Đánh giá kết quả
- So sánh Train/Val Score để phát hiện overfitting
- Confusion Matrix trực quan hóa kết quả dự đoán
- Báo cáo Precision, Recall, F1-Score và AUC theo từng mô hình

---

## 📊 Kết quả

### Độ chính xác (Train / Val Score)

| Mô hình | Train Score | Val Score |
|---|:---:|:---:|
| 🥇 Random Forest | 83.54% | 81.61% |
| 🥈 Decision Tree | 79.17% | 79.03% |
| 🥉 Support Vector Machines | 77.43% | 77.54% |
| Logistic Regression | 77.42% | 77.43% |

### Precision / Recall / F1-Score

| Mô hình | Precision | Recall | F1-Score |
|---|:---:|:---:|:---:|
| 🥇 Random Forest | 0.77 | 0.67 | **0.72** |
| Decision Tree | 0.74 | 0.63 | 0.68 |
| Logistic Regression | 0.69 | 0.65 | 0.67 |
| SVM | 0.69 | 0.66 | 0.67 |

### AUC Score

| Mô hình | AUC |
|---|:---:|
| 🥇 Random Forest | **0.88** |
| Decision Tree | 0.84 |
| Logistic Regression | 0.83 |
| SVM | 0.83 |

---

## 🏆 Kết luận

**Random Forest** là mô hình tốt nhất với:
- AUC cao nhất **(0.88)** — khả năng phân loại vượt trội
- F1-Score cao nhất **(0.72)** — cân bằng tốt giữa Precision và Recall
- Chênh lệch Train/Val thấp — ít bị overfitting nhờ tổng hợp nhiều cây quyết định

✅ **Khuyến nghị:** Sử dụng **Random Forest** cho bài toán dự đoán thuê bao chuyển sang 4G.

---

## 💡 Đề xuất phát triển

- **Bổ sung đặc trưng mới:** Các đặc trưng hiện tại còn hạn chế — cần thu thập thêm dữ liệu hành vi người dùng
- **Xử lý outlier:** Áp dụng log transformation để giảm ảnh hưởng của giá trị ngoại lệ lớn
- **Ensemble nâng cao:** Kết hợp Random Forest với Gradient Boosting (XGBoost, LightGBM) để cải thiện hiệu suất

---

## ▶️ Hướng dẫn chạy

```bash
# Cài đặt thư viện
pip install pandas matplotlib seaborn scikit-learn

# Mở notebook
jupyter notebook DA_TEST_NAMNT.ipynb
```

> ⚠️ Đảm bảo file `data_test_uv.CSV` nằm cùng thư mục với notebook.

---

## 👤 Tác giả

**NAMNT** – Data Analyst
