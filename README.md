#include <iostream>
using namespace std;

// Structure to store customer information
struct Customer {
    char customer_Name[50];
    char customer_Phone[20];
    char customer_ID[20];
    char assigned_producer[50];
};

// Structure to store producer information
struct Producer {
    char producer_Name[50];
    char producer_Phone[20];
    int years_Serviced;
    char producer_ID[20];
};

// Create fixed-size arrays to work as stacks
Customer customerStack[100]; // Stack for customers
int customerTop = -1;        // Top pointer for customer stack

Producer producerStack[100]; // Stack for producers
int producerTop = -1;        // Top pointer for producer stack

// Function to add a new customer to the stack
void add_customer() {
    if (customerTop < 99) { // Check if there's space
        customerTop++; // Move top up
        cout << "Enter new customer details\n";
        cout << "Name: ";
        cin >> customerStack[customerTop].customer_Name;
        cout << "Phone: ";
        cin >> customerStack[customerTop].customer_Phone;
        cout << "ID: ";
        cin >> customerStack[customerTop].customer_ID;
        cout << "Customer added successfully.\n";
    } else {
        cout << "Customer stack is full.\n"; // No more space
    }
}

// Function to add a new producer to the stack
void add_producer() {
    if (producerTop < 99) { // Check if there's space
        producerTop++; // Move top up
        cout << "Enter new producer details\n";
        cout << "Name: ";
        cin >> producerStack[producerTop].producer_Name;
        cout << "Phone: ";
        cin >> producerStack[producerTop].producer_Phone;
        cout << "Years served: ";
        cin >> producerStack[producerTop].years_Serviced;
        cout << "Producer ID: ";
        cin >> producerStack[producerTop].producer_ID;
        cout << "Producer added successfully.\n";
    } else {
        cout << "Producer stack is full.\n"; // No more space
    }
}

// Function to display all customers from top to bottom
void display_customers() {
    if (customerTop == -1) { // If stack is empty
        cout << "No customers to display.\n";
        return;
    }
    for (int i = customerTop; i >= 0; i--) { // From top to bottom
        cout << "Customer " << customerTop - i + 1 << " Details:\n";
        cout << "Name: " << customerStack[i].customer_Name << "\n";
        cout << "Phone: " << customerStack[i].customer_Phone << "\n";
        cout << "ID: " << customerStack[i].customer_ID << "\n\n";
    }
}

// Function to display all producers from top to bottom
void display_producers() {
    if (producerTop == -1) { // If stack is empty
        cout << "No producers to display.\n";
        return;
    }
    for (int i = producerTop; i >= 0; i--) { // From top to bottom
        cout << "Producer " << producerTop - i + 1 << " Details:\n";
        cout << "Name: " << producerStack[i].producer_Name << "\n";
        cout << "Phone: " << producerStack[i].producer_Phone << "\n";
        cout << "Years Served: " << producerStack[i].years_Serviced << "\n";
        cout << "ID: " << producerStack[i].producer_ID << "\n\n";
    }
}

int main() {
    int choice;
    // Menu loop to interact with user
    do {
        cout << "\n1. Add Customer\n2. Add Producer\n3. Display Customers\n4. Display Producers\n0. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;
        switch (choice) {
            case 1: add_customer(); break;        // Add customer
            case 2: add_producer(); break;        // Add producer
            case 3: display_customers(); break;   // Show all customers
            case 4: display_producers(); break;   // Show all producers
            case 0: cout << "Exiting...\n"; break; // Exit program
            default: cout << "Invalid choice.\n";  // Invalid input
        }
    } while (choice != 0); // Repeat until exit

    return 0;
}
