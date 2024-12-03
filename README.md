CS623 DBMS Project:

Overview
This project focuses on tasks like adding, renaming, and deleting products and depots from the Stock table, ensuring data consistency and reliability. It demonstrates practical database transactions that adhere to ACID properties.

Features:
1.Add Products and Stock: Add new products to the Product table and their corresponding stock to the Stock table.
2.Rename Products and Depots: Rename products and depots while ensuring consistency between related tables using ON UPDATE CASCADE foreign key relationships.
3.Delete Products and Depots: Safely delete products and depots, maintaining referential integrity.
4.ACID Compliance: All operations follow the ACID properties to ensure data integrity.

**Technologies Used**
PostgreSQL: For database management.
Python: For implementing database operations and transactions.
psycopg2: A PostgreSQL adapter for Python.
Git: For version control and collaboration.
Prerequisites
To run this project, make sure to have the following installed on your system:

PostgreSQL: Ensure that PostgreSQL is installed and running.
Python: Python 3.x (preferably 3.6 or higher) is required.
psycopg2: Install the PostgreSQL adapter for Python:
bash
Copy code
pip3 install psycopg2-binary
Setting Up the Database
Create the Database:
Create the database:

sql
Copy code
CREATE DATABASE cs623_project;
Create the Product, Depot, and Stock tables:

Product Table:

sql
Copy code
CREATE TABLE Product (
    prodid CHAR(10),
    pname VARCHAR(30),
    price DECIMAL
);
ALTER TABLE Product ADD CONSTRAINT pk_product PRIMARY KEY (prodid);
ALTER TABLE Product ADD CONSTRAINT ck_product_price CHECK (price > 0);
INSERT INTO Product (prodid, pname, price) VALUES ('p1', 'tape', 2.5), ('p2', 'tv', 250), ('p3', 'vcr', 80);
Depot Table:

sql
Copy code
CREATE TABLE Depot (
    depid CHAR(10),
    addr VARCHAR(50),
    volume INT
);
ALTER TABLE Depot ADD CONSTRAINT pk_depot PRIMARY KEY (depid);
INSERT INTO Depot (depid, addr, volume) VALUES ('d1', 'New York', 9000), ('d2', 'Syracuse', 6000), ('d4', 'New York', 2000);
Stock Table:

sql
Copy code
CREATE TABLE Stock (
    prodid CHAR(10),
    depid CHAR(10),
    quantity INT
);
ALTER TABLE Stock ADD CONSTRAINT pk_stock PRIMARY KEY (prodid, depid);
ALTER TABLE Stock ADD CONSTRAINT fk_stock_product FOREIGN KEY (prodid) REFERENCES Product(prodid);
ALTER TABLE Stock ADD CONSTRAINT fk_stock_depot FOREIGN KEY (depid) REFERENCES Depot(depid);
INSERT INTO Stock (prodid, depid, quantity) VALUES
('p1', 'd1', 1000), ('p1', 'd2', -100), ('p1', 'd4', 1200),
('p3', 'd1', 3000), ('p3', 'd4', 2000), ('p2', 'd4', 1500),
('p2', 'd1', -400), ('p2', 'd2', 2000);
How to Use
Clone the Repository:

bash
Copy code
git clone https://github.com/tejakusireddy/CS623_Project.git
Configure the Database Connection: Update the database connection in db_connection.py with your credentials:

python
Copy code
conn = psycopg2.connect(
    dbname="cs623_project",   # database name
    user="your_username",    # PostgreSQL username
    password="your_password",# PostgreSQL password
    host="localhost",        # database host
    port="5432"              # database port
)
Run the Transaction Scripts: Execute the Python scripts in the following order:

Add Depot and Stock:
python transaction6_add_depot_and_stock.py

Add Product and Stock:

python transaction5_add_product_and_stock.py

Rename Depot:
python transaction4_rename_depot.py

Rename Product:
python transaction3_rename_product.py

Delete Depot:
python transaction2_delete_depot.py

Delete Product:
python transaction1_delete_product.py

Example Output
After running the scripts, you will see success or error messages based on transaction results. Example output:
Depot d3 added successfully with stock for product p100.
Product p100 added successfully with stock in depot d2.
Depot d2 renamed to Depot Main.
Product p100 renamed to Product DVD.
Depot d2 deleted successfully.
Product p100 deleted successfully.
Contact
If you have any questions or feedback, feel free to reach out:

Email: tejakusireddy23@gmail.com
GitHub: tejakusireddy
