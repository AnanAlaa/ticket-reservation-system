#include <iostream>
#include <string>
#include <conio.h>
using namespace std;

string enterPassword() {
    string password = "";
    char ch;

    while (true) {
        ch = _getch();
        if (ch == 13) {
            break;
        }
        else if (ch == 8) {
            if (!password.empty()) {
                password.pop_back();
                cout << "\b \b";
            }
        }
        else {
            password += ch;
            cout << '*';
        }
    }
    cout << endl;
    return password;
}


class Admin {
private:
    string username;
    string password;

public:
    void registerAdmin() {
        cout << "Register Admin Username: ";
        cin.ignore();
        getline(cin, username);

        cout << "Register Password: ";
        password = enterPassword();
    }

    bool login() {
        string uname, pass;
        int attempts = 0;

        while (attempts < 3) {
            cout << "Enter Admin Username: ";
            cin.ignore();
            getline(cin, uname);

            cout << "Enter Password: ";
            pass = enterPassword();

            if (uname == username && pass == password) {
                cout << "Login Successful!\n";
                return true;
            }
            else {
                cout << "Invalid credentials.\n";
                attempts++;
            }
        }

        cout << "Too many failed attempts. Exiting login...\n";
        return false;
    }


    void displayAdmin() {
        cout << "Admin Username: " << username << endl;
    }
};

class User {
private:
    int id;
    string name;
    int age;
    string phone;
    string email;
    string username;
    string password;

public:
    User* next;
    User() {
        next = nullptr;
    }
    void registerUser() {
        cout << "Enter User ID: ";
        cin >> id;
        cin.ignore();

        cout << "Enter Name: ";
        getline(cin, name);

        cout << "Enter Age: ";
        cin >> age;
        cin.ignore();

        cout << "Enter Phone: ";
        getline(cin, phone);

        cout << "Enter Email: ";
        getline(cin, email);

        cout << "Enter Username: ";
        getline(cin, username);

        cout << "Enter Password: ";
        password = enterPassword();
    }



    void displayUser() {
        cout << "ID: " << id << "\nName: " << name << "\nAge: " << age
            << "\nPhone: " << phone << "\nEmail: " << email
            << "\nUsername: " << username << endl;
    }
    int getId() { return id; }
    string getName() { return name; }
    string getUsername() { return username; }
    string getPassword() { return password; }
};

class Employee {
private:
    int id;
    string name;
    int age;
    string phone;
    string username;
    string password;

public:
    Employee* next;
    Employee() {
        next = nullptr;
    }
    void registerEmployee() {
        cout << "Enter Employee ID: ";
        cin >> id;
        cin.ignore();

        cout << "Enter Name: ";
        getline(cin, name);

        cout << "Enter Age: ";
        cin >> age;
        cin.ignore();

        cout << "Enter Phone: ";
        getline(cin, phone);

        cout << "Enter Username: ";
        getline(cin, username);

        cout << "Enter Password: ";
        password = enterPassword();
    }

    bool login() {
        string uname, pass;
        int attempts = 0;

        while (attempts < 3) {
            cout << "Enter Username: ";
            cin.ignore();
            getline(cin, uname);

            cout << "Enter Password: ";
            pass = enterPassword();

            if (uname == username && pass == password) {
                cout << "Login Successful!\n";
                return true;
            }
            else {
                cout << "Invalid credentials.\n";
                attempts++;
            }
        }

        cout << "Too many failed attempts. Exiting program...\n";
        return false;
    }


    void displayEmployee() {
        cout << "ID: " << id << "\nName: " << name << "\nAge: " << age
            << "\nPhone: " << phone << "\nUsername: " << username << endl;
    }

    int getId() {
        return id;
    }
};

class Event {
private:
    int id;
    string name;
    string place;
    float price;
    string date;
    string time;
    int availableTickets;
    string category;

public:
    Event* next;
    Event() {
        next = nullptr;
    }
    void createEvent() {
        cout << "Enter Event ID: ";
        cin >> id;
        cin.ignore();

        cout << "Enter Event Name: ";
        getline(cin, name);

        cout << "Enter Place: ";
        getline(cin, place);

        cout << "Enter Price: ";
        cin >> price;
        cin.ignore();

        cout << "Enter Date: ";
        getline(cin, date);

        cout << "Enter Time: ";
        getline(cin, time);

        cout << "Enter Available Tickets: ";
        cin >> availableTickets;
        cin.ignore();

        cout << "Enter Category: ";
        getline(cin, category);
    }

    void displayEvent() {
        cout << "ID: " << id << "\nName: " << name << "\nPlace: " << place
            << "\nPrice: " << price << "\nDate: " << date << "\nTime: " << time
            << "\nTickets Available: " << availableTickets
            << "\nCategory: " << category << endl;
    }
    void editEvent() {
        cout << "Enter new name: ";
        getline(cin, name);

        cout << "Enter new place: ";
        getline(cin, place);

        cout << "Enter new price: ";
        cin >> price;
        cin.ignore();

        cout << "Enter new date: ";
        getline(cin, date);

        cout << "Enter new time: ";
        getline(cin, time);

        cout << "Enter new available tickets: ";
        cin >> availableTickets;
        cin.ignore();

        cout << "Enter new category: ";
        getline(cin, category);
    }


    int getId() {
        return id;
    }

    string getCategory() {
        return category;
    }

    int getAvailableTickets() {
        return availableTickets;
    }
    string getName() {
        return name;
    }
    string getDate() {
        return date;
    }

};

class Request {
private:
    int userId;
    int eventId;
    string status;
    int numTickets;



public:
    Request* next;
    Request() {
        next = nullptr;
    }
    void createRequest(int uId, int eId, int tickets, string stat) {
        userId = uId;
        eventId = eId;
        numTickets = tickets;
        status = stat;
    }
    void displayRequest() {
        cout << "User ID: " << userId << endl;
        cout << "Event ID: " << eventId << endl;
        cout << "Tickets: " << numTickets << endl;
        cout << "Status: " << status << endl;
    }
    int getUserId() {
        return userId;
    }
};

Employee* employeeHead = nullptr;
Event* eventsHead = nullptr;
User* userHead = nullptr;
Request* requestHead = nullptr;


void manageEvents() {
    int choice;
    do {
        cout << "\n--- Event Management ---\n";
        cout << "1. Add Event\n";
        cout << "2. Update Event\n";
        cout << "3. Delete Event\n";
        cout << "4. List All Events\n";
        cout << "5. Filter by Category\n";
        cout << "6. Filter by Availability\n";
        cout << "7. Back to Admin Menu\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
        case 1: {
            Event* NewEvent = new Event();
            NewEvent->createEvent();

            if (eventsHead == nullptr) {
                eventsHead = NewEvent;
            }
            else {
                Event* temp = eventsHead;
                while (temp->next != nullptr) {
                    temp = temp->next;
                }
                temp->next = NewEvent;
            }

            cout << "Event added successfully" << endl;
            break;
        }

        case 2: {
            if (eventsHead == nullptr) {
                cout << "No event to update" << endl;
                break;
            }
            int id;
            cout << "Enter Event ID to update: ";
            cin >> id;
            cin.ignore();
            Event* temp = eventsHead;
            while (temp != nullptr) {
                if (temp->getId() == id) {
                    cout << "Event current information" << endl;
                    temp->displayEvent();
                    cout << "Enter new event information " << endl;
                    temp->editEvent();
                    return;
                }
                temp = temp->next;
            }
            cout << "Event with this ID not found" << endl;

            break;
        }

        case 3: {
            if (eventsHead == nullptr) {
                cout << "No event to delete" << endl;
                return;
            }
            int id;
            cout << "Enter Event ID to delete: ";
            cin >> id;
            Event* current = eventsHead;
            Event* previous = nullptr;
            while (current != nullptr && current->getId() != id) {
                previous = current;
                current = current->next;
            }
            if (current == nullptr) {
                cout << "Event not found" << endl;
                return;
            }
            if (previous == nullptr) {
                eventsHead = current->next;
            }
            else {
                previous->next = current->next;
            }
            delete current;
            cout << "Event deleted " << endl;
            break;
        }

        case 4: {
            if (eventsHead == nullptr) {
                cout << " No events to show" << endl;
            }
            else {
                Event* temp = eventsHead;
                while (temp != nullptr) {
                    temp->displayEvent();
                    temp = temp->next;
                }
            }
            break;
        }
        case 5: {
            string cat;
            cout << "Enter category to filter: ";
            cin.ignore();
            getline(cin, cat);
            Event* temp = eventsHead;
            while (temp != nullptr) {
                if (temp->getCategory() == cat) {
                    temp->displayEvent();
                }
                temp = temp->next;
            }
            break;
        }

        case 6: {
            Event* temp = eventsHead;
            while (temp != nullptr) {
                if (temp->getAvailableTickets() > 0) {
                    temp->displayEvent();
                }
                temp = temp->next;
            }
            break;
        }
        case 7:
            cout << "Returning to Admin Menu...\n";
            break;

        default:
            cout << "Invalid choice.\n";
        }
    } while (choice != 7);
}
void searchEvents() {
    Event* temp = eventsHead;

    if (eventsHead == nullptr) {
        cout << "No events available.\n";
        return;
    }

    int choice;
    cout << "\nSearch Events by:\n";
    cout << "1. Name\n";
    cout << "2. Category\n";
    cout << "3. Date\n";
    cout << "Enter your choice: ";
    cin >> choice;
    cin.ignore();

    string input;
    bool found = false;

    if (choice == 1) {
        cout << "Enter event name: ";
        getline(cin, input);
        while (temp != nullptr) {
            if (temp->getName() == input) {
                temp->displayEvent();
                found = true;
            }
            temp = temp->next;
        }
    }

    else if (choice == 2) {
        cout << "Enter category: ";
        getline(cin, input);

        while (temp != nullptr) {
            if (temp->getCategory() == input) {
                temp->displayEvent();
                found = true;
            }
            temp = temp->next;
        }
    }

    else if (choice == 3) {
        cout << "Enter date (e.g., 2024-07-01): ";
        getline(cin, input);

        while (temp != nullptr) {
            if (temp->getDate() == input) {
                temp->displayEvent();
                found = true;
            }
            temp = temp->next;
        }
    }

    else {
        cout << "Invalid choice.\n";
        return;
    }

    if (!found) {
        cout << "No matching events found.\n";
    }
}
void listEvents() {
    if (eventsHead == nullptr) {
        cout << " No events to show" << endl;
    }
    else {
        Event* temp = eventsHead;
        while (temp != nullptr) {
            temp->displayEvent();
            temp = temp->next;
        }
    }
}
//user
void searchUser() {
    if (userHead == nullptr) {
        cout << "No users in the system.\n";
        return;
    }

    int choice;
    cout << "\nSearch User by:\n";
    cout << "1. ID\n";
    cout << "2. Name\n";
    cout << "3. Username\n";
    cout << "Enter your choice: ";
    cin >> choice;
    cin.ignore();

    bool found = false;

    if (choice == 1) {
        int id;
        cout << "Enter User ID: ";
        cin >> id;
        User* temp = userHead;
        while (temp != nullptr) {
            if (temp->getId() == id) {
                temp->displayUser();
                found = true;
            }
            temp = temp->next;
        }
    }

    else if (choice == 2) {
        string inputName;
        cout << "Enter User Name: ";
        getline(cin, inputName);
        User* temp = userHead;
        while (temp != nullptr) {
            if (temp->getName() == inputName) {
                temp->displayUser();
                found = true;
            }
            temp = temp->next;
        }
    }

    else if (choice == 3) {
        string inputUsername;
        cout << "Enter Username: ";
        getline(cin, inputUsername);
        User* temp = userHead;
        while (temp != nullptr) {
            if (temp->getUsername() == inputUsername) {
                temp->displayUser();
                found = true;
            }
            temp = temp->next;
        }
    }

    else {
        cout << "Invalid choice.\n";
        return;
    }

    if (!found) {
        cout << "User not found.\n";
    }
}
void addUser() {
    User* newUser = new User();
    newUser->registerUser();

    if (userHead == nullptr) {
        userHead = newUser;
    }
    else {
        User* temp = userHead;
        while (temp->next != nullptr)
            temp = temp->next;
        temp->next = newUser;
    }

    cout << "User registered successfully.\n";
}
void viewAllUsers() {
    if (userHead == nullptr) {
        cout << "No users to show.\n";
        return;
    }

    User* temp = userHead;
    while (temp != nullptr) {
        temp->displayUser();
        temp = temp->next;
    }
}
void editUser() {
    if (userHead == nullptr) {
        cout << "No users to edit.\n";
        return;
    }

    int searchID;
    cout << "Enter User ID to edit: ";
    cin >> searchID;
    cin.ignore();

    User* temp = userHead;
    while (temp != nullptr) {
        if (temp->getId() == searchID) {
            cout << "Enter new user data:\n";
            temp->registerUser();
            cout << "User updated.\n";
            return;
        }
        temp = temp->next;
    }

    cout << "User not found.\n";
}
void deleteUser() {
    if (userHead == nullptr) {
        cout << "No users to delete.\n";
        return;
    }

    int searchID;
    cout << "Enter User ID to delete: ";
    cin >> searchID;

    User* current = userHead;
    User* previous = nullptr;

    while (current != nullptr && current->getId() != searchID) {
        previous = current;
        current = current->next;
    }

    if (current == nullptr) {
        cout << "User not found.\n";
        return;
    }

    if (previous == nullptr) {
        userHead = current->next;
    }
    else {
        previous->next = current->next;
    }

    delete current;
    cout << "User deleted successfully.\n";
}
//requests
void viewRequests() {
    if (requestHead == nullptr) {
        cout << "No requests submitted yet.\n";
        return;
    }

    cout << "\n--- User Requests ---\n";
    Request* temp = requestHead;
    int i = 1;
    while (temp != nullptr) {

        cout << "Request #" << i << ":\n";
        temp->displayRequest();
        cout << "----------------------\n";
        temp = temp->next;
        i++;
    }
}
void bookTicket(int userId) {
    if (eventsHead == nullptr) {
        cout << "No events available.\n";
        return;
    }

    cout << "\n--- Available Events ---\n";
    Event* temp = eventsHead;
    int count = 1;
    while (temp != nullptr) {
        cout << "\nEvent #" << count << ":\n";
        temp->displayEvent();
        temp = temp->next;
        count++;
    }

    int eventId, tickets;
    cout << "Enter Event ID to book: ";
    cin >> eventId;
    cout << "Enter number of tickets: ";
    cin >> tickets;

    Event* selected = eventsHead;
    while (selected != nullptr && selected->getId() != eventId)
        selected = selected->next;

    if (selected == nullptr) {
        cout << "Event not found.\n";
        return;
    }

    Request* newRequest = new Request();
    newRequest->createRequest(userId, eventId, tickets, "Waiting");

    // Add to request list
    if (requestHead == nullptr) {
        requestHead = newRequest;
    }
    else {
        Request* tempReq = requestHead;
        while (tempReq->next != nullptr)
            tempReq = tempReq->next;
        tempReq->next = newRequest;
    }

    cout << "Ticket request sent successfully!\n";
}

void viewMyRequests(int userId) {
    Request* temp = requestHead;
    if (requestHead == nullptr) {
        cout << "No requests to show" << endl;
        return;
    } bool found = false;
    while (temp != nullptr) {
        if (temp->getUserId() == userId) {
            temp->displayRequest();
            found = true;
        }
        temp = temp->next;
    }
    if (!found) {
        cout << "No booking requests found.\n";
    }
}

//menus
void adminMenu(Admin& admin) {
    int choice;
    do {
        cout << "\n--- Admin Menu ---\n";
        cout << "1. Register New Employee\n";
        cout << "2. Update Employee\n";
        cout << "3. Delete Employee\n";
        cout << "4. List All Employees\n";
        cout << "5. Manage Events\n";
        cout << "6. Display Admin Info\n";
        cout << "7. Logout\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
        case 1: {
            Employee* newemp = new Employee();
            newemp->registerEmployee();
            if (employeeHead == nullptr) {
                employeeHead = newemp;
            }
            else {
                Employee* temp = employeeHead;
                while (temp->next != nullptr) {
                    temp = temp->next;

                }
                temp->next = newemp;
            }
            cout << "Employee added " << endl;
            break;
        }
        case 2: {
            if (employeeHead == nullptr) {
                cout << "No employees to update" << endl;
                return;
            }
            int id;
            cout << "Enter Employee ID to update: ";
            cin >> id;
            cin.ignore();
            Employee* temp = employeeHead;
            while (temp != nullptr) {
                if (temp->getId() == id) {
                    cout << "Enter new data" << endl;
                    temp->registerEmployee();
                    cout << "Employee updated" << endl;
                    return;
                }temp = temp->next;
            }cout << "Employee not found" << endl;
            break;
        }

        case 3: {
            if (employeeHead == nullptr) {
                cout << "No employees to delete" << endl;
                return;
            }
            int id;
            cout << "Enter Employee ID to delete: ";
            cin >> id;
            cin.ignore();
            Employee* current = employeeHead;
            Employee* previous = nullptr;
            while (current != nullptr && current->getId() != id) {
                previous = current;
                current = current->next;
            }
            if (current == nullptr) {
                cout << "Employee not found" << endl;
                return;
            }
            if (previous == nullptr) {
                employeeHead = current->next;
            }
            else {
                previous->next = current->next;
            }
            delete current;
            cout << "Employee deleted " << endl;
            break;
        }

        case 4: {
            if (employeeHead == nullptr) {
                cout << "No employees to show" << endl;
                return;
            }
            Employee* temp = employeeHead;
            while (temp != nullptr) {
                temp->displayEmployee();
                temp = temp->next;
            }
        }

              break;

        case 5:
            manageEvents();
            break;

        case 6:
            admin.displayAdmin();
            break;

        case 7:
            cout << "Logging out...\n";
            break;

        default:
            cout << "Invalid choice.\n";
        }
    } while (choice != 7);
}
void employeeMenu(Employee& employee) {
    int choice;
    do {
        cout << "\n--- Employee Panel ---\n";
        cout << "1. Search User\n";
        cout << "2. Search Event\n";
        cout << "3. View All Requests\n";
        cout << "4. add user\n";
        cout << "5. view all users\n";
        cout << "6.edit user\n";
        cout << "7.delete user\n";
        cout << "0. Logout\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
        case 1:
            searchUser();
            break;
        case 2:
            searchEvents();
            break;
        case 3:
            viewRequests();
            break;
        case 4:
            addUser();
            break;
        case 5:
            viewAllUsers();
            break;
        case 6:
            editUser();
            break;
        case 7:
            deleteUser();
            break;
        case 0:
            cout << "Logging out...\n";
            break;
        default: cout << "Invalid choice. Try again.\n";
        }
    } while (choice != 0);
}
void userMenu(User& user) {
    int choice;
    do {
        cout << "\n--- User Panel ---\n";
        cout << "1. View All Events\n";
        cout << "2. Book Ticket\n";
        cout << "3. View My Requests\n";
        cout << "0. Logout\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
        case 1:
            listEvents();
            break;
        case 2:
            bookTicket(user.getId());
            break;
        case 3:
            viewMyRequests(user.getId());
            break;
        case 0:
            cout << "Logging out...\n";
            break;
        default:
            cout << "Invalid choice. Try again.\n";
        }
    } while (choice != 0);
}
User* loginUser() {
    string uname, pass;
    int attempts = 0;
    while (attempts < 3) {
        cout << "Enter Username: ";
        cin.ignore();
        getline(cin, uname);
        cout << "Enter Password: ";
        pass = enterPassword();
        User* temp = userHead;
        while (temp) {
            if (temp->getUsername() == uname && temp->getPassword() == pass) {
                cout << "Login Successful!\n";
                return temp;
            }
            temp = temp->next;
        }
        cout << "Invalid credentials.\n";
        attempts++;
    }
    cout << "Too many failed attempts. Exiting...\n";
    return nullptr;
}

int main() {
    Admin admin;
    User user;
    Employee emp;

    int choice;

    do {
        cout << "\n  Ticket Reservation System  \n";
        cout << "1. Register Admin\n2. Register User\n3. Admin Login\n4. User Login\n5. Registrer employee \n6. employee login\n0. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
        case 1:
            admin.registerAdmin();
            break;
        case 2:
            user.registerUser();
            break;
        case 3:
            if (admin.login()) {
                adminMenu(admin);
            }
            break;
        case 4:
        {
            User* loggedUser = loginUser();
            if (loggedUser) {
                userMenu(*loggedUser);
            }

            break;
        }
        case 5:
            emp.registerEmployee();
            break;
        case 6:
            if (emp.login()) {
                employeeMenu(emp);
            }
            break;
        case 0:
            cout << "Exiting..." << endl;
            break;
        default:
            cout << "Invalid choice. Try again." << endl;
        }
    } while (choice != 0);

    return 0;
}
