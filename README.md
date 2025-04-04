# Simple-Task-Manager
this is a simple project to keep and manage your daily life tasks. 
the project code is given below:


#include <stdio.h>
#include <string.h>

// Define Maximum Tasks
#define MAX_TASKS 10 

// Structure for Task
struct Task {
    char title[50];
    char dueDate[15];
    int completed; // 0 = Not Completed, 1 = Completed
};

// Task List and Counter
struct Task tasks[MAX_TASKS];
int taskCount = 0;

// Function to Add a Task
void addTask() {
    if (taskCount >= MAX_TASKS) {
        printf("\nTask list is full!\n");
        return;
    }

    printf("\nEnter Task Title: ");
    getchar(); // Clear input buffer
    fgets(tasks[taskCount].title, sizeof(tasks[taskCount].title), stdin);
    tasks[taskCount].title[strcspn(tasks[taskCount].title, "\n")] = '\0'; // Remove newline

    printf("Enter Due Date (DD/MM/YYYY): ");
    scanf("%14s", tasks[taskCount].dueDate);

    tasks[taskCount].completed = 0; // Task starts as not completed
    taskCount++;

    printf("\nTask Added Successfully!\n");
}

// Function to Show Tasks
void displayTasks() {
    if (taskCount == 0) {
        printf("\nNo tasks available.\n");
        return;
    }

    printf("\nTask List:\n");
    printf("ID   Title                Due Date      Status\n");
    printf("---------------------------------------------\n");

    for (int i = 0; i < taskCount; i++) {
        printf("%-4d %-20s %-12s %s\n", i + 1, tasks[i].title, tasks[i].dueDate,
               tasks[i].completed ? "Done" : "Pending");
    }
}

// Function to Mark Task as Completed
void markCompleted() {
    int id;
    printf("\nEnter Task ID to mark as completed: ");
    scanf("%d", &id);

    if (id > 0 && id <= taskCount) {
        tasks[id - 1].completed = 1;
        printf("\nTask Marked as Completed!\n");
    } else {
        printf("\nInvalid Task ID!\n");
    }
}

// Function to Delete a Task
void deleteTask() {
    int id;
    printf("\nEnter Task ID to delete: ");
    scanf("%d", &id);

    if (id > 0 && id <= taskCount) {
        for (int i = id - 1; i < taskCount - 1; i++) {
            tasks[i] = tasks[i + 1]; // Shift tasks left
        }
        taskCount--;
        printf("\nTask Deleted Successfully!\n");
    } else {
        printf("\nInvalid Task ID!\n");
    }
}

// Function to Show Menu
void showMenu() {
    printf("\nSmart Task Manager\n");
    printf("-----------------------------\n");
    printf("1. Add Task\n");
    printf("2. View Tasks\n");
    printf("3. Mark Task as Completed\n");
    printf("4. Delete Task\n");
    printf("5. Exit\n");
}

// Main Function
int main() {
    int choice;

    while (1) {
        showMenu();
        printf("\nEnter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1: addTask(); break;
            case 2: displayTasks(); break;
            case 3: markCompleted(); break;
            case 4: deleteTask(); break;
            case 5: printf("\nExiting program...\n"); return 0;
            default: printf("\nInvalid choice! Try again.\n");
        }
    }

    return 0;
}
