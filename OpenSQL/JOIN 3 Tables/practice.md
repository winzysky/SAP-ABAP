1️⃣ zorders
| order_id | customer_id | product_id | amount | status |
| -------- | ----------- | ---------- | ------ | ------ |
| 1001     | C01         | P01        | 5000   | O      |
| 1002     | C01         | P02        | 7000   | C      |
| 1003     | C02         | P01        | 3000   | O      |
| 1004     | C02         | P03        | 2000   | O      |
| 1005     | C03         | P02        | 9000   | C      |
| 1006     | C03         | P01        | 4000   | O      |
| 1007     | C99         | P04        | 8000   | O      |

2️⃣ zcustomers
| customer_id | customer_name | city       |
| ----------- | ------------- | ---------- |
| C01         | Alice         | Bangkok    |
| C02         | Bob           | Chiang Mai |
| C03         | Charlie       | Bangkok    |
| C04         | David         | Phuket     |

3️⃣ zproducts
| product_id | product_name | category  |
| ---------- | ------------ | --------- |
| P01        | Laptop       | IT        |
| P02        | Phone        | IT        |
| P03        | Desk         | Furniture |
| P04        | Chair        | Furniture |

🎯 โจทย์ฝึก (ระดับจริง)
ต้องการรายงาน:
customer_name
city
product_name
category
จำนวน order (COUNT)
ยอดรวม amount (SUM)

เงื่อนไข:
1️⃣ เอาเฉพาะ order ที่ status = 'O'
2️⃣ แสดงเฉพาะ category = 'IT'
3️⃣ แสดงเฉพาะกลุ่มที่ยอดรวม ≥ 4000
4️⃣ เรียงจากยอดรวมมาก → น้อย

TYPES : BEGIN OF ty_result,
        customer_name TYPE zcustomers-customer_name,
        city TYPE zcustomers-city,
        product_name TYPE zproducts-product_name,
        category TYPE zproducts-category,
        amount_order TYPE i,
        total_amount TYPE zorders-amount,
        END OF ty_result.

DATA : lt_result TYPE TABLE of ty_result.

Select  cust~customer_name,
        cust~city,
        prod~product_name,
        prod~category,
        COUNT(ord~order_id) AS amount_order,
        SUM(ord~amount) AS total_amount
        FROM zorders AS ord 
        INNER JOIN zcustomers AS cust 
            ON ord~customer_id = cust~customer_id
        INNER JOIN zproducts AS prod 
            ON ord~product_id = prod~product_id
        INTO TABLE lt_result
        WHERE ord~status = 'O' AND prod~category = 'IT'
        GROUP BY 
        cust~customer_name,
        cust~city,
        prod~product_name,
        prod~category
        HAVING SUM(ord~amount) >= 4000
        ORDER BY SUM(ord~amount) DESCENDING.

If lt_result is not INITIAL.
    WRITE 'Success'.
Else.
    WRITE 'Fail'.




