🚀 วิธีโปร: SORT ก่อน แล้ว READ

| id | name  | age |
| -- | ----- | --- |
| 1  | John  | 20  |
| 2  | John  | 30  |
| 3  | Alice | 25  |

DATA lt_john TYPE TABLE OF ty_user.

# เอาเฉพาะ John มาใส่ table ใหม่
LOOP AT lt_users INTO ls_user WHERE name = 'John'.
  APPEND ls_user TO lt_john.
ENDLOOP.

| id | name  | age |
| -- | ----- | --- |
| 1  | John  | 20  |
| 2  | John  | 30  |

# เรียงจากอายุมากไปน้อย
SORT lt_john BY age DESCENDING.

| id | name  | age |
| -- | ----- | --- |
| 2  | John  | 30  |
| 1  | John  | 20  |

# อ่านแถวแรก
READ TABLE lt_john INTO ls_user INDEX 1.

IF sy-subrc = 0.
  WRITE ls_user-id.
ENDIF.

# Output
# 2
