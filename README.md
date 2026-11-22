# Course Registration Management System

A menu-driven Course Registration Management System developed in C for **CS-115 Computer Programming** (Open Ended Lab / Complex Engineering Problem), Department of Computer & Information Systems Engineering, **NED University of Engineering and Technology**, FE Batch 2026, Fall Semester 2026.

## Group Members

| Name | Roll No. | Section |
| --- | --- | --- |
| Muhammad Rohaan Azhar | CS-26042 | A |
| Abd Ur Rehman | CS-26038 | A |
| Syeda Mahnoor Hashmi | CS-26052 | B |
| Hadia Khan | CS-26064 | B |

**Instructor:** MISS MAHNOOR

## Project Overview

This console application manages courses and student registrations. A user can add, view, search, update and delete records through a text menu. All records are saved to binary files, so data remains available after the program is closed and reopened.

## Main Features

1. **Add New Course:** Add a course with its ID, name and credit hours.
2. **View Courses:** Display all available courses.
3. **Register Student:** Register a student in an existing course.
4. **View Registrations:** Display each student with their registered courses.
5. **Search Course:** Search for a course by course ID.
6. **Search Student:** Search for a student by student ID.
7. **Delete Course:** Delete a course and all registrations linked to it.
8. **Delete Student Registration:** Remove a student from a particular course.
9. **Update Course:** Update the course name or credit hours.
10. **Update Student Name:** Change a student's name in all of their registrations.
11. **Exit:** Save all records and close the program.

## C Concepts Demonstrated

- **Data types and operators:** integers, character arrays, arithmetic, comparison and logical operators
- **Decision making:** `if`, `else if`, `else` and `switch`
- **Loops:** `for`, `while` and `do-while`
- **User-defined functions:** each operation is a separate function
- **Arrays:** fixed-size arrays of structures
- **Strings:** IDs and names handled with `strlen()`, `strcpy()` and `strcmp()`
- **Pointers:** accessing records and returning a matching course from the search function
- **Structures:** `Course` and `Registration` records
- **File I/O:** binary files with `fopen()`, `fread()`, `fwrite()` and `fclose()`

## How to Compile and Run

### Requirements

- GCC compiler (for example MinGW on Windows)
- Any terminal or Visual Studio Code

### Compile

```
gcc course_registration.c -o course
```

### Run

**Windows:**

```
.\course.exe
```

**Linux / macOS:**

```
./course
```

## Menu

```
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

## Example Usage

**Add a course**

```
Enter Course ID: CS101
Enter Course Name: Introduction to Programming
Enter Credit Hours: 3
Course added successfully!
```

**Register a student**

```
Enter Student ID: CS26042
Enter Student Name: Muhammad Rohaan Azhar
Enter Course ID: CS101
Student registered successfully!
```

**Search for a student**

```
Enter Student ID to search: CS26042

========== STUDENT DETAILS ==========
Student ID: CS26042
Student Name: Muhammad Rohaan Azhar

Registered Courses:
- Introduction to Programming (Course ID: CS101)
```

## Data Storage

Two binary files store the data. They are created automatically in the program's working directory when records are first saved, so they do not need to be created manually.

| File | Contents |
| --- | --- |
| `courses.dat` | Course ID, course name and credit hours |
| `registrations.dat` | Student ID, student name and course ID |

- `loadRecords()` runs at startup and loads saved records.
- `saveRecords()` runs after every add, update or delete, and on exit.
- The stored record counts are checked against the array limits before loading.

## Input Validation

- IDs cannot be empty and may contain only letters and digits
- IDs are converted to uppercase automatically
- Duplicate course IDs are rejected
- A student cannot register for a course that does not exist
- The same student cannot register twice in the same course
- A student ID cannot be used with a different name
- Course and student names cannot be blank
- Credit hours must be a whole number greater than zero
- Non-numeric or invalid menu input is rejected

## Limitations

- Maximum 100 courses and 200 registrations
- Maximum ID length: 19 characters; maximum name length: 49 characters
- Console interface only (no GUI)
- Data is stored in binary files, not a database
- No login or user roles

## Project Structure

```
course_management_system/
├── course_registration.c
└── README.md
```

`courses.dat` and `registrations.dat` are generated when the program runs.

## Tools Used

- Language: C
- Compiler: GCC (MinGW.org GCC-6.3.0-1)
- Editor: Visual Studio Code
- Platform: Windows 10
