👉 ใช้สำหรับ:
- จัดกลุ่มข้อมูล
- แปลงค่า
- สร้าง field ใหม่จาก logic

🧠 Syntax พื้นฐาน
SELECT field1,
       CASE 
         WHEN condition1 THEN result1
         WHEN condition2 THEN result2
         ELSE result_default
       END AS new_field
FROM table
INTO TABLE @DATA(result).

🔥 Example 1: Basic (แปลงค่า)
SELECT customer_id,
       CASE 
         WHEN country = 'TH' THEN 'Thailand'
         WHEN country = 'US' THEN 'America'
         ELSE 'Other'
       END AS country_name
FROM zcustomers
INTO TABLE @DATA(gt_result).

# Ex.1 (แปลงค่า country code → ให้เป็นชื่อประเทศ)
Table: zcustomers
| customer_id | country |
| ----------- | ------- |
| C001        | TH      |
| C002        | US      |
| C003        | JP      |
| C004        | TH      |

Select  customer_id,
        country,
        CASE
            WHEN country = 'TH' THEN 'Thailand'
            WHEN country = 'US' THEN 'America'
            WHEN country = 'JP' THEN 'Japan'
            ELSE 'Other'
        END AS country_name
FROM zcustomers
INTO TABLE @DATA(lt_result).

# Ex.2 จัดระดับ price ของสินค้า
Table: zproducts
| product_id | price |
| ---------- | ----- |
| P001       | 1200  |
| P002       | 800   |
| P003       | 300   |
| P004       | 0     |
| P005       | NULL  |

🧠 Logic (สำคัญ อ่านดี ๆ)
- price > 1000 → High
- price > 500 → Medium
- price > 0 → Low
- price = 0 → Free
- price IS NULL → Unknown ⭐ (edge case)
- ใช้ IS NULL ไม่ใช่ = NULL

Select  product_id,
        price,

# Self
        CASE
            WHEN price IS NULL THEN 'Unknown'
            WHEN price > 1000 THEN 'HIGH'
            WHEN price > 500 THEN 'Medium'
            WHEN price > 0 THEN 'Low'
            WHEN price = 0 THEN 'FREE'
            ELSE 'Error'
        END AS price_level

# Senior

        CASE
            WHEN price IS NULL THEN 'Unknown'
            WHEN price = 0 THEN 'FREE'
            WHEN price > 1000 THEN 'HIGH'
            WHEN price > 500 THEN 'Medium'
            ELSE 'Low'
        END AS price_level

FROM zproducts
INTO TABLE @DATA(lt_result).

# Ex.3 (No Group by)
SELECT 
  SUM( CASE WHEN status = 'A' THEN amount ELSE 0 END ) AS active_total,
  SUM( CASE WHEN status = 'I' THEN amount ELSE 0 END ) AS inactive_total
FROM zorders
INTO @DATA(gs_result).
- INTO อย่างเดียวคือมีแถวเดียว

| active_total | inactive_total |
| ------------ | -------------- |
| 350          | 450            |

# Ex.3 (Group by)
SELECT status,
       SUM( amount ) AS total
FROM zorders
GROUP BY status
INTO TABLE @DATA(lt_result).
- INTO TABLE มีหลายแถว
        
| status | total |
| ------ | ----- |
| A      | 350   |
| I      | 450   |

# Ex.4 CASE + SUM
- สรุปยอด amount ออกมาเป็น 3 กลุ่ม
Table: zorders
| order_id | amount |
| -------- | ------ |
| O001     | 300    |
| O002     | 150    |
| O003     | 50     |
| O004     | 220    |
| O005     | NULL   |
| O006     | 180    |

🧠 Logic
- amount > 200 → High
- amount ≤ 200 → Low
- amount IS NULL → Unknown

✍️ Your Task
เขียน ABAP Open SQL ให้ครบ 3 field:
- high_total
- low_total
- unknown_total

Select
        SUM(CASE WHEN amount > 200 THEN amount ELSE 0 END) AS high_total,
        SUM(CASE WHEN amount <= 200 THEN amount ELSE 0 END) AS low_total,
        SUM(CASE WHEN amount IS NULL THEN amount ELSE 0 END) AS unknown_total
FROM zorders
INTO @DATA(lt_result).

# EX5: CASE + SUM + GROUP BY
🎯 Objective
สรุปยอดขาย (amount) แยกตาม customer_id
และแยกเป็น 2 กลุ่ม:
- High (> 200)
- Low (≤ 200)

Table: zorders
| order_id | customer_id | amount |
| -------- | ----------- | ------ |
| O001     | C001        | 300    |
| O002     | C001        | 150    |
| O003     | C002        | 50     |
| O004     | C002        | 220    |
| O005     | C001        | NULL   |
| O006     | C002        | 180    |

SELECT  customer_id,
        SUM(CASE WHEN amount > 200 THEN amount ELSE 0 END) AS high_total,
        SUM(CASE WHEN amount <= 200 THEN amount ELSE 0 END) AS low_total
FROM zorders
GROUP BY customer_id
INTO TABLE @DATA(lt_result).

📊 Mental Model
GROUP BY → แยก row
CASE → แยก logic
SUM → รวมค่า