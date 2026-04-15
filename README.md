[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=23574010&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability

**Student Email:** nyclone569@gmail.com
**Name:** Trương Đăng Nghĩa

---

## Mo ta

Bài lab này xây dựng một ETL Pipeline tự động để xử lý dữ liệu sản phẩm từ file JSON. Pipeline thực hiện:
- **Extract**: Đọc dữ liệu từ raw_data.json
- **Validate**: Kiểm tra và loại bỏ records không hợp lệ (giá <= 0, category rỗng)
- **Transform**: Chuẩn hóa category sang Title Case, tính giá giảm 10%, thêm timestamp
- **Load**: Lưu kết quả vào processed_data.csv

Ngoài ra, bài lab còn thực hiện stress test để so sánh hiệu suất của AI Agent khi sử dụng clean data vs garbage data, chứng minh tầm quan trọng của Data Quality.

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

### Chay Agent Simulation (Stress Test)
```bash
# Tao garbage data
python generate_garbage.py

# Chay thi nghiem so sanh Clean vs Garbage data
python agent_simulation.py
```

---

## Cau truc thu muc

```
├── solution.py              # ETL Pipeline script
├── processed_data.csv       # Output cua pipeline
├── experiment_report.md     # Bao cao thi nghiem
└── README.md                # File nay
```

---

## Ket qua

**ETL Pipeline Results:**
- Total records extracted: 5
- Valid records processed: 3
- Invalid records dropped: 2
  - Record ID 3: Price <= 0 (Mystery Box: -$10)
  - Record ID 4: Missing Category (Phone)
- Output file: processed_data.csv với 3 records đã được transform

**Agent Simulation Results:**
- Clean Data: Agent đưa ra khuyến nghị chính xác (Laptop $1200) - Accuracy: 10/10
- Garbage Data: Agent đưa ra khuyến nghị sai lệch (Nuclear Reactor $999,999) - Accuracy: 1/10

**Key Findings:** Data Quality có tác động trực tiếp đến độ chính xác của AI Agent. Validation là bước quan trọng nhất trong ETL Pipeline.
