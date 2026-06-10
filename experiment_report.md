# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** 2A202600556
**Name:** Nguyễn Văn Minh
**Date:** 2026-06-10

---

## 1. Ket qua thi nghiem

Chay `agent_simulation.py` voi 2 bo du lieu va ghi lai ket qua:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | Agent: Based on my data, the best choice is Laptop at $1200. | 9 | Kết quả chính xác, Laptop là sản phẩm điện tử có giá cao nhất trong dữ liệu đã được làm sạch |
| Garbage Data (`garbage_data.csv`) | Agent: Based on my data, the best choice is Nuclear Reactor at $999999. | 1 | Kết quả hoàn toàn sai — Nuclear Reactor là outlier vô nghĩa với giá $999,999 |

---

## 2. Phan tich & nhan xet

### Tai sao Agent tra loi sai khi dung Garbage Data?

Khi sử dụng dữ liệu chưa được làm sạch (garbage data), Agent đã trả lời hoàn toàn sai vì nhiều lý do liên quan đến chất lượng dữ liệu. Thứ nhất, dữ liệu chứa Duplicate IDs khiến Agent bị nhiễu loạn khi truy vấn — hai sản phẩm khác nhau (Laptop và Banana) cùng mang id = 1, gây ra xung đột về dữ liệu. Thứ hai, giá trị outlier cực kỳ lớn như Nuclear Reactor có giá $999,999 đã làm lệch toàn bộ kết quả, vì Agent đơn giản chỉ tìm sản phẩm có giá cao nhất trong danh mục electronics mà không có cơ chế lọc bất thường. Thứ ba, dữ liệu chứa giá trị sai kiểu (wrong data types) như "ten dollars" thay vì số, khiến các phép tính trên cột price có thể gây lỗi hoặc bị bỏ qua. Thứ tư, các giá trị null (None) ở trường id và category làm cho việc phân loại và truy vấn trở nên không đáng tin cậy. Tất cả những vấn đề này chứng minh rằng nếu không có bước Validate trong pipeline ETL, dữ liệu "độc hại" sẽ đi thẳng vào hệ thống và làm cho Agent đưa ra những câu trả lời vô nghĩa.

---

## 3. Ket luan

**Quality Data > Quality Prompt?** Đồng ý hoàn toàn. Dù cho prompt có được thiết kế tốt đến đâu, nếu dữ liệu đầu vào bị "nhiễm độc" (duplicates, outliers, null values, wrong types) thì Agent vẫn sẽ đưa ra câu trả lời sai. Như thí nghiệm đã chứng minh, cùng một câu hỏi nhưng dữ liệu sạch cho kết quả chính xác (Laptop $1200) còn dữ liệu rác cho kết quả vô lý (Nuclear Reactor $999,999). Việc xây dựng một pipeline ETL với bước Validation chặt chẽ là bước bắt buộc trước khi đưa dữ liệu vào bất kỳ hệ thống AI nào. Đây chính là nguyên tắc "Garbage In, Garbage Out" — chất lượng dữ liệu quyết định chất lượng của AI.
