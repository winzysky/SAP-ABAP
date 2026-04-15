DATA lv_num TYPE i VALUE 10.

DO 3 TIMES.
  lv_num = lv_num + 1.
ENDDO.

WRITE lv_num.

# 13

# ############################################

DATA lv_num TYPE i VALUE 10.

DO 3 TIMES.
  lv_num = lv_num + sy-index.
ENDDO.

WRITE lv_num.

#  16

# ############################################

DATA lv_total TYPE i VALUE 0.

DO 4 TIMES.
# MOD คือ %
  IF sy-index MOD 2 = 0.
    lv_total = lv_total + sy-index.
  ENDIF.
ENDDO.

WRITE lv_total.

# 6

# ############################################

DATA lv_a TYPE i VALUE 5.
DATA lv_b TYPE i VALUE 2.
DATA lv_c TYPE i.

lv_c = lv_a / lv_b.

WRITE lv_c.

# 2 

# ถ้าอยากได้ 2.5 ต้องทำยังไง?
# use TYPE p
DATA lv_a TYPE p DECIMALS 2 VALUE '5'.
DATA lv_b TYPE p DECIMALS 2 VALUE '2'.
DATA lv_c TYPE p DECIMALS 2.

# ############################################

TYPES: BEGIN OF ty_data,
         value TYPE i,
       END OF ty_data.

DATA: lt_data TYPE TABLE OF ty_data,
      ls_data TYPE ty_data.

ls_data-value = 5.
APPEND ls_data TO lt_data.

ls_data-value = 10.
APPEND ls_data TO lt_data.

CLEAR ls_data.

LOOP AT lt_data INTO ls_data.
  ls_data-value = ls_data-value + 1.
ENDLOOP.

LOOP AT lt_data INTO ls_data.
  WRITE: / ls_data-value.
ENDLOOP.

# 5
# 10