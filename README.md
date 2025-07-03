# sqlintern
#task 7:
CREATE DATABASE SchoolDB;
USE SchoolDB;

CREATE TABLE Students (
    StudentID INT PRIMARY KEY,
    Name VARCHAR(100),
    Department VARCHAR(50),
    Marks INT
);
CREATE TABLE Teachers (
    TeacherID INT PRIMARY KEY,
    Name VARCHAR(100),
    Subject VARCHAR(50)
);

INSERT INTO Students VALUES
(1, 'Alice', 'CS', 87),
(2, 'Bob', 'IT', 76),
(3, 'Charlie', 'CS', 92);

INSERT INTO Teachers VALUES
(1, 'Dr. Smith', 'CS'),
(2, 'Prof. John', 'IT');

CREATE VIEW HighScorers AS
SELECT Name, Marks
FROM Students
WHERE Marks > 80;

CREATE VIEW StudentDepartmentInfo AS
SELECT s.Name AS StudentName, s.Department, t.Name AS TeacherName
FROM Students s
JOIN Teachers t ON s.Department = t.Subject;

SELECT * FROM HighScorers;

SELECT * FROM StudentDepartmentInfo;

DROP VIEW HighScorers;

output:
![Screenshot 2025-07-03 213423](https://github.com/user-attachments/assets/a308f906-d021-48fb-9883-093a7732dda1)
![Screenshot 2025-07-03 213342](https://github.com/user-attachments/assets/56c81752-9e5c-4e7b-9da3-0a9909dd08ec)





# task 6:
# 1. Scalar Subquery SELECT title, total_copies FROM books WHERE total_copies = (SELECT MAX(total_copies) FROM books);
![image](https://github.com/user-attachments/assets/91937f42-4470-435d-90b2-6300996d2b53)
# 2. Correlated Subquery SELECT name FROM members m WHERE EXISTS ( SELECT 1 FROM issued_books ib WHERE ib.member_id = m.member_id );
![image](https://github.com/user-attachments/assets/2d27265f-3c7a-4ae7-a713-0abfa4043854)
# 3. Subquery with IN SELECT name FROM authors WHERE author_id IN ( SELECT DISTINCT author_id FROM book_author );
![image](https://github.com/user-attachments/assets/e45c0efa-290a-493b-84ea-c4a72b1ed7ef)
# 4. Subquery with EXISTS SELECT title FROM books b WHERE EXISTS ( SELECT 1 FROM issued_books i WHERE i.book_id = b.book_id );
![image](https://github.com/user-attachments/assets/5dc7c1b8-d171-46e0-9fc5-9f3e183005e6)
# 5. Subquery with = SELECT name FROM categories WHERE category_id = ( SELECT category_id FROM books ORDER BY book_id DESC LIMIT 1 );
![image](https://github.com/user-attachments/assets/1dd39643-0212-40c8-9720-60cf5254fbbe)

# task 5:
# INNER SELECT b.title, c.name AS category FROM books b INNER JOIN categories c ON b.category_id = c.category_id;
![image](https://github.com/user-attachments/assets/b6b4de7e-59d9-45d0-bdfa-7abb41f44c81)
# LEFT SELECT b.title, c.name AS category FROM books b LEFT JOIN categories c ON b.category_id = c.category_id;
![image](https://github.com/user-attachments/assets/32b27152-14ff-4e3f-923c-eceeefaaddf9)

# RIGHT SELECT b.title, c.name AS category FROM books b RIGHT JOIN categories c ON b.category_id = c.category_id;
![image](https://github.com/user-attachments/assets/b9c0a1a2-e3c6-42e3-8388-f0c2fa184511)

# FULL JOIN SELECT b.title, c.name AS category FROM books b LEFT JOIN categories c ON b.category_id = c.category_id UNION SELECT b.title, c.name AS category FROM books b RIGHT JOIN categories c ON b.category_id = c.category_id;
![image](https://github.com/user-attachments/assets/5ef0f233-c2aa-46a2-bd81-c779694538dd)

# task 4:
create database sales_db;

use sales_db;

CREATE TABLE Customers (
    customer_id INT PRIMARY KEY,
    customer_name VARCHAR(100),
    country VARCHAR(50),
    customer_since DATE
);

-- Create Products table
CREATE TABLE Products (
    product_id INT PRIMARY KEY,
    product_name VARCHAR(100),
    category VARCHAR(50),
    price DECIMAL(10,2)
);

-- Create Orders table (for aggregation exercises)
CREATE TABLE Orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    order_date DATE,
    total_amount DECIMAL(10,2),
    status VARCHAR(20),
    FOREIGN KEY (customer_id) REFERENCES Customers(customer_id)
);


INSERT INTO Customers VALUES
(1, 'Alice Johnson', 'USA', '2020-01-15'),
(2, 'Bob Smith', 'UK', '2019-05-20'),
(3, 'Carlos Ruiz', 'Spain', '2021-03-10'),
(4, 'Diana Chen', 'USA', '2020-11-05'),
(5, 'Ethan Wilson', 'Canada', '2022-02-18');

-- Insert products
INSERT INTO Products VALUES
(101, 'Wireless Headphones', 'Electronics', 99.99),
(102, 'Bluetooth Speaker', 'Electronics', 79.99),
(103, 'Desk Lamp', 'Home', 29.99),
(104, 'Notebook', 'Office', 9.99),
(105, 'Coffee Mug', 'Home', 12.99);

-- Insert orders
INSERT INTO Orders VALUES
(1001, 1, '2023-01-10', 199.98, 'Completed'),
(1002, 2, '2023-01-15', 79.99, 'Completed'),
(1003, 1, '2023-02-05', 119.97, 'Shipped'),
(1004, 3, '2023-02-20', 29.99, 'Completed'),
(1005, 4, '2023-03-01', 139.96, 'Processing');


SELECT COUNT(*) AS total_orders FROM Orders;

SELECT SUM(total_amount) AS total_sales FROM Orders;

SELECT AVG(total_amount) AS average_order_value FROM Orders;

SELECT 
    MIN(total_amount) AS smallest_order,
    MAX(total_amount) AS largest_order
FROM Orders;

SELECT 
    status, 
    COUNT(*) AS order_count
FROM Orders
GROUP BY status;

SELECT 
    customer_id,
    COUNT(*) AS order_count
FROM Orders
GROUP BY customer_id
HAVING COUNT(*) > 1;


# output:

![Screenshot 2025-06-27 203223](https://github.com/user-attachments/assets/24be8256-78e4-4c62-952f-274912d574f8)
![Screenshot 2025-06-27 203325](https://github.com/user-attachments/assets/f419deb3-eceb-41ce-bbbe-efd7b93e3b99)
![Screenshot 2025-06-27 203349](https://github.com/user-attachments/assets/743901b1-313d-485f-b91e-79f9f360ad3f)
![Screenshot 2025-06-27 203409](https://github.com/user-attachments/assets/0b0aa528-0bda-42ba-9f2d-338aec52149c)
![Screenshot 2025-06-27 203435](https://github.com/user-attachments/assets/d093fcc1-dde2-42b7-bfad-a10e5d5165a1)
![Screenshot 2025-06-27 203519](https://github.com/user-attachments/assets/d29ee16b-cba9-4c98-a007-488af82dd710)


# task 3:

CREATE DATABASE sample_db;
USE sample_db;

-- Create Employees table
CREATE TABLE Employees (
    employee_id INT PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    department VARCHAR(50),
    salary DECIMAL(10,2),
    hire_date DATE,
    email VARCHAR(100)
);

-- Create Products table
CREATE TABLE Products (
    product_id INT PRIMARY KEY,
    product_name VARCHAR(100),
    category VARCHAR(50),
    price DECIMAL(10,2),
    stock_quantity INT,
    supplier_id INT
);

-- Create Orders table
CREATE TABLE Orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    order_date DATE,
    total_amount DECIMAL(10,2),
    status VARCHAR(20)
);

-- Insert data into Employees
INSERT INTO Employees VALUES
(1, 'John', 'Doe', 'Sales', 55000.00, '2020-05-15', 'john.doe@company.com'),
(2, 'Jane', 'Smith', 'HR', 60000.00, '2019-03-10', 'jane.smith@company.com'),
(3, 'Robert', 'Johnson', 'IT', 75000.00, '2018-07-22', 'robert.johnson@company.com'),
(4, 'Emily', 'Williams', 'Sales', 52000.00, '2021-01-30', 'emily.williams@company.com'),
(5, 'Michael', 'Brown', 'IT', 80000.00, '2017-11-05', 'michael.brown@company.com');

-- Insert data into Products
INSERT INTO Products VALUES
(101, 'Laptop', 'Electronics', 999.99, 50, 1001),
(102, 'Smartphone', 'Electronics', 699.99, 100, 1001),
(103, 'Desk Chair', 'Furniture', 199.50, 30, 1002),
(104, 'Coffee Table', 'Furniture', 249.99, 20, 1002),
(105, 'Monitor', 'Electronics', 299.99, 75, 1003);

-- Insert data into Orders
INSERT INTO Orders VALUES
(1001, 5001, '2023-01-15', 999.99, 'Completed'),
(1002, 5002, '2023-02-20', 949.98, 'Completed'),
(1003, 5003, '2023-03-10', 449.49, 'Shipped'),
(1004, 5001, '2023-04-05', 199.50, 'Processing'),
(1005, 5004, '2023-05-12', 699.99, 'Completed');

SELECT * FROM Employees;

SELECT first_name, last_name, department FROM Employees;

SELECT * FROM Products WHERE category = 'Electronics';

SELECT * FROM Employees 
WHERE department = 'IT' AND salary > 70000;

SELECT * FROM Products 
WHERE category = 'Electronics' OR price > 200;

SELECT * FROM Employees 
WHERE email LIKE '%@company.com';

SELECT * FROM Orders 
WHERE order_date BETWEEN '2023-01-01' AND '2023-03-31';

SELECT * FROM Employees ORDER BY last_name;

# output:

![Screenshot 2025-06-26 210115](https://github.com/user-attachments/assets/6c391dba-cb94-498a-bb31-a4ee1c4033d1)
![Screenshot 2025-06-26 210003](https://github.com/user-attachments/assets/f1de590e-acd6-42d6-b5f8-d0406b6d91ff)
![Screenshot 2025-06-26 205939](https://github.com/user-attachments/assets/1be84beb-1ab6-4638-8eea-84d4f2423742)
![Screenshot 2025-06-26 205917](https://github.com/user-attachments/assets/3a8d7c71-4bd9-4428-8234-765580940fd1)
![Screenshot 2025-06-26 205852](https://github.com/user-attachments/assets/78b6a84a-793b-426b-b42b-4ce257309e53)
![Screenshot 2025-06-26 205823](https://github.com/user-attachments/assets/294eda81-d780-4f89-bda9-adfb0f09df30)
![Screenshot 2025-06-26 205739](https://github.com/user-attachments/assets/3a1dd69c-b4ba-4368-92cb-53a0bb03bb43)
![Screenshot 2025-06-26 205712](https://github.com/user-attachments/assets/eda62a3e-546a-4738-b324-fad12faab0fb)





# task 2:
# insert query:
INSERT INTO members (member_id, name, email, phone, address)
VALUES (3, 'Emily Thomas', 'emily@example.com', '9001234567', '789 Library Ln, City');
# (missing bio handled with NULL):
INSERT INTO authors (author_id, name, biography)
VALUES (3, 'Stephen King', NULL);
# Handle Missing Values using NULL or DEFAULT
ALTER TABLE returns MODIFY fine DECIMAL(10,2) DEFAULT 0.00;
INSERT INTO returns (return_id, issue_id, return_date)
VALUES (2, 1, '2025-07-10');
# Use UPDATE and DELETE with WHERE
UPDATE books
SET available_copies = 4
WHERE book_id = 1;
# Delete a member by ID:
DELETE FROM members
WHERE member_id = 2;
# output:
![image](https://github.com/user-attachments/assets/abbe045e-2458-46a3-bcbc-9ac206cdff0b)
![image](https://github.com/user-attachments/assets/541bd845-b41e-4511-a343-d9429b13203e)
![image](https://github.com/user-attachments/assets/fc711643-ac4e-488b-b4b7-b969a1197120)
![image](https://github.com/user-attachments/assets/ba695a77-c3c3-4324-a617-115a6086d356)
![image](https://github.com/user-attachments/assets/93f3ef4c-61de-4512-a1e1-d4b934293db7)
![image](https://github.com/user-attachments/assets/b8b3d6df-bc85-4194-a8a3-03e42f05251b)

# task-1:
# code:
use library_man;
-- MEMBERS
CREATE TABLE members (
    member_id INT PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100) UNIQUE,
    phone VARCHAR(15),
    address TEXT
);

INSERT INTO members VALUES
(1, 'John Doe', 'john@example.com', '9876543210', '123 Main Street, City'),
(2, 'Jane Smith', 'jane@example.com', '9123456789', '456 Park Ave, City');

-- ADMINS
CREATE TABLE admins (
    admin_id INT PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100) UNIQUE,
    password_hash VARCHAR(255),
    role VARCHAR(50)
);

INSERT INTO admins VALUES
(1, 'Admin One', 'admin1@library.com', '$2y$10$adminhash1', 'superadmin');

-- CATEGORIES
CREATE TABLE categories (
    category_id INT PRIMARY KEY,
    name VARCHAR(100)
);

INSERT INTO categories VALUES
(1, 'Fiction'),
(2, 'Science'),
(3, 'History');

-- AUTHORS
CREATE TABLE authors (
    author_id INT PRIMARY KEY,
    name VARCHAR(100),
    biography TEXT
);

INSERT INTO authors VALUES
(1, 'George Orwell', 'Author of 1984 and Animal Farm'),
(2, 'Isaac Newton', 'Famous physicist and mathematician');

-- BOOKS
CREATE TABLE books (
    book_id INT PRIMARY KEY,
    title VARCHAR(200),
    publisher VARCHAR(100),
    year_published INT,
    category_id INT,
    total_copies INT,
    available_copies INT,
    FOREIGN KEY (category_id) REFERENCES categories(category_id)
);

INSERT INTO books VALUES
(1, '1984', 'Secker & Warburg', 1949, 1, 5, 3),
(2, 'Principia Mathematica', 'Cambridge University Press', 1687, 2, 2, 2);

-- BOOK_AUTHOR
CREATE TABLE book_author (
    book_id INT,
    author_id INT,
    PRIMARY KEY (book_id, author_id),
    FOREIGN KEY (book_id) REFERENCES books(book_id),
    FOREIGN KEY (author_id) REFERENCES authors(author_id)
);

INSERT INTO book_author VALUES
(1, 1),
(2, 2);

-- ISSUED BOOKS
CREATE TABLE issued_books (
    issue_id INT PRIMARY KEY,
    book_id INT,
    member_id INT,
    issue_date DATE,
    due_date DATE,
    FOREIGN KEY (book_id) REFERENCES books(book_id),
    FOREIGN KEY (member_id) REFERENCES members(member_id)
);

INSERT INTO issued_books VALUES
(1, 1, 1, '2025-06-20', '2025-07-05');

-- RETURNS
CREATE TABLE returns (
    return_id INT PRIMARY KEY,
    issue_id INT,
    return_date DATE,
    fine DECIMAL(10,2),
    FOREIGN KEY (issue_id) REFERENCES issued_books(issue_id)
);

INSERT INTO returns VALUES
(1, 1, '2025-07-04', 0.00);

ER DIAGRAM:
![library](https://github.com/user-attachments/assets/57372ebe-f292-4616-8d53-f17dce807d65)

OUTPUT:
![image](https://github.com/user-attachments/assets/73514df5-051b-4279-8374-bd37f47bc927)
![image](https://github.com/user-attachments/assets/24123d2e-0e23-4cfc-a4ee-2fc7156b32e4)
![image](https://github.com/user-attachments/assets/e048bc7b-ec44-40bd-8f41-fbd1c51c8207)
![image](https://github.com/user-attachments/assets/da5b4e54-b697-4b4f-a3ac-82c99ebcccfe)
![image](https://github.com/user-attachments/assets/8022474a-71c0-4706-b20a-d5ea329fc63a)

