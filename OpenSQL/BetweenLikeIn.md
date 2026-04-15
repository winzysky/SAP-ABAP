# BETWEEN
SELECT order_id amount from zorders INTO TABLE lt_orders WHERE amount BETWEEN 3000 AND 7000.
# amount ระหว่าง 3000 - 7000

# LIKE
SELECT * FROM zusers INTO TABLE lt_users WHERE name LIKE 'j%'.
# หา name ที่ j นำหน้า
`ใช้ % แทนหลายตัวอักษร`
`ใช้ _ แทน 1 ตัวอักษร`

# IN
SELECT * FROM zorders INTO TABLE lt_orders WHERE status IN ('O', 'C').
# Select status ที่ มี O หรือ C

# Practice
| order_id | customer_id | amount | status |
| -------- | ----------- | ------ | ------ |
| 1001     | C01         | 5000   | O      |
| 1002     | C02         | 7000   | C      |
| 1003     | C01         | 3000   | O      |
| 1004     | C03         | 12000  | O      |
| 1005     | C04         | 4500   | C      |



🟢 ข้อ 1 — BETWEEN
DATA : lt_orders TYPE TABLE OF zorders.

Select order_id amount from zorders into table lt_orders Where amount between 3000 AND 8000.

if sy-subrc = 0.
    write 'Success'.
else.
    write 'Fail'.

🟢 ข้อ 2 — LIKE
DATA : lt_users TYPE TABLE OF zusers.

Select id name from zusers into table lt_users Where name LIKE 'A%'.

if sy-subrc = 0.
    write 'Success'.
else.
    write 'Fail'.

🟢 ข้อ 3 — IN
DATA : lt_orders TYPE TABLE OF zorders.

Select order_id status from zorders into table lt_orders Where status IN ('O','C').

if sy-subrc = 0.
    write 'Success'.
else.
    write 'Fail'.

# Combine
# ข้อ 4 — รวม BETWEEN + LIKE + IN

| order_id | customer_id | amount | status |
| -------- | ----------- | ------ | ------ |
| 1001     | C01         | 5000   | O      |
| 1002     | C02         | 7000   | C      |
| 1003     | C01         | 3000   | O      |
| 1004     | B01         | 12000  | O      |
| 1005     | C03         | 4500   | X      |
| 1006     | C04         | 9000   | C      |

🎯 Requirement
ดึง order ที่มีเงื่อนไขทั้งหมดนี้:
- amount อยู่ระหว่าง 3000 ถึง 10000
- status เป็น 'O' หรือ 'C'
- customer_id ขึ้นต้นด้วยตัวอักษร 'C'

เลือกเฉพาะ field:
- order_id
- customer_id
- amount

DATA : lt_orders TYPE TABLE OF zorders.

Select order_id customer_id amount From zorders Into Table lt_orders Where amount Between 3000 AND 10000
                                                                    AND status IN ('O','C')
                                                                    AND customer_id LIKE 'C%'.
IF lt_orders IS NOT INITIAL.
    WRITE 'Success'.
ELSE.
    WRITE 'Fail'.
ENDIF.

