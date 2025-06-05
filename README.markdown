# PHÂN TÍCH - TRỰC QUAN HÓA DỮ LIỆU - XÂY DỰNG DASHBOARD TÌNH TRẠNG NGHỈ VIỆC CỦA NHÂN VIÊN

## Mô tả dự án
Dự án này phân tích tập dữ liệu **Employee-turnover.csv** (1,470 dòng, 29 cột) từ Kaggle để xác định các yếu tố ảnh hưởng đến tỷ lệ nghỉ việc (Attrition) của nhân viên. Dự án bao gồm các bước tiền xử lý dữ liệu bằng Python, trực quan hóa và xây dựng dashboard trên Power BI để hỗ trợ ra quyết định trong quản lý nhân sự.

### Mục tiêu
- Xác định các yếu tố chính dẫn đến nghỉ việc (Attrition).
- Xây dựng dashboard trực quan hóa dữ liệu để dễ dàng phân tích.
- Kết quả: **Mức độ cân bằng công việc - cuộc sống (Work Life Balance = Low)** là yếu tố chính với tỷ lệ nghỉ việc 66.67%.

### Dữ liệu
- **Nguồn**: [Employee-turnover.csv trên Kaggle](https://www.kaggle.com/datasets).
- **Quy mô**: 1,470 dòng, 29 cột (bao gồm Age, Job Involvement, Work Life Balance, Monthly Income, Attrition, v.v.).

## Công nghệ sử dụng
- **Python**: Pandas, NumPy (tiền xử lý dữ liệu).
- **Power BI**: Trực quan hóa và xây dựng dashboard.
- **Jupyter Notebook**: Phân tích dữ liệu ban đầu.
- **VS Code**: Soạn thảo code Python.

## Các bước thực hiện

### 1. Tiền xử lý dữ liệu bằng Python
Sử dụng Python (Pandas, NumPy) để làm sạch và chuẩn hóa dữ liệu:
- **Làm sạch dữ liệu**:
  - Kiểm tra giá trị thiếu (missing values) và thay thế bằng trung bình hoặc mode.
  - Chuẩn hóa định dạng cột (ví dụ: Monthly Income thành số, Attrition thành Yes/No).
- **Tạo cột mới**:
  - `Attrition Binary`: 1 (Yes), 2 (No).
  - `Income Category`: Low (<$3000), Medium ($3000-$7000), High (>$7000).
  - `Age Group`:  Under 30, 30-40,  Over 40.
- **Mã Python mẫu**:
  ```python
  import pandas as pd
  import numpy as np

  # Đọc dữ liệu
  df = pd.read_csv('Employee-turnover.csv')

  # Tạo cột Attrition Binary
  df['Attrition Binary'] = df['Attrition'].map({'Yes': 1, 'No': 2})

  # Tạo cột Income Category
  bins = [0, 3000, 7000, float('inf')]
  labels = ['Low', 'Medium', 'High']
  df['Income Category'] = pd.cut(df['Monthly Income'], bins=bins, labels=labels)

  # Lưu dữ liệu đã xử lý
  df.to_csv('Employee-turnover-processed.csv', index=False)
  ```

### 2. Trực quan hóa dữ liệu và xây dựng dashboard trên Power BI
- **Nhập dữ liệu**: Tải file đã xử lý (`Employee-turnover-processed.csv`) vào Power BI.
- **Tạo measure DAX**:
  - Tính tỷ lệ nghỉ việc theo từng yếu tố:
    ```
    AttritionRateWorkLifeBalance = 
    CALCULATE(
        DIVIDE(
            CALCULATE(COUNTROWS('Employee-turnover'), 'Employee-turnover'[Attrition Binary] = 1),
            CALCULATE(COUNTROWS('Employee-turnover')),
            0
        ),
        ALLEXCEPT('Employee-turnover', 'Employee-turnover'[Work Life Balance])
    ) * 100
    ```
- **Các biểu đồ**:
  - **Stacked Bar Chart**
  - **Stacked Column Chart**
  - **Clustered Bar Chart**
  - **Clustered Column Chart**
  - **Line Chart**
  - **Area Chart**
  - **Line and Stacked Column Chart**
  - **Line and Clustered Column Chart**
  - **Ribbon Chart**
  - **Scatter Chart**
  - **Donut Chart**
  - **Gauge**
  - **Pie Chart**
  - **Treemap**
  - **Funnel Chart**
- **Dashboard**:
  - Trang 1: Phân tích chi tiết theo yếu tố.
  - Trang 2: Phân tích chi tiết theo yếu tố.
  - Trang 3: Phân tích chi tiết theo yếu tố.
  - Trang 4: Tỷ lệ nghỉ việc theo các yếu tố.
  - Trang 5: Tỷ lệ nghỉ việc theo các yếu tố
  - Bộ lọc động (Slicer): Lọc theo Age Group, Department, ...

### 3. Kết quả
- **Yếu tố chính**: Mức độ cân bằng công việc - cuộc sống (Work Life Balance = Low) có tỷ lệ nghỉ việc cao nhất: **66.67%**.
- **Các yếu tố khác**:
  - Over Time (Yes): 45.2%.
  - Job Involvement (Low): 30%.
- **Gợi ý**:
  - Cải thiện Work Life Balance bằng cách giảm giờ làm thêm, tăng hỗ trợ nhân viên.
  - Tăng lương cho nhóm Income Category = Low.

## Hình ảnh minh họa
- **Biểu đồ Stacked Bar (Work Life Balance)**:
  ![Stacked Bar Chart](images/stacked-bar-worklifebalance.png) 
- **Dashboard Tổng quan**:
  ![Dashboard](images/dashboard-overview.png) 

## Cách chạy dự án
1. **Tiền xử lý dữ liệu**:
   - Cài đặt Python và các thư viện: `pip install pandas numpy`.
   - Chạy file `preprocess.ipynb` trong Jupyter Notebook để xử lý dữ liệu.
2. **Trực quan hóa**:
   - Tải file `.pbix` (Power BI) và mở bằng Power BI Desktop.
   - Cập nhật đường dẫn dữ liệu nếu cần.
3. **Xem trên GitHub**:
   - File Python: `/code/preprocess.ipynb`.
   - File Power BI: `/powerbi/employee-turnover-dashboard.pbix`.

## Kết luận
Dự án này cung cấp cái nhìn sâu sắc về tình trạng nghỉ việc của nhân viên, với dashboard trực quan hỗ trợ quản lý nhân sự đưa ra quyết định hiệu quả. Work Life Balance là yếu tố cần ưu tiên cải thiện để giảm tỷ lệ nghỉ việc.

## Tác giả
- **Tên**: [Tên của bạn]
- **Liên hệ**: [Email của bạn]
- **Ngày hoàn thành**: 05/06/2025

## Tài liệu tham khảo
- [Power BI Documentation](https://docs.microsoft.com/en-us/power-bi/)
- [Pandas Documentation](https://pandas.pydata.org/docs/)
