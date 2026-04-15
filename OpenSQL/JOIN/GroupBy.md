🔥 โจทย์ฝึก (ระดับกลาง+)
🎯 Requirement
ต้องการรายงาน:
- customer_name
- city
- จำนวน order (COUNT)
- ยอดรวม amount (SUM)

เฉพาะ order ที่:
- status = 'O'

และต้องการแสดง:
เฉพาะลูกค้าที่มียอดรวมมากกว่า 5000

# zorders
| order_id | customer_id | amount | status |
| -------- | ----------- | ------ | ------ |
| 1001     | C01         | 5000   | O      |
| 1002     | C01         | 7000   | C      |
| 1003     | C02         | 3000   | O      |
| 1004     | C02         | 2000   | O      |
| 1005     | C03         | 9000   | C      |
| 1006     | C03         | 4000   | O      |
| 1007     | C99         | 8000   | O      |

# zcustomers
| customer_id | customer_name | city       |
| ----------- | ------------- | ---------- |
| C01         | Alice         | Bangkok    |
| C02         | Bob           | Chiang Mai |
| C03         | Charlie       | Bangkok    |
| C04         | David         | Phuket     |

📌 เงื่อนไขสำคัญ
# ต้องใช้ INNER JOIN
ห้าม SELECT *
ต้องใช้ alias แบบ meaningful (เช่น ord, cust)
เก็บลง internal table

TYPES : BEGIN OF ty_result,
        customer_name TYPE zcustomers-customer_name,
        city TYPE zcustomers-city,
        amount_order TYPE i,
        sum_amount TYPE zorders-amount,
        END OF ty_result.

DATA : lt_result TYPE TABLE of ty_result.

Select  cust~customer_name,
        cust~city,
        COUNT(ord~order_id) AS amount_order,
        SUM(ord~amount) AS sum_amount
    FROM zorders AS ord INNER JOIN zcustomers AS cust
    ON ord~customer_id = cust~customer_id
    INTO TABLE lt_result
    Where ord~status = 'O'
    GROUP BY    cust~customer_name,
                cust~city
    HAVING SUM(ord~amount) > 5000.

If lt_result IS NOT INITIAL.
    Write 'Success'.
Else.
    Write 'Fail'.

# ทุก field ที่ไม่ใช่ aggregate ต้องอยู่ใน GROUP BY

# ///////////////////////////////////////////

# zorders
| order_id | customer_id | amount | status |
| -------- | ----------- | ------ | ------ |
| 1001     | C01         | 5000   | O      |
| 1002     | C01         | 7000   | C      |
| 1003     | C02         | 3000   | O      |
| 1004     | C02         | 2000   | O      |
| 1005     | C03         | 9000   | C      |
| 1006     | C03         | 4000   | O      |
| 1007     | C99         | 8000   | O      |
| 1008     | C04         | 1000   | O      |

# zcustomers
| customer_id | customer_name | city       |
| ----------- | ------------- | ---------- |
| C01         | Alice         | Bangkok    |
| C02         | Bob           | Chiang Mai |
| C03         | Charlie       | Bangkok    |
| C04         | David         | Phuket     |

🔥 โจทย์ฝึก
🎯 Requirement
ต้องการรายงาน:
- customer_id
- customer_name
- city
- จำนวน order (COUNT)
- ยอดรวม amount (SUM)

เงื่อนไข:
1️⃣ ต้องแสดงลูกค้าทุกคนที่มี order status = 'O'
2️⃣ แม้ลูกค้าคนนั้นจะไม่มี master data (เช่น C99) ก็ต้องแสดง
3️⃣ แสดงเฉพาะกลุ่มที่มียอดรวม ≥ 4000
4️⃣ เรียงจากยอดรวมมาก → น้อย

📌 เงื่อนไขทางเทคนิค
ต้องใช้ LEFT OUTER JOIN
ต้องใช้ alias แบบ meaningful (ord, cust)
ต้องใช้ WHERE
ต้องใช้ GROUP BY
ต้องใช้ HAVING
ต้องใช้ ORDER BY
เก็บลง internal table

TYPES : BEGIN of ty_result,
        customer_id TYPE zcustomers-customer_id,
        customer_name TYPE zcustomers-customer_name,
        city TYPE zcustomers-city,
        amount_order TYPE i,
        sum_amount TYPE zorders-amount,
        END OF ty_result.

DATA : lt_result TYPE TABLE OF ty_result.

Select  cust~customer_id,
        cust~customer_name,
        cust~city,
        COUNT(ord~order_id) AS amount_order,
        SUM(ord~amount) AS sum_amount
    FROM zorders AS ord LEFT OUTER JOIN zcustomers AS cust
    ON ord~customer_id = cust~customer_id
    INTO TABLE lt_result
    WHERE ord~status = 'O'
    GROUP BY    ord~customer_id,
                cust~customer_name,
                cust~city
    HAVING SUM(ord~amount) >= 4000
    ORDER BY SUM(ord~amount) DESCENDING.

IF lt_result is not initial.
    Write 'Success'.
Else.
    Write 'Fail'.
    