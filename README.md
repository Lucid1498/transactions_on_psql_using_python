# Transactions on PostgreSQL using Python

# Table of content:

Features

Requirements

Installation

Schema

Roadmap

ACID Transaction Handling



# Features

We created 3 tables in postgreSQL namely product, depot and stock. Each having some tuples in it.
This project is concentrated on connecting postgreSQL with python and run some transactions on the above given tables while maintaining ACID properties.
The transaction we will be executing will be simple queries including update, insert and delete commands while making sure the ACID properties are not overlooked.

# Requirements

Python : >= 3.7

Adapter: psycopg2

PostgreSQL: >= 9.2


# Installation

Package is uploaded on PyPI

You can install with pip

$ pip install psycopg2

# Schema: Schema is provided below of product, depot and stock.

Make use of a simple table

CREATE TABLE Product (
prod_id CHAR(10),
pname VARCHAR(30),
price DECIMAL);

CREATE TABLE Depot (
dep_id CHAR(10),
addr VARCHAR(50),
volume INT);

CREATE TABLE Stock (
prod_id CHAR(10),
dep_id CHAR(10),
quantity INT);

ALTER TABLE Product ADD CONSTRAINT pk_product PRIMARY KEY (prod_id);

ALTER TABLE Depot ADD CONSTRAINT pk_depot PRIMARY KEY (dep_id);

ALTER TABLE Stock ADD CONSTRAINT pk_stock PRIMARY KEY (prod_id, dep_id);

ALTER TABLE stock ADD CONSTRAINT fk_stock FOREIGN KEY (prod_id) REFERENCES product (prod_id) ON UPDATE CASCADE ON DELETE CASCADE;

ALTER TABLE stock ADD CONSTRAINT fk_stock2 FOREIGN KEY (dep_id) REFERENCES depot (dep_id) ON UPDATE CASCADE ON DELETE CASCADE;

INSERT INTO Product (prod_id, pname, price) VALUES
('p1', 'tape', 2.5),
('p2', 'tv', 250),
('p3', 'vcr', 80);

INSERT INTO Depot (dep_id, addr, volume) VALUES
('d1', 'New York', 9000),
('d2', 'Syracuse', 6000),
('d4', 'New York', 2000);

INSERT INTO Stock (prod_id, dep_id, quantity) VALUES
('p1', 'd1', 1000),
('p1', 'd2', -100),
('p1', 'd4', 1200),
('p3', 'd1', 3000),
('p3', 'd4', 2000),
('p2', 'd4', -1500),
('p2', 'd1', -400),
('p2', 'd2', 2000);


# Roadmap

1. Set Up the Environment (PostgreSQL, Python, Psycopg2)
2. Configure PostgreSQL (Database, Tables)
3. Establish Connection Using Python
4. Perform Basic Transactions
5. Handle Transactions - ACID COMPLIANCE
6. Query and Retrieve Data
7. Close Connections


# ACID Transaction Handling:

1. Atomicity

Ensures that a transaction is treated as a single unit: all operations succeed, or none do.

2. Consistency

Ensures that the database moves from one valid state to another, maintaining data integrity.

3. Isolation

Ensures that transactions are executed independently of one another

4. Durability

Ensures that once a transaction is committed, its changes are permanent, even in case of a system crash.
