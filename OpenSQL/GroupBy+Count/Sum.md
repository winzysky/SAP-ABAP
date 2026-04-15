🟢 ตัวอย่าง Table: zorders

| order_id | customer_id | amount | status |
| -------- | ----------- | ------ | ------ |
| 1001     | C01         | 5000   | O      |
| 1002     | C01         | 7000   | C      |
| 1003     | C02         | 3000   | O      |
| 1004     | C02         | 2000   | O      |
| 1005     | C03         | 9000   | C      |

# 🎯 ต้องการ: นับจำนวน order แยกตาม status
DATA: lt_result TYPE TABLE OF zorders.

SELECT status COUNT( * ) AS total_count
  FROM zorders
  INTO TABLE lt_result
  GROUP BY status.

| status | total_count |
| ------ | ----------- |
| O      | 3           |
| C      | 2           |

# 🎯 ต้องการ: หาผลรวม amount แยกตาม customer

DATA: lt_result TYPE TABLE OF zorders.

SELECT customer_id SUM( amount ) AS total_amount
  FROM zorders
  INTO TABLE lt_result
  GROUP BY customer_id.

| customer_id | total_amount |
| ----------- | ------------ |
| C01         | 12000        |
| C02         | 5000         |
| C03         | 9000         |

# Practice 1
ดึงข้อมูล:
- status
- จำนวน order (COUNT)
- ผลรวม amount (SUM)
- แยกตาม status

เงื่อนไข:
- ต้องใช้ GROUP BY
- ห้ามใช้ SELECT *
- เก็บลง internal table
- ใช้ AS ตั้งชื่อ field

TYPES: BEGIN OF ty_result,
         status        TYPE zorders-status,
         total_order   TYPE i,
         total_amount  TYPE zorders-amount,
       END OF ty_result.

DATA : lt_result TYPE Table of ty_result.

Select status Count(order_id) AS total_order Sum(amount) AS total_amount FROM zorders
        into TABLE lt_result GROUP BY status.

# Practice 2

| order_id | customer_id | amount | status |
| -------- | ----------- | ------ | ------ |
| 1001     | C01         | 5000   | O      |
| 1002     | C01         | 7000   | C      |
| 1003     | C02         | 3000   | O      |
| 1004     | C02         | 2000   | O      |
| 1005     | C03         | 9000   | C      |
| 1006     | C03         | 4000   | O      |

🔥 โจทย์

ต้องการรายงาน:
- customer_id
- จำนวน order ของลูกค้าแต่ละคน (COUNT)
- ยอดรวม amount ของลูกค้าแต่ละคน (SUM)

📌 เงื่อนไข
- ต้องใช้ GROUP BY
- ต้องใช้ COUNT
- ต้องใช้ SUM
- ห้ามใช้ SELECT *
- ต้องสร้าง TYPE ใหม่ให้ตรงกับผลลัพธ์
- เก็บลง internal table lt_result

Types : BEGIN OF ty_result,
        customer_id TYPE zorders-customer_id,
        total_order TYPE i,
        total_amount TYPE zorders-amount,
        END OF ty_result.

DATA : lt_result TYPE TABLE OF ty_result.

Select customer_id COUNT(order_id) AS total_order SUM(amount) AS total_amount 
                    FROM zorders INTO TABLE lt_result
                    GROUP BY customer_id.

# Practice (SUM + GROUP BY + ORDER BY + UP TO 1 ROWS)

🎯 Requirement
หาลูกค้าที่มียอดรวม amount สูงที่สุด
ผลลัพธ์ต้องมี:
- customer_id
- total_amount (SUM)

📌 เงื่อนไข
- ต้องใช้ GROUP BY
- ต้องใช้ SUM
- ต้องใช้ ORDER BY
- ต้องใช้ UP TO 1 ROWS
- ห้ามใช้ MAX()
- เก็บลง work area ls_result
- เช็ค sy-subrc
- ห้ามใช้ SELECT *

🎯 โครงสร้างที่ต้องสร้างก่อน
ต้องมี TYPE ใหม่ เพราะผลลัพธ์ไม่ใช่ zorders ตรง ๆ

Types : BEGIN OF ty_result,
        customer_id TYPE zorders-customer_id,
        total_amount TYPE zorders-amount,
        END OF ty_result.

DATA : ls_result TYPE ty_result.

Select customer_id SUM(amount) AS total_amount From zorders INTO ls_result
                                              GROUP BY customer_id
                                              ORDER BY SUM(amount) DESCENDING
                                              
                                              Up to 1 rows
Endselect.

if sy-subrc = 0.
  WRITE 'Success'.
else.
  WRITE 'Fail'.