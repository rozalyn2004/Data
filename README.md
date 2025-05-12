#include <iostream>
#include <string>
#include <queue>
using namespace std;

// Forward declaration of Producer
struct Producer;

// Customer structure with pointer to assigned producer
struct Customer {
    string name;
    string phone;
    string id;
    Producer* assigned_producer_ptr; // Link to assigned producer
    Customer* prev;
    Customer* next;
};

// Producer structure
struct Producer {
    string name;
    string phone;
    int years_serviced;
    string id;
    Producer* prev;
    Producer* next;
};

// Head pointers for linked lists
Customer* customerHead = NULL;
Producer* producerHead = NULL;

// Queue for waiting customers
queue<Customer*> waitingQueue;

// Add a new customer and link them to a producer by ID
void addCustomer() {
    Customer* C = new Customer;
    cout << "Enter Customer Name: ";
    cin.ignore();
    getline(cin, C->name);
    cout << "Enter Phone: ";
    getline(cin, C->phone);
    cout << "Enter Customer ID: ";
    getline(cin, C->id);

    string producerID;
    cout << "Enter Assigned Producer ID: ";
    getline(cin, producerID);

    // Search for the producer by ID
    Producer* assigned = producerHead;
    while (assigned != NULL && assigned->id != producerID) {
        assigned = assigned->next;
    }

    if (assigned == NULL) {
        cout << "Producer not found. Customer will not be assigned.\n";
        C->assigned_producer_ptr = NULL;
    } else {
       C->assigned_producer_ptr = assigned;
    }

    C->next = customerHead;
    C->prev = NULL;
    if (customerHead != NULL)
        customerHead->prev = C;
    customerHead = C;

    cout << "Customer added successfully!\n";
}

// Search for a customer by ID
void searchCustomer(string id) {
    Customer* temp = customerHead;
    while (temp != NULL) {
        if (temp->id == id) {
            cout << "Customer found: " << temp->name << ", Phone: " << temp->phone;
            if (temp->assigned_producer_ptr)
                cout << ", Assigned Producer: " << temp->assigned_producer_ptr->name;
            else
                cout << ", Assigned Producer: [None]";
            cout << endl;
            return;
        }
        temp = temp->next;
    }
    cout << "Customer not found.\n";
}

// Edit customer information by ID
void editCustomer(string id) {
    Customer* temp = customerHead;
    while (temp != NULL) {
        if (temp->id == id) {
            cout << "Enter new name: ";
            cin.ignore();
            getline(cin, temp->name);
            cout << "Enter new phone: ";
            getline(cin, temp->phone);
            string newProducerID;
            cout << "Enter new Assigned Producer ID: ";
            getline(cin, newProducerID);

            Producer* newAssigned = producerHead;
            while (newAssigned != NULL && newAssigned->id != newProducerID) {
                newAssigned = newAssigned->next;
            }

            if (newAssigned == NULL) {
                cout << "Producer not found. Assignment unchanged.\n";
            } else {
                temp->assigned_producer_ptr = newAssigned;
                cout << "Producer reassigned.\n";
            }

            cout << "Customer updated.\n";
            return;
        }
        temp = temp->next;
    }
    cout << "Customer not found.\n";
}

// Delete customer by ID
void deleteCustomer(string id) {
    Customer* temp = customerHead;
    while (temp != NULL) {
        if (temp->id == id) {
            if (temp->prev)
                temp->prev->next = temp->next;
            else
                customerHead = temp->next;
            if (temp->next)
                temp->next->prev = temp->prev;
            delete temp;
            cout << "Customer deleted.\n";
            return;
        }
        temp = temp->next;
    }
    cout << "Customer not found.\n";
}

// Add new producer
void addProducer() {
    Producer* P = new Producer;
    cout << "Enter Producer Name: ";
    cin.

ignore();
    getline(cin, P->name);
    cout << "Enter Phone: ";
    getline(cin, P->phone);
    cout << "Enter Years Serviced: ";
    cin >> P->years_serviced;
    cin.ignore();
    cout << "Enter Producer ID: ";
    getline(cin, P->id);

    P->next = producerHead;
    P->prev = NULL;
    if (producerHead != NULL)
        producerHead->prev = P;
    producerHead = P;

    cout << "Producer added successfully!\n";
}

// Search for producer by ID
void searchProducer(string id) {
    Producer* temp = producerHead;
    while (temp != NULL) {
        if (temp->id == id) {
            cout << "Producer found: " << temp->name << ", Phone: " << temp->phone
                 << ", Years Serviced: " << temp->years_serviced << endl;
            return;
        }
        temp = temp->next;
    }
    cout << "Producer not found.\n";
}

// Edit producer information
void editProducer(string id) {
    Producer* temp = producerHead;
    while (temp != NULL) {
        if (temp->id == id) {
            cout << "Enter new name: ";
            cin.ignore();
            getline(cin, temp->name);
            cout << "Enter new phone: ";
            getline(cin, temp->phone);
            cout << "Enter new years serviced: ";
            cin >> temp->years_serviced;
            cout << "Producer updated.\n";
            return;
        }
        temp = temp->next;
    }
    cout << "Producer not found.\n";
}

// Delete producer by ID
void deleteProducer(string id) {
    Producer* temp = producerHead;
    while (temp != NULL) {
        if (temp->id == id) {
            if (temp->prev)
                temp->prev->next = temp->next;
            else
                producerHead = temp->next;
            if (temp->next)
                temp->next->prev = temp->prev;
            delete temp;
            cout << "Producer deleted.\n";
            return;
        }
        temp = temp->next;
    }
    cout << "Producer not found.\n";
}

// Display all customers
void displayAllCustomers() {
    Customer* temp = customerHead;
    if (!temp) {
        cout << "No customers found.\n";
        return;
    }
    cout << "\nAll Customers:\n";
    while (temp != NULL) {
        cout << "Name: " << temp->name << ", Phone: " << temp->phone
             << ", ID: " << temp->id << ", Assigned Producer: ";
        if (temp->assigned_producer_ptr)
            cout << temp->assigned_producer_ptr->name;
        else
            cout << "[None]";
        cout << endl;
        temp = temp->next;
    }
}

// Display all producers
void displayAllProducers() {
    Producer* temp = producerHead;
    if (!temp) {
        cout << "No producers found.\n";
        return;
    }
    cout << "\nAll Producers:\n";
    while (temp != NULL) {
        cout << "Name: " << temp->name << ", Phone: " << temp->phone
             << ", Years Serviced: " << temp->years_serviced
             << ", ID: " << temp->id << endl;
        temp = temp->next;
    }
}

// Add customer to waiting queue
void enqueueCustomer() {
    Customer* newCustomer = new Customer;
    cout << "Enter Customer Name: ";
    cin.ignore();
    getline(cin, newCustomer->name);
    cout << "Enter Phone: ";
    getline(cin, newCustomer->phone);
    cout << "Enter Customer ID: ";
    getline(cin, newCustomer->id);

    string producerID;
    cout << "Enter Assigned Producer ID: ";
    getline(cin, producerID);

    Producer* assigned = producerHead;
    while (assigned != NULL && assigned->id != producerID) {
        assigned = assigned->next;
    }

    if (assigned == NULL) {
        cout << "Producer not found. Customer will not be assigned.\n";
        newCustomer->assigned_producer_ptr = NULL;
    } else {
        newCustomer->assigned_producer_ptr = assigned;
    }

    waitingQueue.push(newCustomer);
    cout << "Customer added to waiting queue.\n";
}

// Serve customer from queue and move to main list
void serveCustomerFromQueue() {
    if (waitingQueue.empty()) {
        cout << "No customers in queue.\n";
        return;
    }

    Customer* front = waitingQueue.front();
    waitingQueue.pop();

    front->next = customerHead;
    front->prev = NULL;
    if (customerHead != NULL)
        customerHead->prev = front;
    customerHead = front;

    cout << "Customer moved from queue to main list.\n";
}

// Main menu
int main() {
    int choice;
    string id;

    do {
        cout << "\nMenu:\n";
        cout << "1. Add Customer\n";
        cout << "2. Search Customer\n";
        cout << "3. Edit Customer\n";
        cout << "4. Delete Customer\n";
        cout << "5. Add Producer\n";
        cout << "6. Search Producer\n";
        cout << "7. Edit Producer\n";
        cout << "8. Delete Producer\n";
        cout << "9. Display All Customers\n";
        cout << "10. Display All Producers\n";
        cout << "11. Add Customer to Waiting Queue\n";
        cout << "12. Serve Customer from Queue\n";
        cout << "0. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
            case 1: 
                addCustomer(); 
                break;
            case 2: 
                cout << "Enter Customer ID: "; 
                cin.ignore(); 
                getline(cin, id); 
                searchCustomer(id); 
                break;
            case 3: 
                cout << "Enter Customer ID: "; 
                cin.ignore(); 
                getline(cin, id); 
                editCustomer(id); 
                break;
            case 4: 
                cout << "Enter Customer ID: "; 
                cin.ignore(); 
                getline(cin, id); 
                deleteCustomer(id); 
                break;
            case 5: 
                addProducer(); 
                break;
            case 6: 
                cout << "Enter Producer ID: "; 
                cin.ignore(); 
                getline(cin, id); 
                searchProducer(id); 
                break;
            case 7: 
                cout << "Enter Producer ID: "; 
                cin.ignore(); 
                getline(cin, id); 
                editProducer(id); 
                break;
            case 8: 
                cout << "Enter Producer ID: "; 
                cin.ignore(); 
                getline(cin, id); 
                deleteProducer(id); 
                break;
            case 9: 
                displayAllCustomers(); 
                break;
            case 10: 
                displayAllProducers(); 
                break;
            case 11: 
                enqueueCustomer(); 
                break;
            case 12: 
                serveCustomerFromQueue(); 
                break;
            case 0: 
                cout << "Exiting program...\n";
                break;
            default: 
                cout << "Invalid choice. Try again.\n";
        }
    } while (choice != 0);

    return 0;
}
