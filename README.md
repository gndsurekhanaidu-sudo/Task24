# Task24
Objective
Understand how multiple data sources can be combined using a common key and learn how each join type handles matching and unmatched records.
Tools Used
Python
Pandas
Jupyter Notebook
Dataset
Two sample DataFrames are used:
Customers
Customer_ID Name
          1 Ravi
          2 Sita
          3 Ram
Orders
Order_ID   Customer_ID   Amount
     101             1      500
     102             2      700
     103             4      300
Customer_ID is the common key used to combine the two DataFrames.
Installation
If Pandas is not already installed, run:
pip install pandas
Python Code
import pandas as pd

# Create the Customers DataFrame
customers = pd.DataFrame({
    "Customer_ID": [1, 2, 3],
    "Name": ["Ravi", "Sita", "Ram"]
})

# Create the Orders DataFrame
orders = pd.DataFrame({
    "Order_ID": [101, 102, 103],
    "Customer_ID": [1, 2, 4],
    "Amount": [500, 700, 300]
})

print("Customers:")
print(customers)

print("\\nOrders:")
print(orders)

# 1. Inner Join
inner = pd.merge(customers, orders, on="Customer_ID", how="inner")
print("\\nInner Join:")
print(inner)

# 2. Left Join
left = pd.merge(customers, orders, on="Customer_ID", how="left")
print("\\nLeft Join:")
print(left)

# 3. Right Join
right = pd.merge(customers, orders, on="Customer_ID", how="right")
print("\\nRight Join:")
print(right)

# 4. Outer Join
outer = pd.merge(customers, orders, on="Customer_ID", how="outer")
print("\\nOuter Join:")
print(outer)

# Identify matching and unmatched records
checked = pd.merge(
    customers,
    orders,
    on="Customer_ID",
    how="outer",
    indicator=True
)
print("\\nUnmatched Record Check:")
print(checked)

# Save the final combined dataset
outer.to_csv("final_dataset.csv", index=False)
print("\\nFinal dataset saved as final_dataset.csv")
Join Types and Results
Join Type               What it returns         Resulting customer IDs
Inner                   Only matching rows from 1, 2 both DataFrames
Left                    All rows from the left  1, 2, 3 DataFrame and matching
rows from the right
Right                   All rows from the right 1, 2, 4 DataFrame and matching
rows from the left
Outer                   All rows from both      1, 2, 3, 4 DataFrames
Understanding Unmatched Records
When indicator=True is used, Pandas adds a _merge column: - both: the key is present in both DataFrames. - left_only: the key is present only in the left DataFrame. - right_only: the key is present only in the right DataFrame.
NaN indicates a missing value where no matching record was found.
Final Combined Dataset
The outer join is used as the final combined dataset because it keeps every record from both input DataFrames. The result is saved as final_dataset.csv.
Conclusion
This project shows how Pandas merge() combines data from multiple sources using a common key. Inner, left, right, and outer joins produce different results depending on which records are retained. The indicator=True option helps identify unmatched records.
