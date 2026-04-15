🎯 คำถาม
เขียน READ TABLE เพื่อหา:
name = 'John' และ age = 30

| id | name  | age |
| -- | ----- | --- |
| 1  | John  | 20  |
| 2  | John  | 30  |
| 3  | Alice | 25  |

READ TABLE lt_users INTO ls_user.
    WITH KEY name = 'John' age = 30.

IF sy-subrc = 0.
    WRITE ls_user-id.
ELSE.
    WRITE 'Not Found'.

# Output
# 2

🧠 Insight สำคัญ

READ TABLE ... WITH KEY
จะคืน [แถวแรกที่ match]

ถ้ามีหลาย record ตรงเงื่อนไข
มันจะหยุดที่ตัวแรกที่เจอ

(ใน STANDARD TABLE คือเรียงตามลำดับที่เก็บ)



# หา John ที่อายุมากที่สุด

DATA lv_max_age TYPE i VALUE 0.
DATA lv_max_id  TYPE i.

# Loop หา max age และ จดจำ id max age ของ 'John'
LOOP AT lt_users INTO ls_user
     WHERE name = 'John'.

  IF ls_user-age > lv_max_age.
    lv_max_age = ls_user-age.
    lv_max_id  = ls_user-id.
  ENDIF.

ENDLOOP.

WRITE lv_max_id.

🎯READ TABLE
เหมาะกับกรณี:
- หา record เฉพาะเจาะจง
- รู้ key ชัดเจน
- ต้องการ 1 record

🎯LOOP AT ... WHERE
เหมาะกับกรณี:
- หา max
- หา min
- หา count
- filter หลาย record
