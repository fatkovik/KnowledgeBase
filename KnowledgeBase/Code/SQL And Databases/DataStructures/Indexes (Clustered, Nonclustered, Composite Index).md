[[Data Structures in DB core]]

Indexes are data structure that improve the performance of data retrieval operations in a database. they create a sorted representation of the data in a table allowing for faster searches and queries. There several types of indexes:

- **Clustered Index**: A clustered index physically reorders the rows in a table based on the **index** key values. Each table can have only one clustered index.
- **Nonclustered Index**: A nonclustered index is a separate object that contains the index key values and pointers to the corresponding rows in the table. A table can have multiple nonclustered indexes.
- **Composite Index**: A composite index is an index that includes multiple columns in the index key. It can be either clustered or nonclustered.

```
-- Clustered index
CREATE CLUSTERED INDEX idx_customers_name
ON customers (last_name, first_name);

-- Nonclustered index
CREATE NONCLUSTERED INDEX idx_orders_date
ON orders (order_date);

-- Composite index
CREATE INDEX idx_products_category_price
ON products (category_id, price);
```