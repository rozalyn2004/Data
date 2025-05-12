# Electrical Grid System - Data Structures Project

## Project Description
This project simulates an electrical grid customer management system using core data structures. It allows managing customers and producers using a doubly linked list and a queue for waiting customers. Each customer is linked to a producer using pointers.

## Features
- Add, Search, Edit, and Delete Customers
- Add, Search, Edit, and Delete Producers
- Assign customers to producers by ID
- Queue system for waiting customers
- Serve customers from the waiting queue
- Menu-based user interface

## Data Structures Used
- **Doubly Linked List**: For managing both customers and producers
- **Queue (FIFO)**: For handling waiting customers
- **Pointer Linking**: Each customer holds a pointer to the assigned producer

## How to Compile and Run
1. Open the terminal and navigate to the project directory.
2. Compile the program using a C++ compiler:
   ```
   g++ -o grid_system main.cpp
   ```
3. Run the program:
   ```
   ./grid_system
   ```

## Instructor
Dr. Hala Hamdoun

## Course
Data Structures & Algorithms (0921-211) - King Faisal University
