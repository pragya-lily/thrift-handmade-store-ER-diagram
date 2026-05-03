#  Thrift & Handmade Store – Database Design (ER Diagram)

##  Overview

This project represents the database design for a growing Instagram-based thrift and handmade store. Initially operated through DMs and WhatsApp, the business requires a structured system to manage products, inventory, customer orders, payments, and shipping details.

The ER diagram models real-world scenarios where:

* Some products are **unique (thrift items)**
* Some products are **reusable (handmade items)**
* Orders may contain multiple items
* Customers can place multiple orders
* Payment and shipping tracking is required

---

##  Objectives

The database is designed to:

* Track all available products and their types (thrift/handmade)
* Manage inventory efficiently (including unique items)
* Store customer details and order history
* Handle multiple products within a single order
* Track payment and shipping status
* Maintain clean and normalized data structure

---

##  Entities & Attributes

###  CUSTOMER

Stores customer details.

**Primary Key:** `customer_id`
**Attributes:**

* full_name
* phone
* instagram_handle
* whatsapp_number
* address_line, city, state, postal_code
* created_at

---

###  ORDER

Represents a purchase made by a customer.

**Primary Key:** `order_id`
**Foreign Key:** `customer_id`
**Attributes:**

* order_date
* order_status
* subtotal_amount
* shipping_fee
* total_amount
* order_source (Instagram / WhatsApp)
* notes

---

###  ORDER_ITEM

Handles multiple products within an order (junction table).

**Primary Key:** `order_item_id`
**Foreign Keys:** `order_id`, `variant_id`
**Attributes:**

* quantity
* unit_price
* line_total

---

###  PRODUCT_TYPE

Defines whether a product is thrifted or handmade.

**Primary Key:** `product_type_id`
**Attributes:**

* type_name (Thrift / Handmade)
* description

---

###  PRODUCT

Represents the main product entity.

**Primary Key:** `product_id`
**Foreign Keys:** `product_type_id`, `category_id`
**Attributes:**

* product_name
* description
* base_price
* active_status
* created_at

---

###  CATEGORY

Groups products into categories (e.g., Tops, Dresses, Accessories).

**Primary Key:** `category_id`
**Attributes:**

* category_name
* description

---

###  PRODUCT_VARIANT

Stores product variations like size, color, condition.

**Primary Key:** `variant_id`
**Foreign Keys:** `product_id`, `condition_id`
**Attributes:**

* sku
* size
* color
* unit_price
* is_unique_piece (important for thrift items)
* status

---

###  CONDITION

Defines condition of thrift items.

**Primary Key:** `condition_id`
**Attributes:**

* condition_name (New, Like New, Used, etc.)
* description

---

###  INVENTORY

Tracks stock for each product variant.

**Primary Key:** `inventory_id`
**Foreign Key:** `variant_id`
**Attributes:**

* quantity_on_hand
* quantity_reserved
* reorder_note
* last_updated

---

###  PAYMENT

Stores payment details for orders.

**Primary Key:** `payment_id`
**Foreign Key:** `order_id`
**Attributes:**

* payment_date
* amount_paid
* payment_method
* payment_status
* transaction_reference

---

###  SHIPMENT

Manages delivery and shipping details.

**Primary Key:** `shipment_id`
**Foreign Key:** `order_id`
**Attributes:**

* recipient_name
* phone
* shipping_address
* courier_name
* tracking_number
* shipped_date
* delivered_date
* shipping_status

---

##  Relationships & Cardinality

* **Customer → Order**

  * One customer can place multiple orders (1 : N)

* **Order → Order_Item**

  * One order can contain multiple items (1 : N)

* **Product → Product_Variant**

  * One product can have multiple variants (1 : N)

* **Variant → Inventory**

  * One variant has one inventory record (1 : 1)

* **Order_Item → Variant**

  * Many order items refer to one variant (N : 1)

* **Product → Category**

  * Many products belong to one category (N : 1)

* **Product → Product_Type**

  * Many products belong to one type (N : 1)

* **Order → Payment**

  * One order can have one or multiple payments (1 : N)

* **Order → Shipment**

  * One order has one shipment (1 : 1)

---

##  Key Design Decisions

###  Thrift vs Handmade Handling

* `is_unique_piece` ensures thrift items are treated as **single stock**
* Handmade items can have **multiple quantities in inventory**

###  Inventory Separation

* Inventory is separated from product to:

  * Support scalability
  * Handle stock updates efficiently
  * Avoid redundancy

###  Order Flexibility

* Orders use a junction table (`ORDER_ITEM`) to support:

  * Multiple products per order
  * Quantity tracking
  * Price at time of purchase

###  Payment Tracking

* Separate payment entity allows:

  * Partial payments
  * Multiple payment methods

###  Shipping Tracking

* Shipment stored separately for:

  * Real-time tracking
  * Delivery status management

---
##   ER diagram 
<img width="2000" height="1250" alt="image" src="https://github.com/user-attachments/assets/e003dc11-d631-4d0d-905d-b723d0846fd2" />


##  Conclusion

This ER diagram provides a scalable and realistic database structure for a small but growing Instagram-based thrift and handmade store. It ensures proper handling of unique thrift items, reusable handmade inventory, and complete order lifecycle management from purchase to delivery.

---
