# Chipotle-Data-Analysis

Columns: 

●	Order Id
●	Quantity
●	Item Name
●	Choice Description
●	Item Price


In this task we are working on tsv file so, before diving into the questions, here's a brief introduction to working with TSV files in Pandas:

A TSV (Tab-Separated Values) file is a plain text file where each line represents a data record, and values are separated by tabs. In Pandas, you can use the read_csv function with the sep parameter set to '\t' to read TSV files.

Optional: Converting TSV to CSV in pandas:
If needed, you can convert a TSV file to CSV using the to_csv function with the sep parameter set to ','. Now, let's proceed with the questions for data cleaning using the Chipotle dataset:
Reading TSV File:
Use the pd.read_csv function with sep='\t' to read the Chipotle TSV file into a pandas DataFrame.

# Data Preprocessing

**1. Missing Values:**

**Question:** Check for missing values in each column (Order ID, Quantity, Item Name, Choice Description, Item Price). How should missing values be handled?

**Answer:** 
"Choice Description" column has 1246 missing values. Here are suggestions on how to handle missing values:
With 1246 missing values in the "Choice Description" column, we may consider a few options:
1. If the missing values are not critical for the analysis, leave them as it is.
2. If feasible, infer or impute missing values based on surrounding data or replace them with a placeholder indicating missing information.

**2. Data Types:**
**Question:** Verify the data types of each column. Do they align with their expected types, and should any adjustments be made?

**Answer:** 

**Order ID and Quantity:**

These columns have the expected integer data type (int64) and align with their roles as identifiers and quantities.

**Item Name and Choice Description:**

Both columns have the object data type, which is appropriate for text data. If further analysis involves text processing, no adjustments are necessary.

**Item Price:**

The "Item Price" column is currently of object data type, which suggests it might contain non-numeric characters. To facilitate numerical analysis, consider converting it to a numeric type (e.g., float) using pd.to_numeric or astype(float) after addressing any non-numeric characters.

data['item_price'] = pd.to_numeric(data['item_price'].str.replace('$', ''), errors='coerce')

This code removes the dollar sign and converts the column to a numeric type.

**3. Duplicated Entries:**
**Question:** Identify and handle duplicated entries in the dataset. How might duplicates impact analysis, and what is the appropriate action?

**Answer:** 
There were initially 59 duplicated entries in the dataset. After removing duplicates using data.drop_duplicates(inplace=True), there are no remaining duplicates (output is 0). Here's an explanation of the impact of duplicates on analysis and the appropriate action:

**Impact of Duplicates on Analysis:**

1. Duplicates can lead to inflated or biased statistical measures, affecting the accuracy of analysis results.

2. They may distort frequency distributions and introduce redundancy, potentially influencing insights drawn from the dataset.
   
**Appropriate Action:**

1. Identification: Use data.duplicated().sum() to identify the number of duplicated entries.

2. Removal: Use data.drop_duplicates(inplace=True) to remove duplicated rows.

3. Caution: Before removing duplicates, carefully assess whether duplicates are unintentional or if there's a valid reason for their presence (e.g., repeated orders by the same customer).

4. Consideration: If duplicates are intentional or carry meaningful information, handling them may involve a different strategy, such as aggregating data or keeping the first occurrence.
   
**4. Quantity and Item Price:**
**Question:** Examine the Quantity and Item Price columns. Are there any inconsistencies or anomalies that need correction?

**Answer:**

Quantity:

1. Most orders have a quantity of 1 (4296 occurrences), suggesting standard orders.
2. Some orders have higher quantities. Investigate these for legitimacy or anomalies.
3. Handle anomalies based on the specific analysis requirements. If legitimate, no action may be needed.

Item Price:

1. The "Item Price" column contains numeric values with various price points.
2. Common prices include $8.75 (730 occurrences), $11.25 (521 occurrences), $9.25 (398 occurrences), and $4.45 (349 occurrences).
3. There are 78 unique item prices, and no apparent anomalies are evident from the provided output.
4. Check for non-numeric characters in the "Item Price" column using additional methods. If found, investigate and correct as needed.

**5. Choice Description:**
**Question:** Analyze the Choice Description column. How should choices be handled, especially when there are multiple descriptions for a single item?

**Answer:**

Common Choices:

1. Common choices include individual beverages like Diet Coke (133 occurrences), Coke (115 occurrences), and Sprite (77 occurrences).

2. There are also more complex choices involving combinations of ingredients for items like salsa, rice, black beans, cheese, sour cream, guacamole, and lettuce.

Handling Choices:

1. Choices are represented in a nested format (e.g., [Diet Coke] or [Fresh Tomato Salsa, [Rice, Black Beans, Cheese, Sour Cream, Lettuce]]).

2. Choices with multiple descriptions may require normalization for better analysis.

3. Consider extracting key ingredients or condensing descriptions to create a standardized representation for each choice.
Unique Choices:

4. There are 1043 unique choice descriptions in the dataset, indicating a variety of customization options for items.

Action:

1. Explore and decide on a strategy for handling the nested structure and multiple descriptions in the "Choice Description" column.

2. Standardize choices for consistent analysis, potentially by extracting key ingredients or consolidating similar choices.

3.The goal is to create a uniform representation that captures the essence of each choice.

**6. Handling Special Characters:**
**Question:** Check for special characters in text-based columns (e.g., Item Name, Choice Description). How can these be addressed for consistency?

**Answer:**

The output indicates the presence of special characters in the "Item Name" and "Choice Description" columns:

Item Name: There are 68 occurrences of special characters in the "Item Name" column.

Choice Description: There are 3335 occurrences of special characters in the "Choice Description" column.

Addressing Special Characters:

1. Special characters may impact data consistency and analysis.

2. For both columns, consider removing or replacing special characters to ensure uniformity.

3. Utilize the str.replace method to replace special characters with spaces or an appropriate substitute.

**7. Order Id Integrity:**
**Question:** Cross-reference the Order ID column for integrity. Are there any irregularities or patterns that need validation?

**Answer:**
Here are observations:

Order ID Counts:

1. Each "Order ID" appears multiple times, indicating multiple items/orders associated with each ID.

2. The count column shows the number of occurrences for each unique "Order ID."

Patterns and Irregularities:

1. No obvious irregularities or patterns are immediately apparent from the provided output.

2."Order ID" values seem to be sequential and without missing gaps.
Validation:

1. Verify that "Order ID" values are unique identifiers for each order.

2. Confirm that there are no missing or duplicated "Order ID" values.

3. Cross-reference with the original dataset to ensure consistency.


**8. Item Name Standardization:**
**Question:** Standardize the Item Name column. Are there variations that can be unified for better analysis?

**Answer:** 
The "Item Name" column has been standardized by removing special characters and converting to lowercase, facilitating a consistent format for better analysis and comparisons.

**9. Quantity and Price Relationships:**

**Question:** Investigate the relationships between Quantity and Item Price. Are there cases where adjustments need to be made for accurate analysis?

**Answer:**

Quantity and Item Price Aggregation: The table aggregates the total quantity and total item price for each unique item name.

Relationships: Examining the relationships between quantity and item price for individual items can provide insights into purchasing patterns and pricing strategies.

Adjustments:

1. Investigate cases where the relationship between quantity and item price seems unusual or inconsistent.

2. Verify if there are any outliers or anomalies that need correction.

3. Consider calculating the average price per unit (item) to identify discrepancies.

**10. Handling Categorical Data:**
**Question:** For categorical columns (e.g., Item Name), consider encoding or transforming them into a format suitable for analysis.
**Answer:**

The code data_encoded = pd.get_dummies(data, columns=['item_name'], prefix='item') has encoded the categorical column 'item_name' using one-hot encoding, resulting in a new DataFrame with binary columns for each unique item name. This encoding is suitable for analysis, machine learning models, and various other applications where categorical data needs to be represented in a numerical format.

Key Points:

1. The pd.get_dummies function has created binary columns for each unique item name.

2. Columns are prefixed with 'item_' to distinguish them from other columns.

3. Each row now has a 1 in the corresponding 'item' column, indicating the presence of that item, and 0 in all other 'item' columns.

# Exploratory Data Analysis

**1.  What are the top 5 items available in the store based on the quantity sold?**

**Answer:**

The top 5 items available in the store, ranked by the total quantity sold, are as follows:

Chicken Bowl: 752.0 units
Chicken Burrito: 584.0 units
Chips and Guacamole: 501.0 units
Steak Burrito: 383.0 units
Canned Soft Drink: 340.0 units

**2. What are the top 3 most ordered items in the 'choice_description' category, considering unique names?**

**Answer:**

The top 3 most ordered items in the 'choice_description' category, based on the total quantity sold, are:

[Diet Coke]: 158.0 units
[Coke]: 135.0 units
[Sprite]: 89.0 units

**3. What is the total order count based on the 'order_id' column?**

**Answer:**

The total order count in the dataset, considering unique order IDs, is 4563. This count represents the number of distinct orders made in the dataset.

**4. How is revenue calculated, and what is the overall revenue for the dataset?**

**Answer:** 

Revenue is calculated by multiplying the 'item_price' by the 'quantity' for each row. The formula for revenue is: revenue = item_price * quantity. The total revenue generated from all orders in the dataset is $39,237.02.

**5. What is the average revenue per order for the top 5 and bottom 5 items in the dataset?**

**Answer:**

The average revenue per order for the top 5 items is approximately $18.18.
The average revenue per order for the bottom 5 items is approximately $2.37.

**6. How many different items are sold, and what are their names?**

**Answer:**

There are 50 different items sold, and here is the list of unique item names:

chips and fresh tomato salsa
izze
nantucket nectar
chips and tomatillogreen chili salsa
chicken bowl
side of chips
steak burrito
steak soft tacos
chips and guacamole
chicken crispy tacos
chicken soft tacos
chicken burrito
canned soda
barbacoa burrito
carnitas burrito
carnitas bowl
bottled water
chips and tomatillo green chili salsa
barbacoa bowl
chips
chicken salad bowl
steak bowl
barbacoa soft tacos
veggie burrito
veggie bowl
steak crispy tacos
chips and tomatillo red chili salsa
barbacoa crispy tacos
veggie salad bowl
chips and roasted chilicorn salsa
chips and roasted chili corn salsa
carnitas soft tacos
chicken salad
canned soft drink
steak salad bowl
6 pack soft drink
chips and tomatillored chili salsa
bowl
burrito
crispy tacos
carnitas crispy tacos
steak salad
chips and mild fresh tomato salsa
veggie soft tacos
carnitas salad bowl
barbacoa salad bowl
salad
veggie crispy tacos
veggie salad
carnitas salad


**7. What is the total cost and quantity of every unique item?**

**Answer:**

| Item Name | Total Quantity | Total Cost |
| --- | --- | --- |
| 6 pack soft drink | 55.0 | 356.95 |
| barbacoa bowl | 65.0 | 663.11 |
| barbacoa burrito | 90.0 | 885.50 |
| barbacoa crispy tacos | 12.0 | 120.21 |
| barbacoa salad bowl | 9.0 | 97.01 |
| barbacoa soft tacos | 25.0 | 250.46 |
| bottled water | 204.0 | 292.06 |
| bowl | 4.0 | 29.60 |
| burrito | 6.0 | 44.40 |
| canned soda | 124.0 | 135.16 |
| canned soft drink | 340.0 | 425.00 |
| carnitas bowl | 71.0 | 736.71 |
| carnitas burrito | 60.0 | 597.83 |
| carnitas crispy tacos | 8.0 | 77.96 |
| carnitas salad | 1.0 | 8.99 |
| carnitas salad bowl | 6.0 | 66.34 |
| carnitas soft tacos | 40.0 | 375.94 |
| chicken bowl | 752.0 | 7259.75 |
| chicken burrito | 584.0 | 5509.57 |
| chicken crispy tacos | 50.0 | 472.13 |
| chicken salad | 9.0 | 81.09 |
| chicken salad bowl | 123.0 | 1228.75 |
| chicken soft tacos | 116.0 | 1070.85 |
| chips | 227.0 | 487.89 |
| chips and fresh tomato salsa | 130.0 | 361.36 |
| chips and guacamole | 501.0 | 2178.79 |
| chips and mild fresh tomato salsa | 1.0 | 3.00 |
| chips and roasted chili corn salsa | 23.0 | 67.85 |
| chips and roasted chilicorn salsa | 18.0 | 43.02 |
| chips and tomatillo green chili salsa | 45.0 | 132.75 |
| chips and tomatillo red chili salsa | 48.0 | 141.60 |
| chips and tomatillogreen chili salsa | 33.0 | 78.87 |
| chips and tomatillored chili salsa | 24.0 | 57.36 |
| crispy tacos | 2.0 | 14.80 |
| izze | 19.0 | 64.41 |
| nantucket nectar | 29.0 | 98.31 |
| salad | 2.0 | 14.80 |
| side of chips | 110.0 | 185.90 |
| steak bowl | 220.0 | 2250.94 |
| steak burrito | 383.0 | 3818.94 |
| steak crispy tacos | 36.0 | 357.34 |
| steak salad | 4.0 | 35.66 |
| steak salad bowl | 31.0 | 343.59 |
| steak soft tacos | 56.0 | 536.05 |
| veggie bowl | 87.0 | 867.99 |
| veggie burrito | 97.0 | 934.77 |
| veggie crispy tacos | 1.0 | 8.49 |
| veggie salad | 6.0 | 50.94 |
| veggie salad bowl | 18.0 | 182.50 |
| veggie soft tacos | 8.0 | 73.96 |

## Data Cleaning and Analysis Summary:

### 1. Handling Duplicates

```python
data.drop_duplicates(inplace=True)
```
The dataset initially had 59 duplicated entries. After removal, a clean dataset with no duplicate records was obtained.

### 2. Quantity and Item Price Examination
```
data['quantity'].value_counts()
```
Quantity had reasonable values, and no anomalies were observed. Item prices were within a reasonable range, and no inconsistencies were detected.

### 3. Choice Description Analysis
```
data['choice_description'].value_counts()
```
The 'Choice Description' column revealed numerous variations for similar items. Multiple descriptions exist for a single item.

### 4. Special Characters Handling
```
data['item_name'] = data['item_name'].str.replace('[^A-Za-z0-9 ]', '', regex=True)
data['choice_description'] = data['choice_description'].str.replace('[^A-Za-z0-9 ]', '', regex=True)
```
Special characters in 'Item Name' and 'Choice Description' columns were identified and removed for consistency.

### 5. Standardizing Item Names
```
data['item_name'] = data['item_name'].str.replace('[^A-Za-z0-9 ]', '', regex=True)
data['item_name'] = data['item_name'].str.lower()
```
Item names were standardized by removing special characters and converting to lowercase.

### 6. Cross-Referencing Order ID
```
data.groupby('order_id').size().reset_index(name='count')
```
Order IDs were cross-referenced for integrity, revealing a count of orders for each ID.

### 7. Quantity and Item Price Relationship
```
data.groupby('item_name')['quantity', 'item_price'].sum().reset_index()
```
The relationship between Quantity and Item Price was examined for each item.

### 8. Average Price per Unit Calculation
```
average_price_per_unit = data.groupby('item_name')['item_price'].mean()
```
Average price per unit (item) was calculated to identify discrepancies.

### 9. Encoding Categorical Columns
```
data_encoded = pd.get_dummies(data, columns=['item_name'], prefix='item')
```
Categorical columns, such as 'Item Name', were encoded for analysis.

### 10. Top 5 Items by Quantity
```
data.groupby('item_name')['quantity'].sum().sort_values(ascending=False).head(5)
```
The top 5 items by quantity were identified.

### 11. Top 3 Choice Descriptions
```
data.groupby('choice_description')['quantity'].sum().sort_values(ascending=False).head(3)
```
The top 3 choice descriptions were identified based on the total quantity.

### 12. Total Order Count
```
data['order_id'].value_counts().sum()
```
The total order count in the dataset was found to be 4563.

### 13. Total Revenue Calculation
```
data['revenue'] = data['item_price'] * data['quantity']
total_revenue = data['revenue'].sum()
```
A new 'revenue' column was created by multiplying item price and quantity. The total revenue was calculated.

### 14. Average Revenue per Order
```
average_revenue_per_order = data['revenue'].groupby(data['order_id']).mean()
```
Average revenue amount per order was calculated.

### 15. Unique Items Count and List
```
print(data['item_name'].nunique())
print(data['item_name'].unique())
```
The number of different items sold was found to be 50, and the unique names were listed.

### 16. Total Cost and Quantity of Each Item
```
data.groupby('item_name')['quantity', 'item_price'].sum()
```
Total cost and quantity for each unique item were calculated and presented.


## Conclusion:

The analysis and cleaning procedures have resulted in a comprehensive understanding of the dataset. Duplicates were successfully removed, and columns were standardized for consistency. The examination of quantities, item prices, and choice descriptions provided insights into the dataset's characteristics.

The encoding of categorical columns allows for a more in-depth analysis, and the identification of top items by quantity and revenue sheds light on popular products. The total order count and revenue metrics provide an overview of the overall performance.

Going forward, these clean and processed data can be used for more advanced analytics, such as trend analysis, forecasting, or customer segmentation. The insights gained from this dataset can be valuable for strategic decision-making within the business.



