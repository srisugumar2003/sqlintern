# sqlintern

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

