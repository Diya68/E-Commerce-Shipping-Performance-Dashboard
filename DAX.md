# 📊 DAX Measures & Calculated Columns

This document contains the DAX measures and calculated columns used to build the **E-Commerce Shipping Performance Dashboard**.

---

# 📈 Measures

## 1. Total Orders

```DAX
Total Orders = COUNT('Ecommerce Shipping Data'[ID])
```

Returns the total number of orders in the dataset.

---

## 2. Average Product Cost

```DAX
Average Cost = AVERAGE('Ecommerce Shipping Data'[Cost_of_the_Product])
```

Calculates the average cost of all products.

---

## 3. Average Customer Rating

```DAX
Average Rating = AVERAGE('Ecommerce Shipping Data'[Customer_rating])
```

Returns the average customer rating.

---

## 4. Average Discount Offered

```DAX
Average Discount = AVERAGE('Ecommerce Shipping Data'[Discount_offered])
```

Calculates the average discount offered across all orders.

---

## 5. Average Product Weight

```DAX
Average Weight = AVERAGE('Ecommerce Shipping Data'[Weight_in_gms])
```

Returns the average weight of shipped products.

---

## 6. Average Customer Care Calls

```DAX
Average Calls = AVERAGE('Ecommerce Shipping Data'[Customer_care_calls])
```

Calculates the average number of customer care calls per order.

---

## 7. On-Time Orders

```DAX
On Time Orders =
CALCULATE(
    COUNT('Ecommerce Shipping Data'[ID]),
    'Ecommerce Shipping Data'[Reached.on.Time_Y.N] = 1
)
```

Counts the number of orders delivered on time.

---

## 8. Delayed Orders

```DAX
Delayed Orders =
CALCULATE(
    COUNT('Ecommerce Shipping Data'[ID]),
    'Ecommerce Shipping Data'[Reached.on.Time_Y.N] = 0
)
```

Counts the number of delayed orders.

---

## 9. On-Time Delivery Percentage

```DAX
On Time % =
DIVIDE(
    [On Time Orders],
    [Total Orders],
    0
)
```

Calculates the percentage of on-time deliveries.

---

## 10. Delayed Delivery Percentage

```DAX
Delayed % =
DIVIDE(
    [Delayed Orders],
    [Total Orders],
    0
)
```

Calculates the percentage of delayed deliveries.

---

# 📋 Calculated Columns

## 1. Delivery Status

```DAX
Delivery Status =
IF(
    'Ecommerce Shipping Data'[Reached.on.Time_Y.N] = 1,
    "On Time",
    "Delayed"
)
```

Categorizes each order based on delivery status.

---

## 2. Customer Satisfaction

```DAX
Customer Satisfaction =
SWITCH(
    TRUE(),
    'Ecommerce Shipping Data'[Customer_rating] >= 4, "Satisfied",
    'Ecommerce Shipping Data'[Customer_rating] = 3, "Neutral",
    "Dissatisfied"
)
```

Groups customers based on their ratings.

---

## 3. Weight Category

```DAX
Weight Category =
SWITCH(
    TRUE(),
    'Ecommerce Shipping Data'[Weight_in_gms] < 2000, "Light",
    'Ecommerce Shipping Data'[Weight_in_gms] < 3500, "Medium",
    "Heavy"
)
```

Categorizes products into Light, Medium, and Heavy based on weight.

---
