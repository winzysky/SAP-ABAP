| WHERE             | HAVING              |
| ----------------- | ------------------- |
| กรองก่อน GROUP     |      กรองหลัง GROUP  |
| ใช้กับ field ปกติ    |     ใช้กับ aggregate  |
| เร็วกว่า             |   ใช้กับ report logic |

🟢 ตัวอย่าง Table: zorders
| order_id | customer_id | amount | status |
| -------- | ----------- | ------ | ------ |
| 1001     | C01         | 5000   | O      |
| 1002     | C01         | 7000   | C      |
| 1003     | C02         | 3000   | O      |
| 1004     | C02         | 2000   | O      |
| 1005     | C03         | 9000   | C      |

# Example
TYPES: BEGIN OF ty_result,
         customer_id  TYPE zorders-customer_id,
         total_amount TYPE zorders-amount,
       END OF ty_result.

DATA: lt_result TYPE TABLE OF ty_result.

SELECT customer_id,
       SUM( amount ) AS total_amount
  FROM zorders
  INTO TABLE lt_result
  GROUP BY customer_id
  HAVING SUM( amount ) > 8000.
# Having หลัง GROUP BY

🎯 โจทย์ให้ลอง
ดึงข้อมูล:
- status
- จำนวน order (COUNT)
- ผลรวม amount (SUM)

แต่เอาเฉพาะ status ที่:
- มีจำนวน order มากกว่า 2

เงื่อนไข:
- ต้องใช้ GROUP BY
- ต้องใช้ COUNT
- ต้องใช้ HAVING
- ห้ามใช้ SELECT *
- เก็บลง internal table

TYPES : BEGIN OF ty_result,
        status TYPE zorders-status,
        order_amount TYPE i,
        sum_amount TYPE zorders-amount,
        END OF ty_result.

DATA : lt_result TYPE TABLE of ty_result.

Select status COUNT(order_id) AS order_amount SUM(amount) AS sum_amount
        FROM zorders
        INTO TABLE lt_result
        GROUP BY status
        HAVING COUNT(order_id) > 2.

if sy-subrc = 0.
    WRITE 'Success'.
else.
    WRITE 'Fail'.