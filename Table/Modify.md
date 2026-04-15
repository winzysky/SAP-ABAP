🔥 MODIFY — แก้ข้อมูลใน Internal Table อย่างถูกต้อง

# 1 MODIFY หลังใช้ INTO

| id | age |
| -- | --- |
| 1  | 20  |
| 2  | 30  |

LOOP AT lt_users INTO ls_user.

  IF ls_user-id = 1.
    ls_user-age = 99.
    MODIFY lt_users FROM ls_user.
  ENDIF.

ENDLOOP.

# 2 ใช้ ASSIGNING (ไม่ต้อง MODIFY)

FIELD-SYMBOLS <fs_user> TYPE ty_user.

LOOP AT lt_users ASSIGNING <fs_user>.

  IF <fs_user>-id = 1.
    <fs_user>-age = 99.
  ENDIF.

ENDLOOP.

🎯 สรุปสั้นๆ
| วิธี                 | ต้อง MODIFY ไหม |
| ------------------ | --------------- |
| LOOP ... INTO      | ✅ ต้อง          |
| LOOP ... ASSIGNING | ❌ ไม่ต้อง       |


# 3 🔥(สำคัญในงานจริง)

READ TABLE lt_users INTO ls_user
     WITH KEY id = 1.

IF sy-subrc = 0.
  ls_user-age = 99.
  MODIFY lt_users FROM ls_user INDEX sy-tabix.
ENDIF.

# sy-tabix = index ของ row ล่าสุดที่เจอ


# Practice
| id | age |
| -- | --- |
| 1  | 20  |
| 2  | 30  |
| 3  | 40  |

id = 2 ให้ age = 35
โดยใช้ ASSIGNING

FIELD-SYMBOLS <fs_user> TYPE ty_user.

LOOP AT lt_users ASSIGNING <fs_user>.
    IF <fs_user>-id = 2.
        <fs_user>-age = 35.
    ENDIF.
ENDLOOP.
        




