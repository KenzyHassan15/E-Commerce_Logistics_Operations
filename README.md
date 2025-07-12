# 📦 E-Commerce Logistics Case Study with Power BI

## 🎯 Objective
Hello,
I’m going to walk you through the full process I followed to clean, process, and analyze e-commerce logistics datasets using Power BI. The goal was to assess key operational KPIs and derive actionable insights from real-world delivery data.

---

## 🔹 1. Data Loading and Initial Checks

- Imported the following datasets into Power BI:
  - `Orders.xlsx`
  - `Deliveries.xlsx`
  - `Products.xlsx`
- Reviewed and corrected data types (Dates, Booleans, Text, etc.)
- Created relationships to form a unified data model:
  - `Orders[OrderID]` → `Deliveries[OrderID]`
  - `Orders[ProductID]` → `Products[ProductID]`
---

## 🔹 2. Calendar Table Creation

- Built a dynamic calendar table using Power Query.
- Extracted additional fields for time-based analysis:
  - `Year`
  - `Month Number`
  - `Month Name`
  - `Quarter`
  - `Day`
---

## 🔹 3. Data Cleaning and Validation Logic

To ensure consistency between the Orders and Deliveries tables, several calculated columns were created using DAX.

### ✅ Key Logic Columns

| Column Name                         | Description                                                               |
|------------------------------------|----------------------------------------------------------------------------|
| `Delivery Before Order`            | Flags rows where the delivery date < order date                            |
| `Expected Date Before Order`       | Flags rows where expected date < order date                                |
| `Delivered = 0 but has Delivery Date` | Flags cases where order was delivered but the status is incorrect       |
| `Delivered = 1 but Shipped = 0`    | Flags logically invalid deliveries (delivery without shipment)             |
| `IsValid`                          | Master flag consolidating all invalid scenarios                            |
| `ConfirmedShipped`                 | Corrected shipping status using logical assumptions                        |
| `CorrectedDelivered`               | Corrected delivery status based on order timeline and order confermation   |

### 📅 Business Date Logic
#### - I assumed that:-
- `CleanDeliveryDate` = `OrderDate` + 5 days  
- `CleanExpectedDate` = `OrderDate` + 7 days

This assumption standardized delivery timelines for consistency.

---

## 🔹 4. KPI Calculation Using DAX

### 📊 Core KPIs
- `Order Confirmation Rate` = Confirmed Orders / Total Orders
- `Ship Rate` = Shipped Orders / Confirmed Orders
- `Delivery Rate` = Delivered Orders / Shipped Orders
- `Delivery On Time %` = On-Time Delivered / Delivered

### ➕ Extended KPIs
- `Late Delivery Rate` = Late Delivered / Delivered
- `Cancelled Orders Count`
- `Total Orders`
- `Total Customers` (Distinct Count)

---

## 🔹 5. Key Insights & Observations

From the cleaned and validated dataset, the following business insights were extracted:

- ✅ **Order Confirmation Rate**: ~95% —> which is quite strong, Most orders are getting confirmed, showing minimal rejection at the confirmation stage.
- 🚚 **Ship Rate**: ~99% —> So after cleaning our delivery dates. Nearly all confirmed orders are being shipped, showing high logistics responsiveness.
- 📦 **Delivery Rate**: ~86% — High efficiency, reaching 100% among valid records.
- ⏱️ **On-Time Delivery Rate**: ~64% — Suggests improvement opportunities in last-mile delivery.
- ⚠️ **Data Quality Issues**:
  - **490** orders had expected delivery dates **before** the order date.
  - **456** deliveries occurred **before** the order was placed.
  - **144** delivered orders had a `Delivered` flag still set to 0.
  - **41** deliveries occurred where `Shipped` = 0, which is logically incorrect.
- 🛒 **Customer Behavior**:
  - `Call Center` channel accounts for the most orders **(351)** and deliveries **(286)**.
  - `App` and `Website` users show strong engagement with moderate delivery performance.
- 📊 **Product Trends**:
  - `Electronics` category represents **39.3%** of all orders — a high-value and sensitive category.
- 📅 **Seasonality**:
  - Highest order and delivery volume observed in **Month 5 (May)**.

---

## ✅ Final Outcome

This project successfully transformed messy, real-world logistics data into a clean, valid, structured, and insightful Power BI report. The dashboard enables stakeholders to monitor:

- Customer order behavior
- Supplier contributions
- Shipment status
- Delivery accuracy

By using DAX, Power Query, and logical data validation, the analysis provides a reliable operational overview to drive decision-making and logistics optimization.

---

## 📁 Files Included

- `Orders.xlsx` –> Raw order data
- `Deliveries.xlsx` –> Delivery metadata
- `Products.xlsx` –> Product metadata
- `E-Commerce_Logistics_Operations.pbix` –> Complete Power BI report with cleaning logic, KPI calculations, and visuals
- `Logistics Case Study.docx` –> Collected Insights File

---

## 🔧 Tools Used

- **Power BI Desktop**
- **Power Query**
- **DAX**
