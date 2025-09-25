# Online_Bookstore_SQLProject

## 📖 Overview

This project simulates an Online Bookstore Database using SQL.
It contains tables such as Books, Customers, and Orders and demonstrates useful SQL queries for analyzing book sales, customer behavior, and inventory management.

The goal of this project is to practice SQL joins, aggregation, filtering, grouping, and analytical queries on a real-world use case.

## Database Schema

Books (Book_ID, Title, Author, Genre,Published_Year, Price, Stock)

Customers (Customer_ID, Name, Email, Phone, City, Country)

Orders (Order_ID, Customer_ID, Book_ID, Quantity, Total_Amount)

### 📊 Business Problems & SQL Solutions
1. **Retrieve the total number of books sold for each genre**:
```sql
select b.Genre, sum(o.Quantity) as Total_Books_sold
from books b
join orders o on b.Book_ID=o.Book_ID
group by b.Genre;
```

2. **Find the average price of books in the "Fantasy" genre**:
```sql
select avg(price) as avg_price
from books
where Genre='Fantasy';
```

3. **List customers who have placed at least 2 orders**:
```sql
select customer_id, count(order_id) as order_count
from orders
group by Customer_ID
having count(order_id)>=2;
```

4. **Find the most frequently ordered book**:
```sql
select o.Book_Id, b.title, count(o.order_id) as order_count
from orders o
join books b on o.Book_ID=b.Book_ID
group by o.Book_Id, b.title
order by order_count desc
;
```

5. **Show the top 3 most expensive books of 'Fantasy' Genre**:
```sql
select * from books
where Genre='Fantasy'
order by Price desc limit 3
;
```

6. **Retrieve the total quantity of books sold by each author**:
```sql
select b.Author, sum(o.Quantity) as Total_Books_count
from orders o
join books b on o.Book_ID=b.Book_ID
group by b.Author
;
```

7. **List the cities where customers who spent over $30 are located**:
```sql
select c.City, o.Total_Amount
from orders o
join customers c on o.Customer_ID=c.Customer_ID
where Total_Amount>30;
```
8. **Find the customer who spent the most on orders**:
```sql
select c.Customer_ID, c.Name, sum(o.Total_Amount) as Total_spent
from orders o
join customers c on o.Customer_ID=c.Customer_ID
group by c.Customer_ID, c.Name
order by Total_spent desc limit 1
;
```

9. **Calculate the stock remaining after fulfilling all orders**:
```sql
select b.Book_ID, b.Title, b.Stock, coalesce(sum(o.Quantity),0) as order_qty,
b.Stock- coalesce(sum(o.Quantity),0) as remaining_qty
from books b
left join orders o on b.Book_ID=o.Book_ID
group by b.Book_ID;
```
## Tech Stack
- **Database**: MySQL / SQL
- **Concepts Used**: Joins, Group By, Aggregate Functions, Having Clause, Order By, Limit

