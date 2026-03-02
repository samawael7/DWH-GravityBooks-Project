# 📊 Gravity Books - Data Warehouse Project

A complete **Data Warehouse** solution implementing a **Star Schema** with **ETL pipeline** using **SQL Server Integration Services (SSIS)**.

---

## 🎯 Project Overview

This project demonstrates end-to-end data warehouse design and implementation for **Gravity Books**, a bookstore database. The solution enables analytical reporting on sales, customers, and inventory data.

**Key Features:**
- ⭐ Star Schema dimensional modeling
- 🔄 Complete ETL pipeline using SSIS
- 📈 Business intelligence ready for reporting
- 🗂️ Fact and dimension tables with proper relationships

---

## 🏗️ Architecture

### **Star Schema Design**

**Fact Table:**
- `Sales_fact` - Grain: One row per book sold in each order
  - Measures: quantity, unit_price, shipping_cost, total_sales

**Dimension Tables:**
- `Date_dim` - Time dimension (2015-2030)
- `Customer_dim` - Customer information
- `Book_dim` - Book catalog with authors and publishers
- `Shipping_method_dim` - Shipping methods
- `Address_dim` - Delivery addresses
- `Order_status_dim` - Order statuses

<img width="1032" height="769" alt="Star Schema DWH" src="https://github.com/user-attachments/assets/dc81ec12-750d-4879-9bdb-42f295163cae" />

---

## 🔄 ETL Process

**Tool:** SQL Server Integration Services (SSIS)

**Pipeline:**
1. **Extract** - Read data from source OLTP database (gravity_books)
2. **Transform** - Data cleansing, lookups, and surrogate key generation
3. **Load** - Insert into dimensional model (gravity_books_DWH)

### SSIS Package Structure

**Load Dimensions:**

<img width="324" height="417" alt="Load Dimensions" src="https://github.com/user-attachments/assets/a4ea4e2d-7117-45e4-9179-6b214a6ced88" />

**Load Fact (with Lookups):**

<img width="526" height="550" alt="Load Fact (Lookups)" src="https://github.com/user-attachments/assets/4c4360a4-c2a7-4622-bd5b-e36acc58424d" />

**Key Transformations:**
- Surrogate key generation using IDENTITY columns
- Date dimension pre-populated with calendar dates
- Lookup transformations for dimension keys
- Data type conversions and NULL handling

---

## 📊 Data Volume

| Table | Rows |
|-------|------|
| Customer_dim | ~2,000 |
| Book_dim | ~11,000 |
| Date_dim | ~5,800 |
| Sales_fact | ~15,400 |

---

## 🛠️ Technologies

- **Database:** Microsoft SQL Server
- **ETL:** SQL Server Integration Services (SSIS)
- **IDE:** Visual Studio with SSDT
- **Version Control:** Git & GitHub

---

## 📁 Project Structure
```
DWH-GravityBooks-Project/
│
├── README.md
├── Databases/
│   ├── gravity_books.bak           # Source OLTP database
│   └── Gravity_books_DWH           # Data Warehouse
│
├── GravityBooks_ETL/
│   └── project ssis.dtsx            # SSIS Package
│
└── Output screenshots/
    ├── Star Schema DWH.png
    ├── Load Dimensions.png
    └── Load Fact (Lookups).png
```

---

## 🚀 Quick Start

### Prerequisites
- SQL Server 2019+
- SSIS / Visual Studio with SSDT

### Setup
1. **Restore source database:**
```sql
   RESTORE DATABASE gravity_books
   FROM DISK = 'Databases/gravity_books.bak'
```

2. **Create Data Warehouse:**
   - Run DWH creation scripts
   - Load Date dimension

3. **Execute SSIS Package:**
   - Open `project ssis.dtsx` in Visual Studio
   - Configure connection managers
   - Run package (F5)

---

## 📈 Sample Queries

### Top Selling Books
```sql
SELECT TOP 10
    b.title,
    b.author_name,
    COUNT(*) as UnitsSold,
    SUM(f.total_sales) as Revenue
FROM Sales_fact f
JOIN Book_dim b ON f.book_key = b.book_key
GROUP BY b.title, b.author_name
ORDER BY UnitsSold DESC;
```

### Sales by Month
```sql
SELECT 
    d.year_num,
    d.month_num,
    SUM(f.total_sales) as MonthlySales
FROM Sales_fact f
JOIN Date_dim d ON f.date_key = d.date_key
GROUP BY d.year_num, d.month_num
ORDER BY d.year_num, d.month_num;
```

---

## 🎓 Key Learnings

- ✅ Dimensional modeling (Star Schema)
- ✅ Fact vs Dimension design
- ✅ Surrogate keys implementation
- ✅ SSIS ETL development
- ✅ Data quality and integrity
- ✅ Performance optimization

---

## 👤 Author

**Sama Wael**
- GitHub: [@samawael7](https://github.com/samawael7)

---

## 📄 License

This project is part of the ITI Data Engineering Track.

---

*Data Warehouse & ETL Project - March 2026*
