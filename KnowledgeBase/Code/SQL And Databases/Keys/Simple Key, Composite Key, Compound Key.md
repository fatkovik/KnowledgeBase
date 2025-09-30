[[Introduction to Keys]]
- A simple key is a single column used as a primary key or a foreign key.
- A composite key is a combination of two or more columns used as a primary key or a foreign key.
- A compound key is a combination of two or more simple keys used as a foreign key.

```
-- Simple key
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    ...
);

-- Composite key
CREATE TABLE order_items (
    order_id INT,
    product_id INT,
    quantity INT,
    PRIMARY KEY (order_id, product_id)
);

-- Compound key
CREATE TABLE shipments (
    shipment_id INT PRIMARY KEY,
    order_id INT,
    product_id INT,
    FOREIGN KEY (order_id, product_id) REFERENCES order_items(order_id, product_id)
);
```