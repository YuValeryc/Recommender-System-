# Triển khai các thuật toán Lọc cộng tác (Collaborative Filtering)

Chào mừng bạn đến với repo triển khai các kỹ thuật Lọc cộng tác (CF) cơ bản và nâng cao cho Hệ thống gợi ý. Mục tiêu của dự án này là cung cấp một cái nhìn tổng quan, dễ hiểu kèm theo code minh họa cho từng phương pháp.

## 📚 Mục lục

1.  [Cấu trúc dự án](#cấu-trúc-dự-án)
2.  [Dữ liệu](#dữ-liệu)
3.  [Cài đặt](#cài-đặt)
4.  [Tổng quan các Notebook](#tổng-quan-các-notebook)
    -   [Notebook 1: Lọc cộng tác dựa trên User (User-Based CF)](#notebook-1)
    -   [Notebook 2: Lọc cộng tác dựa trên Item (Item-Based CF)](#notebook-2)
    -   [Notebook 3: Xử lý dữ liệu thưa & Cold Start](#notebook-3)
    -   [Notebook 4: Phân rã ma trận (Matrix Factorization)](#notebook-4)
5.  [Metric đánh giá](#metric-đánh-giá)
6.  [Đóng góp](#đóng-góp)

## 📂 Cấu trúc dự án

```
recommender-systems-cf/
├── README.md
├── requirements.txt
├── data/
├── notebooks/
└── src/
```
- **`notebooks/`**: Chứa code triển khai chính cho từng thuật toán.
- **`data/`**: Chứa bộ dữ liệu MovieLens 100k.
- **`src/`**: Chứa các hàm tiện ích được sử dụng trong các notebook.

## 🗃️ Dữ liệu

Dự án này sử dụng bộ dữ liệu [MovieLens 100k](https://grouplens.org/datasets/movielens/100k/). Bộ dữ liệu này chứa 100,000 ratings từ 943 users cho 1682 bộ phim.

Để sử dụng, hãy tải và giải nén dữ liệu vào thư mục `data/`.

## ⚙️ Cài đặt

1.  Clone repo này:
    ```bash
    git clone https://github.com/your-username/recommender-systems-cf.git
    cd recommender-systems-cf
    ```

2.  Cài đặt các thư viện cần thiết:
    ```bash
    pip install -r requirements.txt
    ```

## 📓 Tổng quan các Notebook

### <a id="notebook-1"></a>Notebook 1: `01_user_based_CF.ipynb`

-   **Ý tưởng**: "Những người dùng giống nhau sẽ thích những item giống nhau."
-   **Kỹ thuật**:
    -   Xây dựng ma trận User-Item.
    -   Tính toán độ tương đồng giữa các user (Cosine Similarity, Pearson Correlation).
    -   Tìm `K` láng giềng gần nhất (K-Nearest Neighbors).
    -   Dự đoán rating của một user cho một item chưa được đánh giá.

### <a id="notebook-2"></a>Notebook 2: `02_item_based_CF.ipynb`

-   **Ý tưởng**: "Nếu bạn thích một item, bạn cũng sẽ thích các item tương tự."
-   **Kỹ thuật**:
    -   Tính toán độ tương đồng giữa các item.
    -   Tạo ma trận Item-Item Similarity (bước tiền xử lý quan trọng).
    -   Dự đoán rating dựa trên các item tương tự mà user đã đánh giá cao.

### <a id="notebook-3"></a>Notebook 3: `03_sparse_matrix_problems.ipynb`

-   **Vấn đề**: Giải quyết vấn đề "Cold Start" (user/item mới) và ma trận rating cực kỳ thưa.
-   **Giải pháp**:
    -   Gán giá trị mặc định (trung bình toàn cục, trung bình của item).
    -   Sử dụng các phương pháp dựa trên đồ thị (Graph-based methods) để tìm các liên kết gián tiếp.

### <a id="notebook-4"></a>Notebook 4: `04_matrix_factorization.ipynb`

-   **Ý tưởng**: Phân rã ma trận User-Item thành hai ma trận đặc trưng (latent factors) cho user và item.
-   **Kỹ thuật**:
    -   Mô hình hóa: `r̂_ui ≈ U_u^T * V_i`.
    -   Tối ưu hóa bằng **Stochastic Gradient Descent (SGD)**.
    -   Mở rộng với **Regularization** (chống overfitting) và **Bias terms** (để mô hình chính xác hơn).

## 📈 Metric đánh giá

-   **RMSE (Root Mean Squared Error)** và **MAE (Mean Absolute Error)** để đo lường độ chính xác của rating dự đoán.
-   **Precision@K / Recall@K** để đánh giá chất lượng của danh sách Top-N item gợi ý.

## 🤝 Đóng góp

Mọi đóng góp đều được chào đón! Vui lòng tạo một Pull Request hoặc mở một Issue để thảo luận.