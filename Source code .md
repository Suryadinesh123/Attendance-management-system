
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_STUDENTS 100
#define MAX_NAME_LENGTH 50

// Structure to represent a student
typedef struct {
    int rollNumber;
    char name[MAX_NAME_LENGTH];
    int attendance;
} Student;

// Function to mark attendance
void markAttendance(Student students[], int numStudents) {
    int rollNumber;
    printf("Enter roll number: ");
    scanf("%d", &rollNumber);

    for (int i = 0; i < numStudents; i++) {
        if (students[i].rollNumber == rollNumber) {
            students[i].attendance = 1;
            printf("Attendance marked for %s.\n", students[i].name);
            return;
        }
    }

    printf("Student not found.\n");
}

// Function to show attendance report
void showAttendanceReport(Student students[], int numStudents) {
    printf("Attendance Report:\n");
    for (int i = 0; i < numStudents; i++) {
        if (students[i].attendance == 1) {
            printf("%s (Roll Number: %d): Present\n", students[i].name, students[i].rollNumber);
        } else {
            printf("%s (Roll Number: %d): Absent\n", students[i].name, students[i].rollNumber);
        }
    }
}

// Function to save attendance report to file
void saveAttendanceReportToFile(Student students[], int numStudents) {
    FILE* file = fopen("attendance_log.txt", "a");
    if (file == NULL) {
        printf("Error opening file.\n");
        return;
    }

    fprintf(file, "Attendance Report:\n");
    for (int i = 0; i < numStudents; i++) {
        if (students[i].attendance == 1) {
            fprintf(file, "%s (Roll Number: %d): Present\n", students[i].name, students[i].rollNumber);
        } else {
            fprintf(file, "%s (Roll Number: %d): Absent\n", students[i].name, students[i].rollNumber);
        }
    }
    fprintf(file, "\n");

    fclose(file);
    printf("Attendance report saved to file.\n");
}

int main() {
    int numStudents;
    printf("Enter the number of students: ");
    scanf("%d", &numStudents);

    Student students[numStudents];
    for (int i = 0; i < numStudents; i++) {
        printf("Enter name for student %d: ", i + 1);
        scanf("%s", students[i].name);
        students[i].rollNumber = i + 1;
        students[i].attendance = 0;
    }

    while (1) {
        printf("\nAttendance Management System\n");
        printf("1. Mark Attendance\n");
        printf("2. Show Attendance Report\n");
        printf("3. Save Attendance Report to File\n");
        printf("4. Exit\n");
        printf("Enter your choice: ");

        int choice;
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                markAttendance(students, numStudents);
                break;
            case 2:
                showAttendanceReport(students, numStudents);
                break;
            case 3:
                saveAttendanceReportToFile(students, numStudents);
                break;
            case 4:
                return 0;
            default:
                printf("Invalid choice. Please choose a valid option.\n");
        }
    }

    return 0;
}
