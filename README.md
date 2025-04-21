This is my first SQL assignment while learning at luxdev.Luxdev is a data bootcamp that specializes in teaching anything data science, data engineering and Artificial Intelligence.
Below is the table creation script to be used
create schema luxsql;
SET search_path TO luxsql;

create table customer(
customer_id SERIAL primary key,
first_name VARCHAR(50) not null,
second_name VARCHAR(50) not null,
email VARCHAR(100) unique not null,
phone_number CHAR(10)
);

insert into customer (customer_id,first_name, second_name, email, phone_number)
values
(1,'John', 'Doe', 'john.doe@gmail.com', '0712345678'),
(2,'Jane', 'Smith', 'janesmith@gmail.com', '0778654239'),
(3,'Paul', 'Otieno', 'paulotis@gmail.com', '0722567981'),
(4,'Mary', 'Okello', 'okellomary@gmail.com', '0798723865');

ALTER TABLE customer
ADD COLUMN city VARCHAR(100);
UPDATE customer
SET city = CASE customer_id
WHEN 1 THEN 'Nairobi'
WHEN 2 THEN 'Mombasa'
WHEN 3 THEN 'Kisumu'
WHEN 4 THEN 'Nakuru'
ELSE city -- Keep existing value for other customer IDs
END;
select * from customer;

CREATE TABLE books (
book_id INT PRIMARY KEY,
title VARCHAR(150) NOT NULL,
author VARCHAR(100),
price NUMERIC(8, 2) NOT NULL,
published_date DATE
);

INSERT INTO books (book_id, title, author, price, published_date)
VALUES
(101, 'Understanding SQL', 'David Kimani', 1500.00, '2023-01-15'),
(102, 'Advanced PostgreSQL', 'Grace Achieng', 2500.00, '2023-02-20'),
(103, 'Learning Python', 'James Mwangi', 3000.00, '2022-11-10'),
(104, 'Data Analytics Basics', 'Susan Njeri', 2200.00, '2023-03-05');
select * from books;

CREATE TABLE orders (
order_id SERIAL PRIMARY KEY,
customer_id INT REFERENCES customer(customer_id),
book_id INT REFERENCES books(book_id),
order_date DATE DEFAULT CURRENT_DATE
);

INSERT INTO orders (customer_id, book_id, order_date)

VALUES
(1, 103, '2023-04-01'), -- John ordered Learning Python
(2, 101, '2023-04-02'), -- Jane ordered Understanding SQL
(3, 102, '2023-04-03'), -- Paul ordered Advanced PostgreSQL
(4, 104, '2023-04-04'), -- Mary ordered Data Analytics Basics
(1, 102, '2023-04-05'); -- John ordered Advanced PostgreSQL again

