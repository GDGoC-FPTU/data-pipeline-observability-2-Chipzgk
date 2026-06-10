[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=24112731&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability

**Student Email:** vinhv304@gmail.com
**Name:** Vũ Quang Vinh

---

## Mô tả

Bài lab này yêu cầu xây dựng một **ETL Pipeline tự động** để xử lý dữ liệu sản phẩm:

### Các tác vụ chính:

1. **Extract (Trích xuất):** Đọc dữ liệu từ file JSON (`raw_data.json`)
2. **Validate (Xác thực):** Loại bỏ dữ liệu không hợp lệ:
   - Loại bỏ sản phẩm có giá ≤ 0
   - Loại bỏ sản phẩm không có category
3. **Transform (Chuyển đổi):** Áp dụng business logic:
   - Tính `discounted_price` = price × 0.9 (giảm 10%)
   - Chuyển `category` sang Title Case (VD: "electronics" → "Electronics")
   - Thêm cột `processed_at` với timestamp xử lý
4. **Load (Tải):** Lưu dữ liệu đã xử lý ra file CSV

### Kết quả đạt được:
✅ Pipeline xử lý dữ liệu không lỗi
✅ Validation loại bỏ dữ liệu không hợp lệ
✅ Transform thêm các cột và chuẩn hóa dữ liệu
✅ Load xuất kết quả ra CSV
✅ Agent simulation kiểm tra chất lượng dữ liệu

---

## Cach chay (How to Run)

### Prerequisites
```bash
pip install pandas
```

### Chay ETL Pipeline
```bash
python solution.py
```

### Chạy Agent Simulation (Stress Test)

Agent simulation được sử dụng để kiểm tra chất lượng dữ liệu bằng cách so sánh:
- **Clean Data:** Dữ liệu đã qua xử lý (từ pipeline)
- **Garbage Data:** Dữ liệu chưa được xử lý (để test)

```bash
python agent_simulation.py
```

**Kết quả mong đợi:**
- Agent tìm được sản phẩm electronics từ clean data
- Agent không tìm thấy dữ liệu hợp lệ từ garbage data

---

## Cau truc thu muc

```
├── solution.py              # ETL Pipeline script
├── processed_data.csv       # Output cua pipeline
├── experiment_report.md     # Bao cao thi nghiem
└── README.md                # File nay
```

---

## Kết quả

Sau khi chạy pipeline:

- **Input:** 5 records từ `raw_data.json`
- **Valid Records:** 3 records hợp lệ
- **Invalid Records (Loại bỏ):** 2 records
  - Record ID 3: Price = -10 (âm)
  - Record ID 4: Category rỗng
- **Output:** File `processed_data.csv` với 3 records đã xử lý

### Ví dụ dữ liệu sau xử lý:

| id | product | price | category   | discounted_price | processed_at        |
|----|---------|-------|------------|------------------|---------------------|
| 1  | Laptop  | 1200  | Electronics| 1080.0           | 2026-06-10T...      |
| 2  | Chair   | 45    | Furniture  | 40.5             | 2026-06-10T...      |
| 5  | Monitor | 300   | Electronics| 270.0            | 2026-06-10T...      |
