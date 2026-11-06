#include <stdio.h>

#define MAX_STUDENTS 5
#define MAX_SUBJECTS 4

int main() {
    // 2D Array to store marks: [Students][Subjects]
    float marks[MAX_STUDENTS][MAX_SUBJECTS] = {
        {85.5, 90.0, 78.5, 92.0},
        {70.0, 65.5, 80.0, 75.0},
        {95.0, 92.5, 88.0, 96.0},
        {60.0, 55.0, 65.5, 58.0},
        {82.0, 79.5, 85.0, 88.0}
    };

    char studentNames[MAX_STUDENTS][20] = {
        "Alice Smith",
        "Bob Jones",
        "Charlie Brown",
        "Diana Prince",
        "Ethan Hunt"
    };

    char subjectNames[MAX_SUBJECTS][15] = {"Mathematics", "Physics", "Chemistry", "Computer Sci"};

    float studentTotals[MAX_STUDENTS] = {0};
    float studentAverages[MAX_STUDENTS] = {0};
    float subjectTotals[MAX_SUBJECTS] = {0};
    float subjectAverages[MAX_SUBJECTS] = {0};

    float highestScore = marks[0][0];
    float lowestScore = marks[0][0];
    int topStudent = 0, topSubject = 0;

    // --- NESTED LOOP 1: Calculate Student Totals and Find High/Low Scores ---
    for (int i = 0; i < MAX_STUDENTS; i++) {
        for (int j = 0; j < MAX_SUBJECTS; j++) {
            studentTotals[i] += marks[i][j];

            // Track absolute highest and lowest marks in the system
            if (marks[i][j] > highestScore) {
                highestScore = marks[i][j];
            }
            if (marks[i][j] < lowestScore) {
                lowestScore = marks[i][j];
            }
        }
        studentAverages[i] = studentTotals[i] / MAX_SUBJECTS;
    }

    // --- NESTED LOOP 2: Calculate Subject Totals and Averages ---
    for (int j = 0; j < MAX_SUBJECTS; j++) {
        for (int i = 0; i < MAX_STUDENTS; i++) {
            subjectTotals[j] += marks[i][j];
        }
        subjectAverages[j] = subjectTotals[j] / MAX_STUDENTS;
    }

    // --- OUTPUT SECTION: Display Report Card ---
    printf("=========================================================================\n");
    printf("                     STUDENT GRADE MANAGEMENT SYSTEM                     \n");
    printf("=========================================================================\n\n");

    // Print Header
    printf("%-15s", "Student");
    for (int j = 0; j < MAX_SUBJECTS; j++) {
        printf("%-15s", subjectNames[j]);
    }
    printf("%-10s%-10s\n", "Total", "Average");
    printf("-------------------------------------------------------------------------\n");

    // --- NESTED LOOP 3: Print Matrix Data ---
    for (int i = 0; i < MAX_STUDENTS; i++) {
        printf("%-15s", studentNames[i]);
        for (int j = 0; j < MAX_SUBJECTS; j++) {
            printf("%-15.2f", marks[i][j]);
        }
        printf("%-10.2f%-10.2f\n", studentTotals[i], studentAverages[i]);
    }

    printf("-------------------------------------------------------------------------\n");
    
    // Print Subject Averages Footer
    printf("%-15s", "Sub. Avg");
    for (int j = 0; j < MAX_SUBJECTS; j++) {
        printf("%-15.2f", subjectAverages[j]);
    }
    printf("\n=========================================================================\n\n");

    // Print Statistics Summary
    printf("SYSTEM PERFORMANCE SUMMARY:\n");
    printf("------------------------------------\n");
    printf("Highest Score Recorded : %.2f\n", highestScore);
    printf("Lowest Score Recorded  : %.2f\n", lowestScore);
    printf("------------------------------------\n");

    return 0;
}
