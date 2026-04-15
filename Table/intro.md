DATA: lt_data TYPE TABLE OF ty_data,
      ls_data TYPE ty_data.

READ TABLE lt_data INTO ls_data
     WITH KEY value = 10.
# find row ที่ col (value) that equals 10

IF sy-subrc = 0.
  WRITE 'Found'.
ELSE.
  WRITE 'Not Found'.
ENDIF.

# sy-subrc
| ค่า | ความหมาย |
| --- | -------- |
| 0   | เจอ      |
| 4   | ไม่เจอ   |

# นี่คือ pattern ที่ใช้ทั้งระบบ SAP

# Internal Table:
# ไม่มี primary key อัตโนมัติ
# ทุกอย่างขึ้นกับ structure ที่คุณ define เอง

# ถ้ามีหลาย field ก็ใส่หลาย key ได้
READ TABLE lt_data INTO ls_data
     WITH KEY id = 2
              value = 10.

READ TABLE lt_data INTO ls_data.
    WITH KEY name = "John".

# ห้ามลืมเช็ค sy-subrc เด็ดขาด นี่คือมาตรฐาน SAP

////////////////////////////////

TYPES: BEGIN OF ty_user,
         id   TYPE i,
         name TYPE string,
         age  TYPE i,
       END OF ty_user.

DATA: lt_users TYPE TABLE OF ty_user,
      ls_user  TYPE ty_user.

ls_user-id = 1.
ls_user-name = 'John'.
ls_user-age = 20.
APPEND ls_user TO lt_users.

ls_user-id = 2.
ls_user-name = 'John'.
ls_user-age = 30.
APPEND ls_user TO lt_users.

ls_user-id = 3.
ls_user-name = 'Alice'.
ls_user-age = 25.
APPEND ls_user TO lt_users.

| id | name  | age |
| -- | ----- | --- |
| 1  | John  | 20  |
| 2  | John  | 30  |
| 3  | Alice | 25  |

1️⃣ sy-subrc
# Return Code ของคำสั่งล่าสุด
❗ ห้ามใช้กับ LOOP เพื่อเช็คเงื่อนไขภายใน : เพราะ LOOP สำเร็จ = sy-subrc = 0

2️⃣ sy-tabix
#  Index ของ row ปัจจุบันใน Internal Table
such as :
MODIFY lt_users INDEX sy-tabix.
DELETE lt_users INDEX sy-tabix.
❗ ใช้ไม่ได้กับ HASHED TABLE
เพราะ hashed ไม่มีลำดับ

3️⃣ sy-dbcnt
# จำนวน record ที่ถูกกระทบโดยคำสั่งล่าสุด

DELETE lt_users WHERE age >= 35.

WRITE sy-dbcnt.

# ถ้าลบ 2 แถว → sy-dbcnt = 2


🧠 เปรียบเทียบแบบชีวิตจริง

sy-subrc = งานผ่านไหม

sy-tabix = ตอนนี้ยืนอยู่ลำดับที่เท่าไหร่

sy-dbcnt = ทำงานไปกี่ชิ้นแล้ว


# ลำดับหลังจากนี้
1️⃣ READ TABLE
2️⃣ MODIFY
3️⃣ DELETE
4️⃣ SORT
5️⃣ แล้วค่อยไป SELECT