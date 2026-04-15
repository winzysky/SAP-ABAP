DATA lv_score TYPE i.

lv_score = 100.

CASE lv_score.
    WHEN 100.
        Write "Perfect".
    WHEN 80.
        Write "Good".
    WHEN OTHERS.
        Write "Other".
ENDCASE.