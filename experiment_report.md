# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** nyclone569@gmail.com
**Name:** Trương Đăng Nghĩa
**Date:** 2026-04-15

---

## 1. Ket qua thi nghiem

Chay `agent_simulation.py` voi 2 bo du lieu va ghi lai ket qua:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | Based on my data, the best choice is Laptop at $1200. | 10 | Correct recommendation based on validated data |
| Garbage Data (`garbage_data.csv`) | Based on my data, the best choice is Nuclear Reactor at $999999. | 1 | Completely wrong due to extreme outlier and data quality issues |

---

## 2. Phan tich & nhan xet

### Tai sao Agent tra loi sai khi dung Garbage Data?

Khi Agent sử dụng garbage_data.csv, nó đưa ra khuyến nghị hoàn toàn sai lệch vì nhiều vấn đề về chất lượng dữ liệu:

1. **Duplicate IDs**: Có 2 records với id=1 (Laptop và Banana), gây nhầm lẫn trong việc xác định sản phẩm duy nhất.

2. **Wrong Data Types**: Giá của "Broken Chair" là chuỗi "ten dollars" thay vì số, khiến việc so sánh giá không chính xác.

3. **Extreme Outliers**: "Nuclear Reactor" có giá $999,999 - một giá trị cực đoan không hợp lý cho sản phẩm điện tử thông thường. Agent chọn sản phẩm này vì nó có giá cao nhất, nhưng đây rõ ràng không phải là khuyến nghị hợp lý.

4. **Null Values**: Record với id=None và category=None làm giảm độ tin cậy của toàn bộ dataset.

5. **Lack of Validation**: Không có bước validation nào để loại bỏ các giá trị bất thường này trước khi Agent sử dụng, dẫn đến quyết định sai lầm.

Kết quả là Agent đưa ra khuyến nghị "Nuclear Reactor" - một sản phẩm không thực tế, thay vì "Laptop" như trong clean data. Điều này chứng minh rằng chất lượng dữ liệu ảnh hưởng trực tiếp đến độ chính xác của AI Agent.

---

## 3. Ket luan

**Quality Data > Quality Prompt?** (Dong y hay khong? Giai thich ngan gon.)

Hoàn toàn đồng ý. Một prompt tốt không thể bù đắp cho dữ liệu kém chất lượng. Trong thí nghiệm này, cả hai trường hợp đều sử dụng cùng một prompt ("What is the best electronic product?"), nhưng kết quả hoàn toàn khác biệt:

- **Clean Data**: Agent đưa ra khuyến nghị chính xác (Laptop $1200)
- **Garbage Data**: Agent đưa ra khuyến nghị sai lầm (Nuclear Reactor $999,999)

Điều này chứng minh rằng: **"Garbage In, Garbage Out"**. Dù prompt có được thiết kế tốt đến đâu, nếu dữ liệu đầu vào chứa lỗi, outliers, hoặc giá trị không hợp lệ, Agent sẽ đưa ra kết quả sai lệch. 

Vì vậy, Data Validation và Data Quality là nền tảng quan trọng nhất cho bất kỳ hệ thống AI nào. ETL Pipeline với các bước validation nghiêm ngặt là điều cần thiết để đảm bảo Agent hoạt động chính xác.
