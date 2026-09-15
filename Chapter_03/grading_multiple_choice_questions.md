#include <iostream>

int main() {
    // Define the dimensions of the dataset
    const int NUM_STUDENTS = 8;
    const int NUM_QUESTIONS = 10;

    // Two-dimensional array storing students' answers
    char answers[NUM_STUDENTS][NUM_QUESTIONS] = {
        {'A', 'B', 'A', 'C', 'C', 'D', 'E', 'E', 'A', 'D'}, // Student 0
        {'D', 'B', 'A', 'B', 'C', 'A', 'E', 'E', 'A', 'D'}, // Student 1
        {'E', 'D', 'D', 'A', 'C', 'B', 'E', 'E', 'A', 'D'}, // Student 2
        {'C', 'B', 'A', 'E', 'D', 'C', 'E', 'E', 'A', 'D'}, // Student 3
        {'A', 'B', 'D', 'C', 'C', 'D', 'E', 'E', 'A', 'D'}, // Student 4
        {'B', 'B', 'E', 'C', 'C', 'D', 'E', 'E', 'A', 'D'}, // Student 5
        {'B', 'B', 'A', 'C', 'C', 'D', 'E', 'E', 'A', 'D'}, // Student 6
        {'E', 'B', 'E', 'C', 'C', 'D', 'E', 'E', 'A', 'D'}  // Student 7
    };

    // One-dimensional array storing the answer key
    char key[NUM_QUESTIONS] = {'D', 'B', 'D', 'C', 'C', 'D', 'A', 'E', 'A', 'D'};

    std::cout << "--- Test Grading Results ---" << std::endl;

    // Outer loop iterates through each student
    for (int i = 0; i < NUM_STUDENTS; i++) {
        int correctCount = 0;

        // Inner loop iterates through each question for the current student
        for (int j = 0; j < NUM_QUESTIONS; j++) {
            if (answers[i][j] == key[j]) {
                correctCount++;
            }
        }

        // Display the results for the current student
        std::cout << "Student " << i << "'s correct count is " << correctCount << std::endl;
    }

    return 0;
}
