#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#include <math.h>

// Function declarations
char getRandomOperator();
double calculateResult1(double num1, double num2, char operator);
double calculateResult2(double num1, double num2,double num3, char operator);
int askQuestion(double num1, double num2, char operator);
void runQuiz(int difficulty);

int main() {
    srand(time(0)); // Seed for random number generation
    int choice;

    printf("Welcome to Math Quiz\n");
    printf("Select difficulty level: 1. Easy  2. Hard:\n");
    scanf("%d", &choice);

    switch (choice) {
        case 1:
            printf("You selected Easy mode.\n");
            runQuiz(1);
            break;
        case 2:
            printf("You selected Hard mode.\n");
            runQuiz(2);
            break;
        default:
            printf("Invalid choice. Please restart the program.\n");
            break;
    }

    return 0;
}
char getRandomOperator() {
    char operators[] = {'+', '-', '*', '/'};
    int size = sizeof(operators) / sizeof(operators[0]);
    return operators[rand() % size]; // Randomly select an operator
}

double calculateResult1(double num1, double num2, char operator) {
    switch (operator) {
        case '+': return num1 + num2;
        case '-': return num1 - num2;
        case '*': return num1 * num2;
        case '/': return (num2 != 0) ? num1 / num2 : NAN; // Handle division by zero
        default: return NAN; // Invalid operator
    }
}

double calculateResult2(double num1, double num2, double num3, char operator) {
    switch (operator) {
        case '+': return (num3 - num2) / num1;
        case '-': return (num3 + num2) / num1;
        case '*': return (num1 != 0) ? num3 / (num1 * num3) : NAN; // Avoid division by zero
        case '/': return (num2 != 0) ? (num3 * num2) / num1 : NAN; // Avoid division by zero
        default: return NAN; // Invalid operator
    }
}

int askQuestion(double num1, double num2, char operator) {
    double correctAnswer = calculateResult1(num1, num2, operator);
    double userAnswer;

    printf("What is %.1f %c %.1f? ", num1, operator, num2);
    scanf("%lf", &userAnswer);

    if (fabs(userAnswer - correctAnswer) < 0.01) { // Allow for minor floating-point errors
        printf("Correct!\n");
        return 1; // Correct answer
    } else {
        printf("Wrong! The correct answer was %.2f.\n", correctAnswer);
        return 0; // Incorrect answer
    }
}
void runQuiz(int difficulty) {
    int score = 0;
    int numQuestions = 5; // Number of questions

    for (int i = 0; i < numQuestions; i++) {
        double num1 = rand() % 100 + 1; // Random number between 1 and 100
        double num2 = rand() % 100 + 1;
        char operator = getRandomOperator();

        if (difficulty == 1) { // Easy mode
            score += askQuestion(num1, num2, operator);
        } else if (difficulty == 2) { // Hard mode
            double num3 = rand() % 100 + 1; // A third random number for hard mode
            printf("Solve for x: %.1f %c %.1f = %.1f\n", num1, operator, num2, num3);
            
            // Calculate the answer for hard mode
            double correctAnswer = calculateResult2(num1, num2, num3, operator);
            double userAnswer;
            scanf("%lf", &userAnswer);

            if (fabs(userAnswer - correctAnswer) < 0.01) {
                printf("Correct!\n");
                score++;
            } else {
                printf("Wrong! The correct answer was %.2f.\n", correctAnswer);
            }
        }
    }

    printf("Your final score: %d/%d\n", score, numQuestions);
}



    
    default:
        break;
    }
}
