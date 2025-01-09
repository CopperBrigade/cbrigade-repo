create database DB1;
CREATE OR REPLACE SCHEMA DEV;
create or replace schema PROD;
use schema DEV;

CREATE TABLE DB1.DEV.customers (
  customer_id NUMBER PRIMARY KEY,
  name VARCHAR(255),
  email VARCHAR(255)
);

CREATE TABLE DB1.DEV.orders (
  order_id NUMBER PRIMARY KEY,
  customer_id NUMBER,
  order_date DATE,
  FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
);

insert into DB1.DEV.customers (customer_id,name,email)
values 
(1,'alpha','alpha123@gmail.com'),
(2,'beta','beta123@gmail.com'),
(3,'gamma','gamma123@gmail.com');

insert into DB1.DEV.orders (order_id,customer_id,order_date)
values
(1,1,'2022-01-01'),
(2,1, '2022-01-15'),
(3, 2, '2022-02-01'),
(4,3, '2022-03-01');

create or replace view DB1.DEV.my_view1 as
select c.customer_id, c.name, c.email, o.order_id, o.order_date
FROM DB1.DEV.customers c
INNER JOIN DB1.DEV.orders o ON c.customer_id = o.customer_id;

select * from my_view1