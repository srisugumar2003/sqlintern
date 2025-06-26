# sqlintern

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

