🟢 ตัวอย่าง
# 🎯 ต้องการ order ที่ amount มากที่สุด
DATA: ls_order TYPE zorders.

SELECT order_id amount
  FROM zorders
  INTO ls_order
  ORDER BY amount DESCENDING
  UP TO 1 ROWS.
ENDSELECT.

# Practice 1
🎯 โจทย์ให้ลอง
ดึง order ที่:
- status = 'O'
- amount มากที่สุด

- เก็บลง work area ls_order
- เช็ค sy-subrc

DATA : ls_order TYPE zorders.

Select * from zorders into ls_order Where status = 'O' ORDER BY amount DESCENDING Up to 1 rows ENDSELECT.

if sy-subrc = 0.
    Write 'success'.
else.
    Write 'fail'.
                                    
