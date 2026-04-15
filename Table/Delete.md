🧨 DELETE — ลบข้อมูลใน Internal Table

| id | age |
| -- | --- |
| 1  | 20  |
| 2  | 30  |
| 3  | 40  |

# ลบคนที่ age > 30

DELETE lt_users WHERE age > 30.

✅ ผลลัพธ์

| id | age |
| -- | --- |
| 1  | 20  |
| 2  | 30  |

# DELETE ด้วย INDEX

DELETE lt_users INDEX 2.

⚠️ ใช้กับ STANDARD / SORTED เท่านั้น, HASHED ใช้ไม่ได้

# DELETE หลัง READ

READ TABLE lt_users INTO ls_user
     WITH KEY id = 2.

IF sy-subrc = 0.
  DELETE lt_users INDEX sy-tabix.
ENDIF.

`ถ้าลบตามเงื่อนไขธรรมดา → ใช้ DELETE ... WHERE เสมอ`

🎯 โจทย์สั้น ๆ

| id | age |
| -- | --- |
| 1  | 20  |
| 2  | 35  |
| 3  | 28  |
| 4  | 40  |

เขียนคำสั่งลบคนที่ age >= 35

DELETE lt_users WHERE age >= 35.

# 🧠 Insight เพิ่มอีกนิด (ระดับโปร)
# หลัง DELETE คุณสามารถเช็คได้ว่าลบไปกี่แถวด้วย:

DATA lv_deleted TYPE i.

DELETE lt_users WHERE age >= 35.
lv_deleted = sy-dbcnt.

# sy-dbcnt = จำนวน row ที่ถูกกระทบ (affected rows)
# ใช้ได้กับ DELETE / MODIFY / SELECT บางกรณี

