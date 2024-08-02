# WEEK-4
#include <iostream>
#include <queue>

using namespace std;

class Patient {
public:
    int age;
    
    Patient(int age) : age(age) {}
};

// Comparator for the priority queue to sort patients based on their age
class Compare {
public:
    bool operator()(const Patient& p1, const Patient& p2) {
        // Define priority based on age brackets
        if (p1.age >= 60 && p2.age >= 60) return p1.age < p2.age;
        if (p1.age >= 60) return false;
        if (p2.age >= 60) return true;
        
        if (p1.age > 50 && p1.age < 60 && p2.age > 50 && p2.age < 60) return p1.age < p2.age;
        if (p1.age > 50 && p1.age < 60) return false;
        if (p2.age > 50 && p2.age < 60) return true;
        
        if (p1.age > 40 && p1.age <= 50 && p2.age > 40 && p2.age <= 50) return p1.age < p2.age;
        if (p1.age > 40 && p1.age <= 50) return false;
        if (p2.age > 40 && p2.age <= 50) return true;
        
        if (p1.age > 30 && p1.age <= 40 && p2.age > 30 && p2.age <= 40) return p1.age < p2.age;
        if (p1.age > 30 && p1.age <= 40) return false;
        if (p2.age > 30 && p2.age <= 40) return true;
        
        return p1.age < p2.age;
    }
};

class PriorityQueue {
private:
    priority_queue<Patient, deque<Patient>, Compare> pq;

public:
    void addPatient(int age) {
        Patient p(age);
        pq.push(p);
        cout << "Patient with age " << age << " added to the queue." << endl;
    }
    
    void deletePatient() {
        if (!pq.empty()) {
            Patient p = pq.top();
            pq.pop();
            cout << "Patient with age " << p.age << " has been treated and removed from the queue." << endl;
        } else {
            cout << "No patients in the queue." << endl;
        }
    }
    
    void displayPatients() {
        if (pq.empty()) {
            cout << "No patients in the queue." << endl;
            return;
        }
        
        priority_queue<Patient, deque<Patient>, Compare> temp = pq;
        cout << "Patients in the queue (in priority order):" << endl;
        while (!temp.empty()) {
            Patient p = temp.top();
            temp.pop();
            cout << "Age: " << p.age << endl;
        }
    }
};

int main() {
    PriorityQueue pq;
    int choice, age;
    
    while (true) {
        cout << "\nHospital Management System" << endl;
        cout << "1. Add patient" << endl;
        cout << "2. Treat (delete) patient" << endl;
        cout << "3. Display patients" << endl;
        cout << "4. Exit" << endl;
        cout << "Enter your choice: ";
        cin >> choice;
        
        switch (choice) {
            case 1:
                cout << "Enter patient's age: ";
                cin >> age;
                pq.addPatient(age);
                break;
            case 2:
                pq.deletePatient();
                break;
            case 3:
                pq.displayPatients();
                break;
            case 4:
                return 0;
            default:
                cout << "Invalid choice. Please try again." << endl;
        }
    }
    
    return 0;
}
