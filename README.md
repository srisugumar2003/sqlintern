# sqlintern

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

