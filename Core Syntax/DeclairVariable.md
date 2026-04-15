# Declair Variable
DATA lv_name TYPE string.
DATA lv_score TYPE i.


# Convention:
lv_ = local variable
ls_ = structure
lt_ = internal table
(ในโลกจริงใช้ prefix พวกนี้)
# ///////////////////


# Set Variable

lv_name = "Wuttipat".
lv_score = 80.

# WRITE
WRITE lv_name
WRITE lv_score

# Output [in the same line]
# // Wuttipat80 //

`ถามว่ามีทริคอื่นไหม`

# WRITE
WRITE: / lv_name,
       / lv_score.

# Output [Next line]
# // Wuttipat
# // 80