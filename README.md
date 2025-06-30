# LAB-3-NMXLAS
# **Nhập Môn Xử Lý Ảnh Số - Lab 3**
----------------------------------------------------------------------------------------------------------------
# **Biến Đổi Hình Học**
----------------------------------------------------------------------------------------------------------------
- **Sinh viên thực hiện:** Bùi Chí Kiệt
- **Môn học:** Nhập môn Xử lý ảnh số
- **Giảng viên:** Đỗ Hữu Quân

## Giới thiệu
----------------------------------------------------------------------------------------------------------------
Bài lab này nhằm mục đích thực hiện các phép biến đổi hình học trong ảnh – là những thao tác cơ bản, nền tảng trong lĩnh vực xử lý ảnh số. Các biến đổi này giúp:

### **Chọn đối tượng trong ảnh**
### **Tịnh tiến ảnh**
### **Thay đổi kích thước ảnh**
### **Xoay ảnh**
### **Biến đổi cực**
----------------------------------------------------------------------------------------------------------------
- Python: Ngôn ngữ chính
- NumPy: Xử lý ảnh dưới dạng mảng số học
- ImageIO: Đọc file ảnh với định dạng hiện đại
- Matplotlib: Hiển thị ảnh trực quan
- Scipy-Ndimage: Xử lý và biến đổi ảnh

## **Chi tiết các phép biến đổi & công thức**
----------------------------------------------------------------------------------------------------------------
**Phép chọn đối tượng trong ảnh (Object Selection/Image Segmentation)**

* Mục đích:
- Tách vùng quan tâm ra khỏi nền
- Tiền xử lý cho các bước phân tích sau
- Loại bỏ nhiễu, giảm lỗi

* Code chính
<pre>data = iio.imread("Tên file hình ảnh")
bmg = data[y1:y2, x1:x2]
[y1:y2, x1:x2] là giá trị của vùng bạn muốn cắt
Ví dụ: y1 = 100, y2 = 300, x1 = 200, x2 = 400
bmg = data[100:300, 200:400]
y1, y2 là hàng từ 100 đến 299 
x1, x2 là cột từ 200 đến 399 </pre>
----------------------------------------------------------------------------------------------------------------
**Phép tịnh tiến ảnh (Image Translation)**

* Mục đích:
- Dịch chuyển đối tượng để dễ thao tác
- Nếu đối tượng không nằm ở vị trí mong muốn, dịch trước khi tính toán hình học
- Trước khi áp dụng các phép biến đổi khác: cắt, xoay, phóng to

* Công thức toán học
- Nếu (𝑥,𝑦)(x,y) là điểm ảnh gốc, thì sau khi tịnh tiến:
- (x′,y′)=(x+dx,y+dy)
* Trong đó:
- dx: dịch ngang (trục x)
- dy: dịch dọc (trục y)
- Dịch sang phải dx > 0, sang trái dx < 0
- Dịch xuống dy > 0, dịch lên dy < 0

* Code chính
<pre>Ví dụ: Tịnh tiến hình sang phải 30 pixel
Sử dụng thư viện scipy.ndimage để dễ thao tác

import scipy.ndimage as nd
data = iio.imread("Tên file hình ảnh")
cdata = nd.shift(data, (0, 30, 0))</pre>
----------------------------------------------------------------------------------------------------------------
**Phép thay đổi kích thước ảnh (Image Scaling)**

* Mục đích:
- Làm ảnh lớn hơn (phóng to) hoặc nhỏ hơn (thu nhỏ)
- Đưa ảnh về kích thước chuẩn (ví dụ 256×256) để làm đầu vào cho các thuật toán xử lý (nhận dạng, học máy)
- Giảm dung lượng lưu trữ hoặc tăng tốc độ xử lý (ví dụ resize ảnh trước khi tải lên web)

* Công thức toán học
- Giả sử như (x, y) là điểm ảnh gốc, (Sx, Sy) là tỷ lệ phóng theo chiều ngang và dọc
- Sau khi thay đổi kích thước: (x', y') = (Sx.x, Sy.y)
- Điều kiện: Phóng to S > 1, Thu nhỏ S < 1

* Code chính
<pre>Ví dụ: Tăng kích thước ảnh lên 5 lần
import scipy.ndimage as nd
data = iio.imread("Tên file hình ảnh")
date2 = nd.zoom(data, (5, 5, 1))
(5, 5, 1) có nghĩa là tăng 5 lần chiều cao, 5 lần chiều rộng, kênh màu giữ nguyên</pre>
----------------------------------------------------------------------------------------------------------------
**Phép xoay ảnh (Image Rotation)**

* Mục đích:
- Đưa ảnh về hướng mong muốn
- Chuẩn hóa góc của đối tượng trước khi so khớp hình dạng, nhận dạng ký tự, OCR,...
* Công thức toán học
- Xoay ảnh là xoay hệ tọa độ điểm (x, y) quanh tâm gốc (0,0) hoặc một điểm cố định (x0, y0).
- Công thức xoay điểm (x, y) quanh gốc:
- [x', y'] = [cos(alp) -sin(alp), cos(alp) sin(alp)].[x y]
- Trong đó : alp là góc xoay (đơn vị: độ hoặc radian)
- Xoay thuận chiều kim đồng hồ: alp < 0
- Xoay ngược chiều kim đồng hồ: alp > 0
* Code chính
<pre>Ví dụ: Xoay hình ảnh góc 45 độ
import scipy.ndimage as nd
import imageio.v2 as iio
data = iio.imread("Tên file hình ảnh")
rotate = nd.rotate(data, 45)</pre>
----------------------------------------------------------------------------------------------------------------

## Cấu Trúc File
<pre>
├── exercise/
│   ├── colorful-ripe-tropical-fruits.jpg
│   ├── pagoda.jpg
│   ├── quang_ninh.jpg
│   ├── ha-long-bay-in-vietnam.jpg
├── BAITAP1.ipynb
├── BAITAP2.ipynb    
├── BAITAP3.ipynb 
├── BAITAP4.ipynb          
├── BAITAP5.ipynb 
├── README.md </pre>
----------------------------------------------------------------------------------------------------------------

Hướng dẫn
1. Cài đặt môi trường
<pre>pip install pillow numpy matplotlib imageio</pre>
2. Chạy notebook
- Mở Jupyter Notebook trên VSCode
- Nếu có lỗi không tìm thấy ảnh, đảm bảo file ảnh đã được đặt đúng vị trí
----------------------------------------------------------------------------------------------------------------

Tài liệu tham khảo
Slide bài giảng Nhập môn Xử lý ảnh số - Văn Lang University
