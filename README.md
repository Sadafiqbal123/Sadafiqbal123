// Online C++ compiler to run C++ program online
// Online C++ compiler to run C++ program online
#include <iostream>
#include <string>
#include <vector>
#include <fstream>
#include <algorithm>

class Student {
public:
    std::string name;
    int roll_number;
    std::string course;
    std::string student_class;
    double GPA;
    std::string email;
};

class StudentDatabase {
private:
    std::vector<Student> students;

public:
    void enter();
    void show();
    void search();
    void update();
    void readFromFile(const std::string& filename);
    void saveToFile(const std::string& filename);
};

void StudentDatabase::enter() {
    int ch = 0;
    std::cout << "How many students do you want to enter data? ";
    std::cin >> ch;

    for (int i = 0; i < ch; i++) {
        Student student;
        std::cout << "\nEnter the Data of student " << i + 1 << std::endl;
        std::cout << "Enter name: ";
        std::cin >> student.name;

        std::cout << "Enter Roll no: ";
        std::cin >> student.roll_number;

        std::cout << "Enter course: ";
        std::cin >> student.course;

        std::cout << "Enter class: ";
        std::cin >> student.student_class;

        std::cout << "Enter GPA: ";
        std::cin >> student.GPA;

        std::cout << "Enter Email: ";
        std::cin >> student.email;

        students.push_back(student);
    }
}

void StudentDatabase::readFromFile(const std::string& filename) {
    std::ifstream fin(filename);
    if (!fin) {
        std::cout << "Error opening file: " << filename << std::endl;
        return;
    }

    while (!fin.eof()) {
        Student student;
        fin >> student.name;
        fin >> student.roll_number;
        fin >> student.course;
        fin >> student.student_class;
        fin >> student.GPA;
        fin >> student.email;

        if (!fin.eof()) {
            students.push_back(student);
        }
    }
    fin.close();
}

void StudentDatabase::show() {
    if (students.empty()) {
        std::cout << "No data is entered" << std::endl;
    } else {
        std::vector<int> displayedRollNumbers;
        int studentCount = 1;

        for (const Student& student : students) {
            if (std::find(displayedRollNumbers.begin(), displayedRollNumbers.end(), student.roll_number) == displayedRollNumbers.end()) {
                std::cout << "\nData of Student " << studentCount << std::endl << std::endl;
                std::cout << "Name: " << student.name << std::endl;
                std::cout << "Roll no: " << student.roll_number << std::endl;
                std::cout << "Course: " << student.course << std::endl;
                std::cout << "Class: " << student.student_class << std::endl;
                std::cout << "GPA: " << student.GPA << std::endl;
                std::cout << "Email: " << student.email << std::endl;

                displayedRollNumbers.push_back(student.roll_number);
                studentCount++;
            }
        }

        if (studentCount == 1) {
            std::cout << "No unique data is entered" << std::endl;
        }
    }
}

void StudentDatabase::search() {
    if (students.empty()) {
        std::cout << "No data is entered" << std::endl;
    } else {
        int rollno;
        std::cout << "Enter the roll no of the student you want to search: ";
        std::cin >> rollno;

        bool found = false;
        for (const Student& student : students) {
            if (rollno == student.roll_number) {
                std::cout << "\nData of Student with Roll no " << rollno << std::endl << std::endl;
                std::cout << "Name: " << student.name << std::endl;
                std::cout << "Roll no: " << student.roll_number << std::endl;
                std::cout << "Course: " << student.course << std::endl;
                std::cout << "Class: " << student.student_class << std::endl;
                std::cout << "GPA: " << student.GPA << std::endl;
                std::cout << "Email: " << student.email << std::endl;
                found = true;
                break;
            }
        }

        if (!found) {
            std::cout << "Student with Roll no " << rollno << " not found." << std::endl;
        }
    }
}

void StudentDatabase::update() {
    if (students.empty()) {
        std::cout << "No data is entered" << std::endl;
    } else {
        int rollno;
        std::cout << "Enter the roll no of the student you want to update: ";
        std::cin >> rollno;

        bool found = false;
        for (Student& student : students) {
            if (rollno == student.roll_number) {
                std::cout << "\nUpdating data of Student with Roll no " << rollno << std::endl << std::endl;

                // Store the original data before updating
                std::string originalName = student.name;
                int originalRollNumber = student.roll_number;
                std::string originalCourse = student.course;
                std::string originalStudentClass = student.student_class;
                double originalGPA = student.GPA;
                std::string originalEmail = student.email;

                // Show previous data
                std::cout << "Previous Data:" << std::endl;
                std::cout << "Name: " << originalName << std::endl;
                std::cout << "Roll no: " << originalRollNumber << std::endl;
                std::cout << "Course: " << originalCourse << std::endl;
                std::cout << "Class: " << originalStudentClass << std::endl;
                std::cout << "GPA: " << originalGPA << std::endl;
                std::cout << "Email: " << originalEmail << std::endl;

                // Enter new data
                std::cout << "Enter new name: ";
                std::cin >> student.name;

                std::cout << "Enter new roll number: ";
                std::cin >> student.roll_number;

                std::cout << "Enter new course: ";
                std::cin >> student.course;

                std::cout << "Enter new class: ";
                std::cin >> student.student_class;

                std::cout << "Enter new GPA: ";
                std::cin >> student.GPA;

                std::cout << "Enter new Email: ";
                std::cin >> student.email;

                found = true;
                break;
            }
        }

        if (!found) {
            std::cout << "Student with Roll no " << rollno << " not found." << std::endl;
        }
    }
}

void StudentDatabase::saveToFile(const std::string& filename) {
    std::ofstream fout(filename);
    if (!fout) {
        std::cout << "Error creating file: " << filename << std::endl;
        return;
    }

    for (const Student& student : students) {
        fout << student.name << " "
             << student.roll_number << " "
             << student.course << " "
             << student.student_class << " "
             << student.GPA << " "
             << student.email << std::endl;
    }

    fout.close();

    std::cout << "Saving data to file." << std::endl;
}

int main() {
    StudentDatabase studentDB;
    studentDB.readFromFile("students.txt");

    // Display data read from the file
    studentDB.show();

    int value;
    while (true) {
        std::cout << "\t\t............................." << std::endl;
        std::cout << "\t\t STUDENT MANAGEMENT SYSTEM" << std::endl;
        std::cout << "\t\t............................." << std::endl;
        std::cout << "\t\t 1.Add new students" << std::endl;
        std::cout << "\t\t 2.Display student" << std::endl;
        std::cout << "\t\t 3.Search student" << std::endl;
        std::cout << "\t\t 4.Update student" << std::endl;
        std::cout << "\t\t 5.Save to file" << std::endl;
        std::cout << "\t\t 6.Exit student" << std::endl;
        std::cout << "\t\tEnter your choice: ";
        std::cin >> value;

        switch (value) {
            case 1:
                studentDB.enter();
                break;

            case 2:
                studentDB.show();
                break;

            case 3:
                studentDB.search();
                break;

            case 4:
                studentDB.update();
                break;

            case 5:
                studentDB.saveToFile("students.txt");
                break;

             case 6:
                std::cout << "Goodbye!" << std::endl;
                exit(0);
                break;

            default:
                std::cout << "Invalid input" << std::endl;
                break;
        }
    }

    return 0;
}
