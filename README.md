# DỰ ĐOÁN GIÁ NHÀ VÀ XỬ LÝ OVERFITTING

## 1. Giới thiệu

Bài tập thực hiện xây dựng mô hình Machine Learning để dự đoán giá nhà
dựa trên dữ liệu nhà ở trong file `Housing.xlsx`.

Mục tiêu của bài:

- Xây dựng mô hình dự đoán giá nhà.
- Chia dữ liệu thành tập Train và Test.
- Huấn luyện mô hình.
- Đánh giá mô hình.
- Tạo ra hiện tượng Overfitting.
- Phân tích dấu hiệu của Overfitting.
- Sử dụng kỹ thuật để giảm Overfitting.
- So sánh kết quả với các giá trị `max_depth` khác nhau.

---

## 2. Dữ liệu

File dữ liệu:

`Housing.xlsx`

Dữ liệu gồm:

- 545 dòng
- 13 thuộc tính

Các thuộc tính được sử dụng để xây dựng mô hình:

- `area`: diện tích nhà
- `bedrooms`: số phòng ngủ
- `bathrooms`: số phòng tắm
- `stories`: số tầng
- `parking`: số chỗ đỗ xe

Biến mục tiêu:

- `price`: giá nhà

Trong bài này, `price` là biến cần dự đoán.

---

## 3. Chia dữ liệu

Dữ liệu được chia thành:

- 80% dữ liệu dùng để Train.
- 20% dữ liệu dùng để Test.

Kết quả:

- Train: 436 mẫu
- Test: 109 mẫu

Sử dụng:

```python
train_test_split(
    X,
    y,
    test_size=0.2,
    random_state=42
)
