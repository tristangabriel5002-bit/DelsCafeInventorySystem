Del's Cafe Inventory System

📌 Overview
Del's Cafe Inventory System is a console-based application developed in C that helps manage cafe products, stock levels, and customer orders. 

The system allows users to add, update, delete, search, and sort inventory items, as well as process customer orders and track transaction history. It is designed to demonstrate the practical application of Data Structures and Algorithms (DSA) in a real-world scenario.

📌Purpose
The main goal of this project is to apply fundamental Data Structures and Algorithms concepts learned in CC104 to build a functional and efficient inventory management system.

📌Data Structures Used

**1. Array**
- Used to store the list of products in the inventory
- Allows fast access using index

**2. Linked List**
- Used to store transaction history
- Supports dynamic memory allocation

**3. Stack**
- Used for undo functionality
- Follows LIFO (Last In, First Out)

** 4. Queue**
- Used to manage customer orders
- Follows FIFO (First In, First Out)

---

##  Algorithms Used

### 1. Linear Search
- Used to find products by ID
- Simple and effective for small datasets

### 2. Bubble Sort
- Used to sort inventory items by quantity
- Demonstrates basic sorting logic

### 3. Queue Processing (FIFO)
- Used to process customer orders in correct order

---

##  Features
- Add new products
- View all products
- Update product details
- Delete products
- Search for products
- Sort inventory by quantity
- View transaction history
- Undo last operation
- Add customer orders
- Process customer orders

---

## How to Compile and Run

### Step 1: Install Compiler
Install a C compiler such as:
- MinGW / TDM-GCC / WSL

### Step 2: Compile the Program
Open terminal and run:
```bash
gcc main.c -o inventory
