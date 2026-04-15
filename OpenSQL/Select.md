🟢 โจทย์ที่ 1 — SELECT INTO TABLE
# Database Table: zusers
| id | name | age | status |
| -- | ---- | --- | ------ |
| 1  | A    | 25  | A      |
| 2  | B    | 40  | A      |
| 3  | C    | 38  | I      |
| 4  | D    | 45  | A      |

🎯 Requirement
ดึงข้อมูลผู้ใช้ที่:
อายุ ≥ 35
status = 'A'
เก็บลง internal table lt_users

เลือกเฉพาะ field:
id
name
age

DATA: lt_users TYPE TABLE OF zusers.

SELECT id name age FROM zusers INTO TABLE lt_users WHERE age >= 35 AND status = 'A'.

IF sy-subrc = 0.
    WRITE 'Done'.
ELSE.
    WRITE 'Fail'.

# /////////////////////////////////////////

🟢 โจทย์ที่ 2 — SELECT INTO wa

# Database Table: zusers
| id | name | age | status |
| -- | ---- | --- | ------ |
| 1  | A    | 25  | A      |
| 2  | B    | 40  | A      |
| 3  | C    | 38  | I      |
| 4  | D    | 45  | A      |

ดึงข้อมูลของ user ที่มี:
id = 2
เก็บลง work area ls_user

ถ้าเจอ → WRITE name
ถ้าไม่เจอ → WRITE 'Not Found'

# ls_user ก็คือ work area
DATA : ls_users TYPE zusers.

SELECT * FROM zusers INTO ls_users WHERE id = 2.
ENDSELECT.

IF sy-subrc = 0.
    WRITE ls_users-name.
ELSE.
    WRITE 'Not Found'.

# or Select Single
# Database จะหา record แรกที่ match เงื่อนไข

🟢 โจทย์: SELECT SINGLE
# Database Table: zorders

| order_id | customer_id | amount | status |
| -------- | ----------- | ------ | ------ |
| 1001     | C01         | 5000   | O      |
| 1002     | C02         | 7000   | C      |
| 1003     | C01         | 3000   | O      |

🎯 Requirement
order_id = 1002
เก็บลง work area ls_order

เลือกเฉพาะ field:
- order_id
- amount
- status

ถ้าเจอ → WRITE amount
ถ้าไม่เจอ → WRITE 'Order Not Found'

Data : ls_order type zorders.

SELECT SINGLE order_id amount status FROM zorders INTO ls_order WHERE order_id = 1002.

if sy-subrc = 0.
    write ls_order-amount.
else.
    write 'Order Not Found'.

