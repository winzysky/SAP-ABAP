# zorders
| order_id | customer_id | amount | status |

# zcustomers
| customer_id | customer_name | city |


🟩 ข้อที่ 2 — LEFT OUTER JOIN (ใช้ alias)
🎯 Requirement
ดึงข้อมูล:
- order_id
- customer_id
- customer_name
- amount

ต้องการ:
แสดง order ทุก record แม้ไม่มี customer match

📌 เงื่อนไข
- ต้องใช้ LEFT OUTER JOIN
- ต้องใช้ alias (ตั้งชื่อ meaningful ห้ามใช้ a,b)
- ห้าม SELECT *
- เก็บลง internal table
- ต้องสร้าง TYPE ใหม่

TYPES : BEGIN OF ty_result,
        order_id TYPE zorders-order_id,
        customer_id TYPE zorders-customer_id,
        customer_name TYPE zcustomers-customer_name,
        amount TYPE zorders-amount,
        END OF ty_result.

DATA : lt_result TYPE TABLE OF ty_result.

Select  ord~order_id,
        ord~customer_id,
        cust~customer_name,
        ord~amount
    FROM zorders AS ord LEFT OUTER JOIN
         zcustomers AS cust
    ON ord~customer_id = cust~customer_id
    INTO TABLE lt_result.

IF lt_result IS NOT INITIAL.
    Write 'Success'.
Else.
    Write 'Fail'.
    
