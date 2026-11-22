/*
 * Course Registration Management System:
 
 */

#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define COURSE_LIMIT 100
#define REGISTRATION_LIMIT 200
#define ID_SIZE 20
#define NAME_SIZE 50

#define COURSE_FILE "courses.dat"
#define REGISTRATION_FILE "registrations.dat"

/* Store course information */
struct Course {
    char courseID[ID_SIZE];
    char courseName[NAME_SIZE];
    int credits;
};

/* Store student registration information */
struct Registration {
    char studID[ID_SIZE];
    char studName[NAME_SIZE];
    char courseID[ID_SIZE];
};

/* Arrays for a course and registration records */
struct Course courses[COURSE_LIMIT];
struct Registration registrations[REGISTRATION_LIMIT];

/* Record counters */
int totalCourses = 0;
int totalRegistrations = 0;

/* Function declarations */
int getInput(char prompt[], char input[], int size);
int getID(char prompt[], char id[]);
int getNumber(char prompt[], int *number);
int isBlank(const char *text);

struct Course *searchCourseByID(const char *id);

void saveRecords(void);
void loadRecords(void);

void addNewCourse(void);
void showCourses(void);
void addStudentRegistration(void);
void showRegistrations(void);
void checkCourseDetails(void);
void checkStudentDetails(void);
void removeCourse(void);
void removeRegistration(void);
void updateCourse(void);
void updateStudentName(void);


/* To get input from a user: */
int getInput(char prompt[], char input[], int size)
{
    char line[256];
    int length;
    int ch;

    printf("%s", prompt);

    if (fgets(line, sizeof(line), stdin) == NULL)
        return 0;

    length = strlen(line);

    /* Remove the Enter key newline */
    if (length > 0 && line[length - 1] == '\n') {
        line[length - 1] = '\0';
    }
    else if (!feof(stdin)) {

        /* Clear the remaining input */
        ch = getchar();

        while (ch != '\n' && ch != EOF) {
            ch = getchar();
        }

        printf("Input is too long!\n");
        return -1;
    }

    /* Check if input fits in the array */
    if (strlen(line) >= (size_t)size) {
        printf("Input is too long! Maximum %d characters allowed.\n",
               size - 1);
        return -1;
    }

    strcpy(input, line);

    return 1;
}


/* Check if input is empty */
int isBlank(const char *text)
{
    int i;

    for (i = 0; text[i] != '\0'; i++) {

        if (text[i] != ' ' && text[i] != '\t')
            return 0;
    }

    return 1;
}


/* Get ID and convert it to uppercase */
int getID(char prompt[], char id[])
{
    int result;
    int i;

    result = getInput(prompt, id, ID_SIZE);

    if (result != 1)
        return result;

    if (strlen(id) == 0) {
        printf("ID cannot be empty!\n");
        return -1;
    }

    /* IDs can only contain letters and numbers */
    for (i = 0; id[i] != '\0'; i++) {

        if (!((id[i] >= 'A' && id[i] <= 'Z') ||
              (id[i] >= 'a' && id[i] <= 'z') ||
              (id[i] >= '0' && id[i] <= '9'))) {

            printf("ID can only contain letters and numbers!\n");
            return -1;
        }

        /* Convert small letters into capital letters */
        if (id[i] >= 'a' && id[i] <= 'z') {
            id[i] = id[i] - 'a' + 'A';
        }
    }

    return 1;
}


/* Get a number from user */
int getNumber(char prompt[], int *number)
{
    char input[100];
    int i = 0;
    int value = 0;
    int negative = 0;
    int result;

    result = getInput(prompt, input, sizeof(input));

    if (result != 1)
        return result;

    /* Check if the number is negative */
    if (input[i] == '-') {
        negative = 1;
        i++;
    }

    /* Check if at least one digit is entered */
    if (input[i] == '\0') {
        printf("Invalid input! Please enter a whole number.\n");
        return -1;
    }

    /* Check each digit */
    while (input[i] != '\0') {

        if (input[i] < '0' || input[i] > '9') {
            printf("Invalid input! Please enter a whole number.\n");
            return -1;
        }

        /* Avoid entering a number that is too large */
        if (i >= 9 + negative) {
            printf("Number is too large!\n");
            return -1;
        }

        value = value * 10 + (input[i] - '0');

        i++;
    }

    if (negative)
        value = -value;

    *number = value;

    return 1;
}


/* Search course by ID */
struct Course *searchCourseByID(const char *id)
{
    struct Course *ptr;

    for (ptr = courses; ptr < courses + totalCourses; ptr++) {

        if (strcmp(ptr->courseID, id) == 0)
            return ptr;
    }

    return NULL;
}


/* Save records to files */
void saveRecords(void)
{
    FILE *fp;
    int saved = 1;

    /* Write courses to file */
    fp = fopen(COURSE_FILE, "wb");

    if (fp == NULL) {
        printf("Could not save course records!\n");
        saved = 0;
    }
    else {

        if (fwrite(&totalCourses, sizeof(int), 1, fp) != 1 ||
            fwrite(courses, sizeof(struct Course), totalCourses, fp)
            != (size_t)totalCourses) {

            saved = 0;
        }

        if (fclose(fp) != 0)
            saved = 0;
    }

    /* Write registrations to file */
    fp = fopen(REGISTRATION_FILE, "wb");

    if (fp == NULL) {
        printf("Could not save registration records!\n");
        saved = 0;
    }
    else {

        if (fwrite(&totalRegistrations, sizeof(int), 1, fp) != 1 ||
            fwrite(registrations, sizeof(struct Registration),
                   totalRegistrations, fp) != (size_t)totalRegistrations) {

            saved = 0;
        }

        if (fclose(fp) != 0)
            saved = 0;
    }

    if (!saved)
        printf("Warning: Some data may not have been saved properly.\n");
}


/* Load saved records */
void loadRecords(void)
{
    FILE *fp;
    int count;
    int i;

    /* Read course records */
    fp = fopen(COURSE_FILE, "rb");

    if (fp != NULL) {

        if (fread(&count, sizeof(int), 1, fp) == 1 &&
            count >= 0 && count <= COURSE_LIMIT &&
            fread(courses, sizeof(struct Course), count, fp)
            == (size_t)count) {

            totalCourses = count;

            /* Make sure strings end properly */
            for (i = 0; i < totalCourses; i++) {
                courses[i].courseID[ID_SIZE - 1] = '\0';
                courses[i].courseName[NAME_SIZE - 1] = '\0';
            }
        }
        else {
            printf("Course file could not be loaded properly.\n");
        }

        fclose(fp);
    }

    /* Read registration records */
    fp = fopen(REGISTRATION_FILE, "rb");

    if (fp != NULL) {

        if (fread(&count, sizeof(int), 1, fp) == 1 &&
            count >= 0 && count <= REGISTRATION_LIMIT &&
            fread(registrations, sizeof(struct Registration), count, fp)
            == (size_t)count) {

            totalRegistrations = count;

            for (i = 0; i < totalRegistrations; i++) {
                registrations[i].studID[ID_SIZE - 1] = '\0';
                registrations[i].studName[NAME_SIZE - 1] = '\0';
                registrations[i].courseID[ID_SIZE - 1] = '\0';
            }
        }
        else {
            printf("Registration file could not be loaded properly.\n");
        }

        fclose(fp);
    }

    printf("Loaded %d course(s) and %d registration(s).\n",
           totalCourses, totalRegistrations);
}


/* Add a new course */
void addNewCourse(void)
{
    char id[ID_SIZE];
    char name[NAME_SIZE];
    int credits;
    int result;
    struct Course *ptr;

    if (totalCourses >= COURSE_LIMIT) {
        printf("Course limit reached!\n");
        return;
    }

    result = getID("Enter Course ID: ", id);

    if (result != 1)
        return;

    /* Check if course already exists */
    if (searchCourseByID(id) != NULL) {
        printf("This Course ID already exists!\n");
        return;
    }

    result = getInput("Enter Course Name: ", name, NAME_SIZE);

    if (result != 1)
        return;

    if (isBlank(name)) {
        printf("Course name cannot be empty!\n");
        return;
    }

    result = getNumber("Enter Credit Hours: ", &credits);

    if (result != 1)
        return;

    if (credits <= 0) {
        printf("Credit hours must be greater than 0!\n");
        return;
    }

    /* Add course to array */
    ptr = &courses[totalCourses];

    strcpy(ptr->courseID, id);
    strcpy(ptr->courseName, name);
    ptr->credits = credits;

    totalCourses++;

    printf("Course added successfully!\n");

    saveRecords();
}


/* Display all courses */
void showCourses(void)
{
    struct Course *ptr;

    if (totalCourses == 0) {
        printf("No courses available.\n");
        return;
    }

    printf("\n========== AVAILABLE COURSES ==========\n");

    printf("%-20s %-30s %s\n",
           "Course ID", "Course Name", "Credit Hours");

    /* Print course records using a pointer */
    for (ptr = courses; ptr < courses + totalCourses; ptr++) {

        printf("%-20s %-30s %d\n",
               ptr->courseID,
               ptr->courseName,
               ptr->credits);
    }
}


/* Register a student */
void addStudentRegistration(void)
{
    char studID[ID_SIZE];
    char studName[NAME_SIZE];
    char courseID[ID_SIZE];

    int result;
    int i;

    struct Registration *ptr;

    if (totalRegistrations >= REGISTRATION_LIMIT) {
        printf("Registration limit reached!\n");
        return;
    }

    if (totalCourses == 0) {
        printf("Please add a course first!\n");
        return;
    }

    result = getID("Enter Student ID: ", studID);

    if (result != 1)
        return;

    result = getInput("Enter Student Name: ", studName, NAME_SIZE);

    if (result != 1)
        return;

    if (isBlank(studName)) {
        printf("Student name cannot be empty!\n");
        return;
    }

    /* Check if student ID already belongs to another name */
    for (i = 0; i < totalRegistrations; i++) {

        if (strcmp(registrations[i].studID, studID) == 0) {

            if (strcmp(registrations[i].studName, studName) != 0) {
                printf("This Student ID already belongs to %s.\n",
                       registrations[i].studName);
                printf("Please enter the same student name.\n");
                return;
            }

            break;
        }
    }

    result = getID("Enter Course ID: ", courseID);

    if (result != 1)
        return;

    /* Check whether course exists */
    if (searchCourseByID(courseID) == NULL) {
        printf("Course not found! Registration failed.\n");
        return;
    }

    /* Check if student is already registered in this course */
    for (i = 0; i < totalRegistrations; i++) {

        if (strcmp(registrations[i].studID, studID) == 0 &&
            strcmp(registrations[i].courseID, courseID) == 0) {

            printf("Student is already registered in this course!\n");
            return;
        }
    }

    /* Add registration to array */
    ptr = &registrations[totalRegistrations];

    strcpy(ptr->studID, studID);
    strcpy(ptr->studName, studName);
    strcpy(ptr->courseID, courseID);

    totalRegistrations++;

    printf("Student registered successfully!\n");

    saveRecords();
}


/* Display all registrations */
void showRegistrations(void)
{
    int i, j;
    int alreadyPrinted;
    int firstCourse;

    struct Course *course;

    if (totalRegistrations == 0) {
        printf("No registrations found.\n");
        return;
    }

    printf("\n========== STUDENT REGISTRATIONS ==========\n");

    printf("%-20s %-25s %s\n",
           "Student ID", "Student Name", "Registered Courses");

    for (i = 0; i < totalRegistrations; i++) {

        alreadyPrinted = 0;

        /* Check if student was already displayed */
        for (j = 0; j < i; j++) {

            if (strcmp(registrations[i].studID,
                       registrations[j].studID) == 0) {

                alreadyPrinted = 1;
                break;
            }
        }

        /* Display each student only once */
        if (alreadyPrinted == 0) {

            printf("%-20s %-25s ",
                   registrations[i].studID,
                   registrations[i].studName);

            firstCourse = 1;

            /* Display all courses of this student */
            for (j = 0; j < totalRegistrations; j++) {

                if (strcmp(registrations[i].studID,
                           registrations[j].studID) == 0) {

                    course = searchCourseByID(
                        registrations[j].courseID);

                    if (course != NULL) {

                        if (firstCourse == 0)
                            printf(", ");

                        printf("%s (ID: %s)",
                               course->courseName,
                               registrations[j].courseID);

                        firstCourse = 0;
                    }
                }
            }

            printf("\n");
        }
    }
}


/* Search and display course details */
void checkCourseDetails(void)
{
    char id[ID_SIZE];
    int result;

    struct Course *ptr;

    result = getID("Enter Course ID to search: ", id);

    if (result != 1)
        return;

    ptr = searchCourseByID(id);

    if (ptr == NULL) {
        printf("Course not found!\n");
    }
    else {

        printf("\n========== COURSE DETAILS ==========\n");

        printf("Course ID: %s\n", ptr->courseID);
        printf("Course Name: %s\n", ptr->courseName);
        printf("Credit Hours: %d\n", ptr->credits);
    }
}


/* Display student details */
void checkStudentDetails(void)
{
    char id[ID_SIZE];

    int result;
    int found = 0;

    struct Registration *ptr;
    struct Course *course;

    result = getID("Enter Student ID to search: ", id);

    if (result != 1)
        return;

    /* Search through all registrations */
    for (ptr = registrations;
         ptr < registrations + totalRegistrations;
         ptr++) {

        if (strcmp(ptr->studID, id) == 0) {

            /* Display student information once */
            if (found == 0) {

                printf("\n========== STUDENT DETAILS ==========\n");

                printf("Student ID: %s\n", ptr->studID);
                printf("Student Name: %s\n", ptr->studName);

                printf("\nRegistered Courses:\n");

                found = 1;
            }

            course = searchCourseByID(ptr->courseID);

            if (course != NULL) {

                printf("- %s (Course ID: %s)\n",
                       course->courseName,
                       ptr->courseID);
            }
        }
    }

    if (found == 0) {
        printf("No registrations found for this student.\n");
    }
}


/* Update course information */
void updateCourse(void)
{
    char id[ID_SIZE];
    char name[NAME_SIZE];

    int result;
    int choice;
    int credits;

    struct Course *ptr;

    result = getID("Enter Course ID to update: ", id);

    if (result != 1)
        return;

    /* Find the course using its ID */
    ptr = searchCourseByID(id);

    if (ptr == NULL) {
        printf("Course not found!\n");
        return;
    }

    printf("\nCurrent Course Name: %s\n", ptr->courseName);
    printf("Current Credit Hours: %d\n", ptr->credits);

    printf("\n1. Update Course Name\n");
    printf("2. Update Credit Hours\n");

    result = getNumber("Enter your choice: ", &choice);

    if (result != 1)
        return;

    if (choice == 1) {

        /* Get the new course name */
        result = getInput("Enter New Course Name: ",
                          name, NAME_SIZE);

        if (result != 1)
            return;

        if (isBlank(name)) {
            printf("Course name cannot be empty!\n");
            return;
        }

        strcpy(ptr->courseName, name);
    }
    else if (choice == 2) {

        /* Get the new credit hours */
        result = getNumber("Enter New Credit Hours: ", &credits);

        if (result != 1)
            return;

        if (credits <= 0) {
            printf("Credit hours must be greater than 0!\n");
            return;
        }

        ptr->credits = credits;
    }
    else {
        printf("Invalid choice!\n");
        return;
    }

    printf("Course updated successfully!\n");

    saveRecords();
}


/* Update a student's name in all registrations */
void updateStudentName(void)
{
    char id[ID_SIZE];
    char name[NAME_SIZE];

    int result;
    int i;
    int found = 0;

    result = getID("Enter Student ID to update: ", id);

    if (result != 1)
        return;

    /* Check if the student exists */
    for (i = 0; i < totalRegistrations; i++) {

        if (strcmp(registrations[i].studID, id) == 0) {
            found = 1;
            break;
        }
    }

    if (found == 0) {
        printf("Student not found!\n");
        return;
    }

    result = getInput("Enter New Student Name: ", name, NAME_SIZE);

    if (result != 1)
        return;

    if (isBlank(name)) {
        printf("Student name cannot be empty!\n");
        return;
    }

    /* Change the name in every registration of this student */
    for (i = 0; i < totalRegistrations; i++) {

        if (strcmp(registrations[i].studID, id) == 0) {
            strcpy(registrations[i].studName, name);
        }
    }

    printf("Student name updated successfully!\n");

    saveRecords();
}


/* Delete course and related registrations */
void removeCourse(void)
{
    char id[ID_SIZE];

    int result;
    int i;
    int j;
    int position;

    struct Course *ptr;

    result = getID("Enter Course ID to delete: ", id);

    if (result != 1)
        return;

    ptr = searchCourseByID(id);

    if (ptr == NULL) {
        printf("Course not found!\n");
        return;
    }

    /* Get course position */
    position = (int)(ptr - courses);

    /* Delete all registrations of this course */
    i = 0;

    while (i < totalRegistrations) {

        if (strcmp(registrations[i].courseID, id) == 0) {

            /* Shift records left */
            for (j = i; j < totalRegistrations - 1; j++) {
                registrations[j] = registrations[j + 1];
            }

            totalRegistrations--;

        }
        else {
            i++;
        }
    }

    /* Delete course from array */
    for (i = position; i < totalCourses - 1; i++) {
        courses[i] = courses[i + 1];
    }

    totalCourses--;

    printf("Course and its registrations deleted successfully!\n");

    saveRecords();
}


/* Delete a student's registration */
void removeRegistration(void)
{
    char studID[ID_SIZE];
    char courseID[ID_SIZE];

    int result;
    int i;
    int j;
    int found = 0;

    result = getID("Enter Student ID: ", studID);

    if (result != 1)
        return;

    result = getID("Enter Course ID to unregister: ", courseID);

    if (result != 1)
        return;

    /* Search for the matching student and course */
    for (i = 0; i < totalRegistrations; i++) {

        if (strcmp(registrations[i].studID, studID) == 0 &&
            strcmp(registrations[i].courseID, courseID) == 0) {

            /* Shift remaining records left */
            for (j = i; j < totalRegistrations - 1; j++) {
                registrations[j] = registrations[j + 1];
            }

            totalRegistrations--;

            found = 1;

            break;
        }
    }

    if (found == 1) {

        printf("Student registration deleted successfully!\n");

        saveRecords();

    }
    else {

        printf("Registration not found!\n");
    }
}


/* Main menu - Functions */
int main(void)
{
    int choice = 0;
    int result;

    /* Load saved records when program starts */
    loadRecords();

    do {

        printf("\n========================================\n");
        printf("       COURSE REGISTRATION SYSTEM\n");
        printf("========================================\n");

        printf("1. Add New Course\n");
        printf("2. View Courses\n");
        printf("3. Register Student\n");
        printf("4. View Registrations\n");
        printf("5. Search Course\n");
        printf("6. Search Student\n");
        printf("7. Delete Course\n");
        printf("8. Delete Student Registration\n");
        printf("9. Update Course\n");
        printf("10. Update Student Name\n");
        printf("11. Exit\n");

        result = getNumber("Enter your choice: ", &choice);

        if (result == 0) {
            printf("\nInput ended. Exiting program.\n");
            break;
        }

        if (result == -1)
            continue;

        switch (choice) {

            case 1:
                addNewCourse();
                break;

            case 2:
                showCourses();
                break;

            case 3:
                addStudentRegistration();
                break;

            case 4:
                showRegistrations();
                break;

            case 5:
                checkCourseDetails();
                break;

            case 6:
                checkStudentDetails();
                break;

            case 7:
                removeCourse();
                break;

            case 8:
                removeRegistration();
                break;

            case 9:
                updateCourse();
                break;

            case 10:
                updateStudentName();
                break;

            case 11:
                saveRecords();
                printf("Thank you for using the system!\n");
                break;

            default:
                printf("Invalid choice! Please enter a number from 1 to 11.\n");
        }

    } while (choice != 11);

    return 0;
}
