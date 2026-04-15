TYPES: BEGIN OF ty_result,
         order_id      TYPE zorders-order_id,
         customer_name TYPE zcustomers-customer_name,
         amount        TYPE zorders-amount,
       END OF ty_result.

DATA: lt_result TYPE TABLE OF ty_result.

SELECT a~order_id,
       b~customer_name,
       a~amount
  FROM zorders AS a
  INNER JOIN zcustomers AS b
    ON a~customer_id = b~customer_id
  INTO TABLE lt_result
  WHERE a~status = 'O'.

# zorders
| order_id | customer_id | amount | status |

# zcustomers
| customer_id | customer_name | city |


🟦 ข้อที่ 1 — INNER JOIN (ห้ามใช้ alias)
🎯 Requirement
ดึงข้อมูล:
- order_id
- customer_name
- amount
- city

เงื่อนไข:
- status = 'O'
- ลูกค้าอยู่ที่เมือง 'Bangkok'
- ต้องเขียนแบบ zorders~field
- ต้องสร้าง TYPE ใหม่ให้ตรงกับผลลัพธ์
- เก็บลง internal table lt_result

TYPES : BEGIN OF ty_result,
        order_id TYPE zorders-order_id,
        customer_name TYPE zcustomers-customer_name,
        amount TYPE zorders-amount,
        city TYPE zcustomers-city,
        END OF ty_result.

DATA : lt_result TYPE TABLE OF ty_result.

Select zorders~order_id zcustomers~customer_name zorders~amount zcustomers~city
        From zorders INNER JOIN zcustomers ON zorders~customer_id = zcustomers~customer_id
        INTO TABLE lt_result
        WHERE zorders~status = 'O'
            AND zcustomers~city = 'Bangkok'.

if sy-subrc = 0.
    Write 'Success'.
else.
    Write 'Fail'.