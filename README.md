# Test for Symplifyca
This is a CRUD app that needs to have only one view on the index.

## Tech requirements
- Java 21
- Maven
- Thymeleaf (for frontend)
- SpringBoot 3.3.3.
- PostgreSQL 14 or 15
- Flyway (For db migrations)

## Db Structure
Table products {
  id int [pk]
  name varchar
  description varchar
  price varchar
  current_Stock int
}

Table orders {
  id int
  product_id int

  Indexes {
    (id, product_id) [pk]
  }
}

Ref: orders.product_id > products.id

## High level app features
### Top section: Order Creation
Table of products ( This list is fetched from PostgreSQL and created by a .sql document migrated using Flyway )

  Each row needs to have: Select, Name, Description, Price, Stock
  - Select contains a checkbox

  Button that says "Create Order"
  - One order is created for each product selected on the Table of products. 
  - All products under the same order must have the same id.
  - Decrease current_Stock by 1 for each product on the order.
  - After an order is created, all products need to have the checkbox disabled again

### Bottom section: List of Orders
Table of orders ( This list is fetched from PostgreSQL and created by the user )

  Each row needs to have: Order ID, Product

  The combination of id and product_id needs to be unique for all orders
  - This restriction is given by the orders Table and the "(id, product_id) [pk]" Index
  - This means theres only 1 product per order