#include <iostream>
#include <vector>
#include <algorithm>

// Class responsible for storing answer data and performing evaluation logic
class ExamGrader {
private:
    std::vector<std::vector<char>> studentAnswers;
    std::vector<char> answerKey;

public:
    // Constructor initializes the student response matrix and key vector
    ExamGrader(const std::vector<std::vector<char>>& answers, const std::vector<char>& key)
        : studentAnswers(answers), answerKey(key) {}

    // Evaluates a single student's total correct answers
    int calculateScore(size_t studentIndex) const {
        if (studentIndex >= studentAnswers.size()) {
            return -1; // Out of bounds safety check
        }

        int correctCount = 0;
        size_t numQuestions = std::min(studentAnswers[studentIndex].size(), answerKey.size());

        for (size_t j = 0; j < numQuestions; ++j) {
            if (studentAnswers[studentIndex][j] == answerKey[j]) {
                correctCount++;
            }
        }
        return correctCount;
    }

    // Evaluates and prints scores for all students
    void gradeAllStudents() const {
        std::cout << "--- Test Grading Results ---" << std::endl;
        for (size_t i = 0; i < studentAnswers.size(); ++i) {
            int score = calculateScore(i);
            std::cout << "Student " << i << "'s correct count is " << score << std::endl;
        }
    }
};

int main() {
    // Student responses stored in a 2D dynamic vector
    const std::vector<std::vector<char>> answers = {
        {'A', 'B', 'A', 'C', 'C', 'D', 'E', 'E', 'A', 'D'}, // Student 0
        {'D', 'B', 'A', 'B', 'C', 'A', 'E', 'E', 'A', 'D'}, // Student 1
        {'E', 'D', 'D', 'A', 'C', 'B', 'E', 'E', 'A', 'D'}, // Student 2
        {'C', 'B', 'A', 'E', 'D', 'C', 'E', 'E', 'A', 'D'}, // Student 3
        {'A', 'B', 'D', 'C', 'C', 'D', 'E', 'E', 'A', 'D'}, // Student 4
        {'B', 'B', 'E', 'C', 'C', 'D', 'E', 'E', 'A', 'D'}, // Student 5
        {'B', 'B', 'A', 'C', 'C', 'D', 'E', 'E', 'A', 'D'}, // Student 6
        {'E', 'B', 'E', 'C', 'C', 'D', 'E', 'E', 'A', 'D'}  // Student 7
    };

    // Correct answer key stored in a 1D vector
    const std::vector<char> key = {'D', 'B', 'D', 'C', 'C', 'D', 'A', 'E', 'A', 'D'};

    // Instantiate object and execute evaluation pipeline
    ExamGrader grader(answers, key);
    grader.gradeAllStudents();

    return 0;
}
```

---

## 2. Program Documentation (`grade_exam.md`)

### OOP Concepts Used

*   **Encapsulation:** The dataset containing student responses (`studentAnswers`) and correct answers (`answerKey`) is bundled inside the `ExamGrader` class under the `private` access specifier. External interactions are strictly managed through `public` member functions (`calculateScore` and `gradeAllStudents`), preventing unauthorized data manipulation.
*   **Abstraction:** The grading process is hidden behind high-level method calls (`grader.gradeAllStudents()`). A caller executing the program does not need to manage array indexing or comparison logic directly; the structural complexity is completely encapsulated within the class interface.

---

### Algorithm & Solution Steps

1.  **Data Ingestion & Initialization:**
    *   Construct an instance of `ExamGrader` by passing a 2D dynamic vector of student responses and a 1D dynamic vector representing the answer key.
    *   Store data internally within `private` member variables via const-reference passing to optimize memory usage.

2.  **Iterative Grading Process:**
    *   Loop through each student index `i` from `0` to $N - 1$, where $N$ is the total number of students.
    *   For each student, iterate through each question index `j` from `0` to $M - 1$, where $M$ is the total number of questions.
    *   Compare `studentAnswers[i][j]` against `answerKey[j]`. If the character values match, increment the student's correct count variable by `1`.

3.  **Result Formatting:**
    *   Output the total count of correct answers per student sequentially to standard output (`std::cout`).

---

### Possible Error Points & Edge Cases

*   **Mismatched Answer Lengths:** If a student's answer vector has fewer elements than the answer key, accessing elements beyond the student array bound causes an out-of-bounds access error. The code mitigates this by restricting comparison iteration to `std::min(studentAnswers[studentIndex].size(), answerKey.size())`.
*   **Case Sensitivity:** The evaluation directly compares character values (e.g., `'a' == 'A'`). Mixed-case inputs will evaluate as incorrect matches unless normalized prior to comparison.
*   **Empty Data Inputs:** Passing an empty student array or empty answer key could cause undefined behavior or out-of-bounds access if bounds checks are omitte
