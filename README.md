#include<stdio.h>
#include<time.h>
#include<stdlib.h>
int main()
{
    int choice;
    float answer;
    int i;
    char sign[] = {'+','-','*','/'};

    srand(time(0));

    printf("Welcome to Math Quiz\n");
    printf("Select difficulty level: 1. Easy  2. Hard:\n");
    scanf("%d",&choice);
    

    switch (choice)
    {
    case 1:
    printf("You selected Easy\n");
    int score = 0;
        for ( i = 1; i < 5; i++)
        {
            float num1 = rand() % 100 + 1;  
            float num2 = rand() % 100 + 1;
            char size = sizeof(sign) / sizeof(sign[0]);
            char random = rand() % size;
            char signval = sign[random];
            double result;
            switch (signval) {
        case '+':
            result = num1 + num2;
            break;
        case '-':
            result = num1 - num2;
            break;
        case '*':
            result = num1 * num2;
            break;
        case '/':
            if (num2 != 0) {
                result = num1 / num2;
            } else {
                printf("Error: Division by zero!\n");
                return 1; 
            }
            break;
        default:
            printf("Invalid operator!\n");
            return 1; 
            }
            printf("Question %d: %0.1f %c %0.1f = ?\n",i,num1,signval,num2);
            printf("Your answer:\n");
            scanf("%f",&answer);
            if (answer == result)
            {
                score++;
                printf("Correct!\n");
                
            }
            
            
            
        }
        printf("Your final score:%d\n",score);
        
        break;
    case 2:
    printf("You selected Hard\n");
    score = 0;
    for ( i = 1; i < 5; i++)
    {
        float num1 = rand() % 100 + 1;  
        float num2 = rand() % 100 + 1;
        float num3 = rand() % 100 + 1;
        char size = sizeof(sign) / sizeof(sign[0]);
        char random = rand() % size;
        char signval = sign[random];
        float result;
        switch (signval) {
        case '+':
            result = (num3 - num2)/num1;
            break;
        case '-':
            result = (num3 + num2)/num1;
            break;
        case '*':
            result = num3 / (num1*num3);
            break;
        case '/':
            if (num2 != 0) {
                result = (num3*num2) / num1;
            } else {
                printf("Error: Division by zero!\n");
                return 1; 
            }
            break;
        default:
            printf("Invalid operator!\n");
            return 1; 
        }
        printf("Question: %0.1fx %c %0.1f = %0.1f\n",num1,signval,num2,num3);
        printf("Your answer:\n");
        scanf("%f",&answer);
        if (answer == result){
            score++;
            printf("Correct!\n");
        }

    }
    
    
    default:
        break;
    }
}
