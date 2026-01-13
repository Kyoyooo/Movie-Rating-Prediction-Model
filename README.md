# DỰ ĐOÁN ĐIỂM RATING CỦA CÁC BỘ PHIM

## Mục lục

1. [Giới thiệu](#1-giới-thiệu)
2. [Nguồn dữ liệu và mô tả dữ liệu](#2-nguồn-dữ-liệu-và-mô-tả-dữ-liệu)
3. [Quy trình](#3-quy-trình)
4. [Cấu trúc thư mục](#4-cấu-trúc-thư-mục)
5. [Cài đặt và setup môi trường](#5-cài-đặt-và-setup-môi-trường)
6. [Giấy phép](#6-giấy-phép)

---

## Thông tin thành viên:

| STT | Họ và tên         | MSSV     |
| --- | ----------------- | -------- |
| 1   | Nguyễn Tuấn Phong | 23120071 |
| 2   | Võ Trần Duy Hoàng | 23120266 |
| 3   | Y Nguyên Mlô      | 23120299 |
| 4   | Nguyễn Đăng Pha   | 23120315 |

---

## 1. Giới thiệu

Trong bối cảnh ngành công nghiệp điện ảnh ngày càng phát triển, số lượng phim được phát hành mỗi năm là rất lớn, kéo theo nhu cầu đánh giá và lựa chọn phim của người xem ngày càng cao. Điểm rating của phim, đặc biệt từ các nền tảng uy tín như IMDB, đóng vai trò quan trọng trong việc phản ánh chất lượng và mức độ đón nhận của khán giả đối với từng bộ phim.

Dữ liệu được thu thập từ website IMDB thông qua kỹ thuật web crawling. Nhóm tiến hành các bước khám phá dữ liệu (EDA), đặt câu hỏi khai thác insight và thực hiện xây dựng mô hình học máy dự đoán điểm rating của phim dựa trên các đặc trưng như: thể loại, năm phát hành, ngân sách và các đặc trưng liên quan khác.

---

## 2. Nguồn dữ liệu và mô tả dữ liệu

- **Nguồn dữ liệu**: Dữ liệu được thu thập thông qua kỹ thuật web crawling từ trang IMDB.(https://www.imdb.com/search/title/?title_type=feature)
- **Tổng quan dữ liệu**: Bộ dữ liệu bao gồm thông tin về các bộ phim phổ biến, được sắp xếp theo thứ tự mức độ phổ biến giảm dần. Việc lựa chọn nhóm phim phổ biến nhằm giảm thiểu tỷ lệ giá trị bị thiếu (missing values) so với phương pháp thu thập phim ngẫu nhiên. Dữ liệu được thu thập vào tháng 12 năm 2025.
- **Kích thước dữ liệu**:
  - 10.048 dòng
  - 10 thuộc tính

### Các feature:

| Tên thuộc tính | Mô tả                                                              |
| -------------- | ------------------------------------------------------------------ |
| `rank`         | Xếp hạng mức độ phổ biến của bộ phim                               |
| `title`        | Tiêu đề của phim                                                   |
| `genres`       | Các thể loại của bộ phim                                           |
| `budget`       | Ngân sách của phim (USD)                                           |
| `release_year` | Năm phát hành                                                      |
| `run_time`     | Thời lượng phim (phút)                                             |
| `mpa`          | Phân loại độ tuổi theo tiêu chuẩn MPA (Motion Picture Association) |
| `metascore`    | Điểm đánh giá từ nhà phê bình/chuyên môn (0–100)                   |
| `vote_count`   | Số lượng lượt đánh giá của người dùng                              |
| `rating`       | Điểm rating trung bình của bộ phim trên IMDB (0–10)                |

- **Đặc điểm dữ liệu**:
  - Missing value khá nhiều ở cột `budget` (33.88%) và `metascore`(23.98%).
  - Các giá trị ở các cột cần numerical kèm theo đơn vị, cần được clean và thống nhất đơn vị.
  - Tính chính xác dữ liệu (Data validation): hợp lệ ở các cột.
  - Phần lớn phim từ năm 2000 trở về sau.

---

## 3. Quy trình

Thu thập dữ liệu → Khám phá dữ liệu (EDA) → Đặt câu hỏi và khai thác insight → Xây dựng mô hình dự đoán điểm rating.

---

## 4. Cấu trúc thư mục

```text

├── data
│   ├── raw                         # Dataset ban đầu sau khi crawl
│   │   └── IMDB_movies_final.csv
│   ├── clean                       # Dataset sau khi chuẩn hóa, clean các cột
│   │   └── IMDB_movies.csv
│   └── processed                   # Data sau khi tiền xử lí cho model
│       ├── train_processed.csv
│       └── test_processed.csv
│
├── notebooks
│   ├── crawl_imdb.ipynb            # Crawl data
│   ├── data_exploration.ipynb      # Khám phá dữ liệu (EDA)
│   ├── Question1.ipynb             # Phương pháp xử lí missing value nào tối ưu nhất để bảo toàn cấu trúc phân phối thống kê
│   ├── Question2.ipynb             # Ngân sách sản xuất có thực sự quyết định chất lượng và mức độ đón nhận của phim
│   ├── Question3.ipynb             # Thể loại và MPA ảnh hưởng ra sao đến đánh giá của giới phê bình và khán giả
│   ├── Question4.ipynb             # Những bộ phim có thời lượng dài (vd > 2 tiếng) có xu hướng đạt điểm cao hơn phim ngắn không
│   ├── Question5.ipynb             # Phân loại các nhóm phim phổ biến-chất lượng, phân tích các tệp khán giả trong mỗi nhóm
│   └── Model.ipynb                 # Sử dụng Linear regression, Random forest, Catboost để dự đoán rating
│
├── README.md
└── requirements.txt
```

---

## 5. Cài đặt và setup môi trường

### 5.1 Yêu cầu môi trường

- Python >= 3.8
- pip (Python package manager)
- Trình duyệt Microsoft Edge(phục vụ web crawling)

### 5.2 Cài đặt các thư viện cần thiết

- Clone project và cài đặt các thư viện trong file `requirements.txt`: **pip install -r requirements.txt**

- Đồ án sử dụng Selenium để crawl dữ liệu từ IMDB, do đó cần cài đặt WebDriver tương ứng với trình duyệt: https://developer.microsoft.com/en-us/microsoft-edge/tools/webdriver/?form=MA13LH Stable Channel phiên bản x64

### 5.3 Hướng dẫn thực thi

- Run `crawl_imdb.ipynb`: để crawl data gốc và tạo `IMDB_movies_final.csv`
- Run `data_exploration.ipynb`: Khám phá và làm sạch dữ liệu, đồng thời tạo các file `IMDB_movies.csv` (dữ liệu đã được clean) và `train_processed.csv`, `test_processed.csv` (dữ liệu đã được tiền xử lý để phục vụ huấn luyện mô hình).
- Run các Question.ipynb: để xem insight dữ liệu
- Run `Model.ipynb`: để xây dựng model dự đoán rating

---

## 6. Giấy phép

- Dữ liệu trong dự án được thu thập từ website IMDB và chỉ được sử dụng cho mục đích học tập, nghiên cứu phi thương mại.
- Việc thu thập dữ liệu tuân thủ các quy định được nêu trong file robots.txt của IMDB: https://www.imdb.com/robots.txt
