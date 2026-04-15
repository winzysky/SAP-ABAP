TYPES: BEGIN OF ty_data,
         value TYPE i,
       END OF ty_data.

DATA: lt_data TYPE TABLE OF ty_data,
      ls_data TYPE ty_data.

ls_data-value = 5.
APPEND ls_data TO lt_data.

ls_data-value = 10.
APPEND ls_data TO lt_data.

# output
# 5
# 10

# #################################

# INTO
LOOP AT lt_data INTO ls_data.
  ls_data-value = ls_data-value + 1.
ENDLOOP.

LOOP AT lt_data INTO ls_data.
  WRITE: / ls_data-value.
ENDLOOP.

# Output
# 5
# 10

# #################################

# ASSIGNING

FIELDS-SYMBOLS : <fs-data> TYPE ty_data.

LOOP AT lt_data ASSIGNING <fs-data>.
    <fs-data>-value = <fs-data>-value + 1.
ENDLOOP.

LOOP AT lt_data INTO ls-data.
    WRITE : / ls_data-value.
ENDLOOP.

# Output
# 6
# 11

| คำสั่ง    | ทำงานแบบ  | แก้ table ได้ไหม |
| --------- | --------- | ---------------- |
| INTO      | Copy      | ❌ ไม่ได้         |
| ASSIGNING | Reference | ✅ ได้            |

# ในงานจริง performance สำคัญ → ใช้ ASSIGNING บ่อยมาก

# แต่ต้องรู้ “กับดัก” นิดนึง ⚠️
หลัง loop:
<fs> ยังชี้ row เดิม
ถ้าไม่ระวัง → แก้ข้อมูลโดยไม่ตั้งใจ

🧠 ทางที่ดี:
UNASSIGN <fs>.


