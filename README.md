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
## 4. Tạo mô hình Overfitting

Sau khi chia dữ liệu thành tập Train và Test, bài sử dụng mô hình **Decision Tree Regression** để dự đoán giá nhà.

Decision Tree là mô hình có khả năng chia dữ liệu thành nhiều nhóm dựa trên các thuộc tính đầu vào. Nếu cây phát triển quá sâu, mô hình có thể học quá chi tiết dữ liệu Train, bao gồm cả những đặc điểm riêng hoặc nhiễu của dữ liệu. Khi đó mô hình hoạt động rất tốt trên tập Train nhưng dự đoán không tốt trên tập Test. Đây là hiện tượng **Overfitting**.

### 4.1. Các thuộc tính sử dụng

Mô hình sử dụng 5 thuộc tính đầu vào:

- `area`: diện tích nhà
- `bedrooms`: số phòng ngủ
- `bathrooms`: số phòng tắm
- `stories`: số tầng
- `parking`: số chỗ đỗ xe

Biến mục tiêu cần dự đoán:

- `price`: giá nhà

### 4.2. Xây dựng và huấn luyện mô hình

Để cố tình tạo ra hiện tượng Overfitting, Decision Tree được thiết lập với:

```python
model = DecisionTreeRegressor(
    max_depth=None,
    random_state=42
)
