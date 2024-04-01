# SE_PROJECT_PHASE3
# Software Design and Modeling
Group Name: LKSHR

# -> Software Architecture
 # 1.Client side (frontend) :
 The frontend of the application is responsible for presenting the user interface to the website visitors.
 Components include product listings, search functionality, checkout process, appointment scheduling interface, and informational pages.
 # 2.Server side (backend) :
 The application's many features are handled by a number of microservices that make up the backend.
 A single domain, such as order processing, content management, product management, authentication, or appointment scheduling, is the focus of each microservice.
 # 3.Database Layer :
 Structured data about goods, orders, appointments, users, and content are all stored in MySQL.
 # 4.Authentication and Authorization:
 Users can register, log in, and manage their accounts securely through the authentication service.

# -> Component Diagram 
                  
User buys —> INDEX —>  log in —> CLIENT INFO <— PRODUCT <—-> EDIT 
               |     <—- product

               | 
               
              USER ——> ORDER 

# -> Detailed Design
# >Class Diagram:

CREATE TABLE orders (
    id INT AUTO_INCREMENT PRIMARY KEY,
    firstname VARCHAR(50) NOT NULL,
    lastname VARCHAR(50) NOT NULL,
    phone VARCHAR(20) NOT NULL,
    email VARCHAR(100) NOT NULL,
    address TEXT NOT NULL,
    product_id INT NOT NULL,
    product_name VARCHAR(255) NOT NULL,
    product_price DECIMAL(10, 2) NOT NULL,
    order_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
Pharmacy class represents the pharmacy entity with attributes such as first name, last name,address , email, and phone. It also includes methods for browsing and searching products.
Product class represents the products available in the pharmacy with attributes such as id, name, description, price, and order date . It includes methods for adding and removing products from the shopping cart.

 # > Sequence Diagrams:
 User        Frontend         Backend          Database
  |             |                |                 |
  |   Browse    |                |                 |
  |  Products   |                |                 |
  |------------>|                |                 |
  |             |                |                 |
  |             |   Get          |                 |
  |             | Products       |                 |
  |             |<---------------|                 |
  |             |                |                 |
  |             |                |                 |
  |             |   Add          |                 |
  |             |  to Cart       |                 |
  |             |--------------->|                 |
  |             |                |    Update       |
  |             |                |   Stock &       |
  |             |                |  Cart Status   |
  |             |                |<---------------|
  |             |                |                 |
  |             |                |                 |
  |   Proceed   |                |                 |
  |   to       |                |                 |
  |   Checkout |                             
  |------------>|                |                 |
  |             |                |                 |
  |             |    Place       |                 |
  |             |   Order        |                 |
  |             |--------------->|                 |
  |             |                |    Update       |
  |             |                |  Order Status  |
  |             |                |<---------------|
  |             |                |                 |
  |   View      |                |                 |
  |   Order     |                |                 |
  |<------------|                |                 |
  |             |                |                 |

  # Database Design:
  # 1.Useres table:
  This table contains data about administrators and clients who have registered to access the pharmacy website.
  User ID, username, email, hashed password, role, and other pertinent information are examples of fields that may be included.
  # 2. Products Table: 
  Information on the drugs, health items, and supplements that are sold at the pharmacy is kept in this table.
Product-related fields might contain the following: product ID, name, description, price, stock amount, category, and so on.
 # 3. Table of orders: 
 This table contains information on user-placed orders, such as order ID, user ID (foreign key), order date, total cost, and order status. 
# > Relationships between Tables:
1. Users-Orders Relationship:
One-to-Many relationship: One user can have multiple orders.
User ID in the Orders table serves as a foreign key referencing the Users table.
2.  Orders-Products Relationship:
Many-to-Many relationship: An order can contain multiple products, and a product can be included in multiple orders.
A separate junction table may be used to represent this relationship, with Order ID and Product ID as foreign keys.

# Modeling 
# -> Use case diagram: 

+-----------------------------------
|          Pharmacy Website         |
+-----------------------------------+
|                                   |
|    1. Browse Products            |
|    2. Search Products            |
|    3. View Product Details       |
|    4. Add Product to Cart        |
|    5. Remove Product from Cart   |
|    6. View Shopping Cart         |
|    7. Proceed to Checkout        |
|    8. Place Order                |
|    9. View Order History         |
|   10. Manage Account             |      |
-----------------------------------
> This use case diagram provides a comprehensive overview of the functionalities offered by the pharmacy website, serving as a roadmap for understanding how different users interact with the application.
# Activity Diagrams:
 Order Product Activity              
          |
      
              Start: User selects             
                 product to order              
          |
         V
             Select Product Activity           
         |
         V
        Add Product to Shopping Cart          
              Activity                       
          |
         V
        View Shopping Cart and Proceed          
             to Checkout Activity              
          |
         V
          Checkout and Payment               
               Activity                       
          |
         V
          Confirm Order and Receive             
             Order Confirmation     
# State Diagrams:
  +---------------------------------------------+
  |            User Authentication             |
  +---------------------------------------------+
         |
         V
  +---------------------------------------------+
  |              Start: User is logged out      |
  |                                             |
  |              +------------------+           |
  |              |                  |           |
  +------------->|    Logged Out    |<----------+
                 |                  |
                 +--------+---------+
                          |
                          V
                 +--------+---------+
                 |                  |
                 |   Authenticating  |
                 |                  |
                 +--------+---------+
                          |
                          V
                 +--------+---------+
                 |                  |
                 |   Authenticated  |
                 |                  |
                 +--------+---------+
-> Use Case Diagram: To give a clear picture of all the features available on the pharmacy website, we built a use case diagram that shows the different actions that different users can take.
Activity Diagrams: We created an activity diagram that shows the flow of the steps involved in placing an order for a product on the website.
States Diagrams: To show how users move between the logged-out, authenticating, and authenticated states, we created a state diagram that represents the various authentication states.
