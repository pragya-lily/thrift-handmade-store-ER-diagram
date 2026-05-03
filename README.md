Thrift & Handmade Store – ER Diagram
Overview
This project represents an ER diagram for a small Instagram-based thrift and handmade store. The database is designed to manage products, customers, orders, payments, and shipping details in a structured way.
It supports both:


Thrift items (usually single/unique pieces)


Handmade items (can have multiple quantities)



Entities


Customer – Stores customer details like name, contact, and address


Product – Contains basic product information


ProductType – Defines whether a product is thrift or handmade


Category – Groups products into categories


ProductVariant – Handles variations like size, color, and condition


Condition – Stores condition of products (important for thrift items)


Inventory – Tracks available stock


Order – Stores order details


OrderItem – Links products with orders


Payment – Stores payment information


Shipment – Stores delivery details



Relationships


One customer can place multiple orders


One order can have multiple products


Products can have multiple variants


Each variant is linked to inventory


Orders are linked to payment and shipment



Key Features


Supports both unique and multiple-quantity products


Handles product variations (size, color, condition)


Tracks inventory and stock


Maintains order history


Includes payment and shipping status



Purpose
This ER diagram helps in designing a database for managing a small online store efficiently and can be used for academic or beginner-level projects.
