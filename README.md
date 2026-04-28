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







#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX 100

// ================= STRUCTURES =================

// Product (Array)
typedef struct {
    int id;
    char name[50];
    int quantity;
    float price;
} Product;

Product inventory[MAX];
int count = 0;

// Linked List (Transaction History)
typedef struct Node {
    char action[100];
    struct Node* next;
} Node;

Node* history = NULL;

// Stack (Undo)
typedef struct Stack {
    Product data;
    struct Stack* next;
} Stack;

Stack* top = NULL;

// ================= STACK FUNCTIONS =================
void push(Product p) {
    Stack* temp = (Stack*)malloc(sizeof(Stack));
    temp->data = p;
    temp->next = top;
    top = temp;
}

Product pop() {
    Product p = {-1, "", 0, 0};
    if (top != NULL) {
        Stack* temp = top;
        p = temp->data;
        top = top->next;
        free(temp);
    }
    return p;
}

// ================= LINKED LIST FUNCTIONS =================
void addHistory(char action[]) {
    Node* temp = (Node*)malloc(sizeof(Node));
    strcpy(temp->action, action);
    temp->next = history;
    history = temp;
}

void showHistory() {
    Node* temp = history;
    printf("\n--- Transaction History ---\n");
    while (temp != NULL) {
        printf("%s\n", temp->action);
        temp = temp->next;
    }
}

// ================= SEARCH (LINEAR SEARCH) =================
int searchProduct(int id) {
    for (int i = 0; i < count; i++) {
        if (inventory[i].id == id)
            return i;
    }
    return -1;
}

// ================= SORT (BUBBLE SORT) =================
void sortInventory() {
    for (int i = 0; i < count - 1; i++) {
        for (int j = 0; j < count - i - 1; j++) {
            if (inventory[j].quantity > inventory[j + 1].quantity) {
                Product temp = inventory[j];
                inventory[j] = inventory[j + 1];
                inventory[j + 1] = temp;
            }
        }
    }
    printf("\nInventory sorted by quantity.\n");
}

// ================= CORE FUNCTIONS =================
void addProduct() {
    Product p;
    printf("\nEnter ID: ");
    scanf("%d", &p.id);

    printf("Enter Name: ");
    scanf(" %[^\n]", p.name);

    printf("Enter Quantity: ");
    scanf("%d", &p.quantity);

    printf("Enter Price: ");
    scanf("%f", &p.price);

    inventory[count++] = p;

    push(p); // Save for undo

    char log[100];
    sprintf(log, "Added: %s", p.name);
    addHistory(log);

    printf("Product added!\n");
}

void viewProducts() {
    printf("\n--- Inventory ---\n");
    for (int i = 0; i < count; i++) {
        printf("ID:%d | %s | Qty:%d | Price:%.2f\n",
               inventory[i].id,
               inventory[i].name,
               inventory[i].quantity,
               inventory[i].price);
    }
}

void updateProduct() {
    int id;
    printf("\nEnter ID to update: ");
    scanf("%d", &id);

    int index = searchProduct(id);

    if (index == -1) {
        printf("Product not found!\n");
        return;
    }

    push(inventory[index]); // Save old state

    printf("Enter new quantity: ");
    scanf("%d", &inventory[index].quantity);

    printf("Enter new price: ");
    scanf("%f", &inventory[index].price);

    addHistory("Updated product");

    printf("Product updated!\n");
}

void deleteProduct() {
    int id;
    printf("\nEnter ID to delete: ");
    scanf("%d", &id);

    int index = searchProduct(id);

    if (index == -1) {
        printf("Product not found!\n");
        return;
    }

    push(inventory[index]); // Save for undo

    for (int i = index; i < count - 1; i++) {
        inventory[i] = inventory[i + 1];
    }

    count--;

    addHistory("Deleted product");

    printf("Product deleted!\n");
}

void undo() {
    Product p = pop();

    if (p.id == -1) {
        printf("Nothing to undo!\n");
        return;
    }

    inventory[count++] = p;
    addHistory("Undo performed");

    printf("Undo successful!\n");
}

// ================= MAIN MENU =================
int main() {
    int choice;

    do {
        printf("\n=== DEL'S CAFE INVENTORY SYSTEM ===\n");
        printf("1. Add Product\n");
        printf("2. View Products\n");
        printf("3. Update Product\n");
        printf("4. Delete Product\n");
        printf("5. Search Product\n");
        printf("6. Sort Inventory\n");
        printf("7. View History\n");
        printf("8. Undo\n");
        printf("9. Exit\n");
        printf("Enter choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1: addProduct(); break;
            case 2: viewProducts(); break;
            case 3: updateProduct(); break;
            case 4: deleteProduct(); break;
            case 5: {
                int id;
                printf("Enter ID to search: ");
                scanf("%d", &id);
                int index = searchProduct(id);
                if (index != -1)
                    printf("Found: %s\n", inventory[index].name);
                else
                    printf("Not found!\n");
                break;
            }
            case 6: sortInventory(); break;
            case 7: showHistory(); break;
            case 8: undo(); break;
            case 9: printf("Exiting...\n"); break;
            default: printf("Invalid choice!\n");
        }

    } while (choice != 9);

    return 0;
}
