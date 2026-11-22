# course_management_system
Menu-driven Course Registration Management System in C (CS-115, NED)
Here is a complete, copy-ready README file for your GitHub repository. It includes the project introduction, features, compilation instructions, menu options, working, and C concepts.

# Course Registration Management System

## Project Overview:

The **Course Registration Management System** is a menu-driven application developed in the C programming language. It is designed to manage university courses and student registrations.

The system allows users to add, view, search, update, and delete courses and student registrations. It also uses file handling to save records permanently, so data remains available even after closing and reopening the program.

## Technologies and Concepts Used

This project demonstrates the following C programming concepts:

- **Structures:** To store course and student registration information.
- **Arrays:** To store multiple course and registration records.
- **Pointers:** To search and access records.
- **Functions:** To divide the program into smaller,manageable tasks.
- **Loops:** To repeat menu operations and search records.
- **Conditional Statements:** To make decisions based on user input.
- **String Handling:** To process IDs and names.
- **File Handling:** To save and load records using binary files.

## Main Features:

The system provides the following features:


1. **Add New Course:** Add a course with its ID, name, and credit hours.
2. **View Courses:** Display all available courses.
3. **Register Student:** Register a student in an existing course.
4. **View Registrations:** Display students along with their registered courses.
5. **Search Course:** Search for a course using its course ID.
6. **Search Student:** Search for a student using their student ID.
7. **Delete Course:** Delete a course and its related registrations.
8. **Delete Student Registration:** Remove a student's registration from a particular course.
9. **Update Course:** Update the course name or credit hours.
10. **Update Student Name:** Change a student's name in all their registrations.
11. **Exit:** Save all records and close the application.

## How to Compile and Run

### Requirements

- GCC Compiler
- Visual Studio Code or any C compiler
- C programming environment

### Step 1: Compile the Program. 

Open the terminal in the project directory and execute:

```bash
gcc main.c -o course
```

### Step 2: Run the Program

**For Windows:**

```bash
.\course.exe
```

**For Linux:**

```bash
./course
```

## How to Use the Program

After running the executable file, the main menu will appear.

```text
========================================
       COURSE REGISTRATION SYSTEM
========================================

1. Add New Course
2. View Courses
3. Register Student
4. View Registrations
5. Search Course
6. Search Student
7. Delete Course
8. Delete Student Registration
9. Update Course
10. Update Student Name
11. Exit

Enter your choice:
```

Enter the number corresponding to the operation you want to perform.

### Example Usage

**1. Add a Course**

```text
Enter Course ID: CP101
Enter Course Name: Programming Fundamentals
Enter Credit Hours: 3

Course added successfully!
```

**2. Register a Student**

```text
Enter Student ID: 038
Enter Student Name: Abdul Rehman
Enter Course ID: CP101

Student registered successfully!
```

**3. Search for a Student**

```text
Enter Student ID to search: 038

========== STUDENT DETAILS ==========

Student ID: 038
Student Name: Abdul Rehman

Registered Courses:
- Programming Fundamentals (Course ID: CP101)
```

## Data Storage and File Handling

The project uses two binary files to store information permanently.

| File Name | Purpose |
|---|---|
| `courses.dat` | Stores course IDs, course names, and credit hours. |
| `registrations.dat` | Stores student IDs, student names, and course IDs. |

### How Data Persistence Works

- When the program starts, `loadRecords()` loads previously saved records.
- When a course or registration is added, updated, or deleted, `saveRecords()` saves the changes.
- When the user exits, the program saves all records again.
- When the program is opened again, the saved records are loaded automatically.

This ensures that information is not lost when the application is closed.

## Input Validation

The program includes several input validation checks:

- Course IDs and student IDs cannot be empty.
- IDs can contain only letters and numbers.
- IDs are automatically converted to uppercase.
- Duplicate course IDs are not allowed.
- Students cannot register for a course that does not exist.
- Duplicate registrations are prevented.
- Course names and student names cannot be empty.
- Credit hours must be greater than zero.
- Invalid menu choices are rejected.

## Project Limitations

- Maximum number of courses: 100.
- Maximum number of registrations: 200.
- Maximum course ID and student ID length: 19 characters.
- Maximum course name and student name length: 49 characters.
- The application is currently terminal-based and does not include a graphical user interface.

## Project Structure

```text
Course-Registration-System/
│
├── main.c
├── courses.dat
├── registrations.dat
└── README.md
```

**Note:** The two `.dat` files are created automatically when records are saved. They do not need to be created manually.

## Conclusion

The Course Registration Management System is a practical C programming project that demonstrates the implementation of fundamental programming concepts in a real-world university management scenario.

It combines structures, arrays, pointers, functions, loops, string handling, and file handling to provide an organized way to manage courses and student registrations.

The project also demonstrates how data can be stored permanently using binary files, making the application useful beyond a single program execution.

---

**Developed Using:** C Programming Language
**Project Type:** Console-Based Application
**Data Storage:** Binary File Handling
