# DỰ ĐOÁN GIÁ NHÀ VÀ XỬ LÝ OVERFITTING

## 1. Giới thiệu

Bài tập xây dựng và huấn luyện mô hình Machine Learning để dự đoán giá nhà từ bộ dữ liệu `Housing.xlsx`.

Mục tiêu:
- Xây dựng và huấn luyện mô hình.
- Đánh giá mô hình.
- Tạo hiện tượng Overfitting.
- Phân tích và khắc phục Overfitting.

## 2. Dữ liệu

File: `Housing.xlsx`

- 545 dòng
- 13 thuộc tính

Các thuộc tính sử dụng:
- `area`: diện tích
- `bedrooms`: số phòng ngủ
- `bathrooms`: số phòng tắm
- `stories`: số tầng
- `parking`: số chỗ đỗ xe

Biến mục tiêu: `price` (giá nhà).

## 3. Chia dữ liệu

Dữ liệu được chia theo tỷ lệ:
- Train: 80% = 436 mẫu
- Test: 20% = 109 mẫu

```python
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)
```

## 4. Tạo Overfitting

Sử dụng mô hình **Decision Tree Regression**.

Để tạo Overfitting, không giới hạn độ sâu của cây:

```python
model = DecisionTreeRegressor(
    max_depth=None,
    random_state=42
)
```

Huấn luyện mô hình:

```python
model.fit(X_train, y_train)
```

### Kết quả

| Chỉ số | Train | Test |
|---|---:|---:|
| R2 | 0.9780 | 0.1126 |
| MSE | 67,774,792,048.93 | 4,485,381,933,539.65 |

R2 Train rất cao nhưng R2 Test thấp:

```text
0.9780 - 0.1126 = 0.8654
```

Mô hình học quá sát dữ liệu Train nhưng dự đoán kém trên Test, cho thấy hiện tượng **Overfitting**.

## 5. Khắc phục Overfitting

Sử dụng kỹ thuật **Tree Pruning**, giới hạn độ sâu của Decision Tree bằng `max_depth`.

Thử nghiệm:

```text
None, 3, 5, 7, 10
```

Kết quả:

| max_depth | R2 Train | R2 Test |
|---:|---:|---:|
| None | 0.9780 | 0.1126 |
| 3 | 0.5773 | 0.3828 |
| 5 | 0.6829 | 0.4337 |
| 7 | 0.8053 | 0.3901 |
| 10 | 0.9234 | 0.2756 |

Với `max_depth=5` trong các giá trị đã thử:

```text
R2 Train = 0.6829
R2 Test  = 0.4337
```

R2 Test tăng từ **0.1126 lên 0.4337**, đồng thời MSE Test giảm từ **4,485,381,933,539.65 xuống 2,862,224,410,232.33**.

Điều này cho thấy việc giới hạn độ sâu giúp giảm Overfitting và cải thiện khả năng dự đoán trên tập Test.

## 6. Kết luận

Bài tập đã thực hiện đầy đủ quá trình:

**Dữ liệu → Chia Train/Test → Xây dựng và huấn luyện mô hình → Tạo Overfitting → Phân tích → Tree Pruning → So sánh kết quả.**

Kỹ thuật `max_depth` giúp kiểm soát độ phức tạp của Decision Tree và giảm hiện tượng Overfitting.

## 7. Cấu trúc thư mục

```text
OVERFITTING/
├── Housing.xlsx
├── README.md
├── du_bao_gia_nha.py
├── tao_overfitting.py
└── fix_overfitting.py
```
