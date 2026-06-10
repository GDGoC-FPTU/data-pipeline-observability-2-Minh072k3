[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=24112838&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability

**Student Email:** nguyenvanminh07012003@gmail.com
**Name:** Nguyễn Văn Minh

---

## Mô tả

Bài lab này xây dựng một ETL Pipeline tự động để xử lý dữ liệu sản phẩm từ file JSON. Pipeline gồm 4 bước: Extract (đọc dữ liệu), Validate (loại bỏ record có giá âm/bằng 0 hoặc category rỗng), Transform (tính giá giảm 10%, chuẩn hóa category thành Title Case, thêm timestamp), và Load (xuất ra file CSV). Ngoài ra, tôi đã thực hiện Stress Test bằng cách chạy Agent Simulation với dữ liệu sạch và dữ liệu "rác" để chứng minh tầm quan trọng của Data Quality đối với AI Agent.

---

## Cach chay (How to Run)

### Prerequisites
```bash
pip install pandas pytest
```

### Chay ETL Pipeline
```bash
python solution.py
```
Kiem tra file `processed_data.csv` duoc tao ra sau khi chay.

### Chay Agent Simulation (Stress Test)
```bash
python generate_garbage.py
python agent_simulation.py
```

### Chay Tests
```bash
pytest tests/test_autograder.py -v
```

---

## Cau truc thu muc

```
├── solution.py              # ETL Pipeline script
├── processed_data.csv       # Output cua pipeline (3 records hop le)
├── experiment_report.md     # Bao cao thi nghiem Clean vs Garbage data
├── agent_simulation.py      # Script mo phong Agent (Stress Test)
├── generate_garbage.py      # Script tao du lieu "rac"
├── raw_data.json            # Du lieu dau vao (5 records)
└── README.md                # File nay
```

---

## Ket qua

- **Tong so records dau vao:** 5
- **Records hop le (sau Validation):** 3 (Laptop, Chair, Monitor)
- **Records bi loai:** 2 (Mystery Box — gia am; Phone — category rong)
- **Stress Test:** Agent tra loi chinh xac voi du lieu sach (Laptop $1200), nhung tra loi sai hoan toan voi du lieu rac (Nuclear Reactor $999,999).
