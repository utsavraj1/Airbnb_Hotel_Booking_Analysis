# Airbnb_Hotel_Booking_Analysis
Edunet-VOIS Internship project

## Project Name
**Airbnb_Hotel_Booking_Analysis**

## Project Overview
This project analyzes the **Airbnb Open Dataset** to extract insights on listings, hosts, pricing, and reviews. Using **data cleaning, exploratory data analysis (EDA), and visualizations**, we explore how property types, neighborhood groups, and host attributes affect listing performance.

---

## Files in the Repository

1. **`Airbnb_Analysis.ipynb`** – Jupyter Notebook containing Python code for data cleaning, analysis, and visualizations.  
2. **`Airbnb Dataset.xlsx`** – Excel dataset used for analysis.  

---

## Dataset Features
The dataset includes:

- `neighbourhood_group` – Borough or neighborhood group  
- `neighbourhood` – Specific neighborhood  
- `room_type` – Entire home/apt, Private room, Shared room, Hotel room  
- `price` – Listing price per night  
- `review_rate_number` – Average review score/stars  
- `calculated_host_listings_count` – Number of listings per host  
- `availability_365` – Number of days available in a year  
- `host_identity_verified` – Whether host is verified  
- `service_fee` – Airbnb service fee  
- `year_built` – Year property was built  

---

## Project Objectives

- Analyze distribution of **property and room types**  
- Identify neighborhoods with **most listings**  
- Determine neighborhoods with **highest average prices**  
- Explore relationship between **property age and price**  
- Identify **top 10 hosts by listings count**  
- Examine if **verified hosts receive more reviews**  
- Explore **price vs service fee correlation**  
- Calculate **Average Review Rate Number (ARRN)** by neighborhood and room type  
- Study **host listings count vs availability**  

---

## Steps Performed

### 1. Data Cleaning
- Checked for missing values and duplicates  
- Standardized column names (lowercase, underscores)  
- Removed duplicate rows  

### 2. Exploratory Data Analysis & Visualizations
- Count and bar plots for room/property types  
- Listings count by neighborhood group  
- Average price by neighborhood  
- Year built vs price scatter plot  
- Top 10 hosts by listings count  
- Verified hosts vs reviews per month  
- Price vs service fee correlation  
- Grouped bar chart for **average review rate (ARRN)**  
- Host listings count vs availability  

---

## Python Code Example

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load dataset
DATA_PATH = "Airbnb Dataset.xlsx"
df = pd.read_excel(DATA_PATH)

# Data Cleaning
df.drop_duplicates(inplace=True)
df.columns = df.columns.str.strip().str.lower().str.replace(" ", "_")

# Example: Average Review Rate Number (ARRN)
ARRN = df.groupby(['neighbourhood_group', 'room_type'])['review_rate_number'].mean().to_frame()
ARRN.rename(columns={'review_rate_number':'average_review_rate'}, inplace=True)
display(ARRN)

# Plot ARRN
ARRN_reset = ARRN.reset_index()
plt.figure(figsize=(12,8))
sns.barplot(data=ARRN_reset, x='neighbourhood_group', y='average_review_rate', hue='room_type', errorbar=None)
plt.xlabel('Neighbourhood Group')
plt.ylabel('Average Review Rate')
plt.title('Average Review Rate for each Room/Property Type in each Neighbourhood Group')
plt.legend(title='Room Type')
plt.show()
