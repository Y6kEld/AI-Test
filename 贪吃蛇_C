#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#include <windows.h>
#include <conio.h>

#define WIDTH 20
#define HEIGHT 20

typedef struct {
    int x;
    int y;
} Point;

Point snake[100];
int snakeLength = 1;
Point food;
int direction = 1;  // 1:right, 2:left, 3:up, 4:down

void gotoxy(int x, int y) {
    COORD coord;
    coord.X = x;
    coord.Y = y;
    SetConsoleCursorPosition(GetStdHandle(STD_OUTPUT_HANDLE), coord);
}

void drawBoard() {
    for (int i = 0; i < WIDTH; i++) {
        printf("#");
    }
    printf("\n");

    for (int i = 0; i < HEIGHT - 2; i++) {
        printf("#");
        for (int j = 0; j < WIDTH - 2; j++) {
            int isSnake = 0;
            for (int k = 0; k < snakeLength; k++) {
                if (snake[k].x == j && snake[k].y == i) {
                    printf("O");
                    isSnake = 1;
                    break;
                }
            }
            if (!isSnake) {
                if (food.x == j && food.y == i) {
                    printf("F");
                } else {
                    printf(" ");
                }
            }
        }
        printf("#\n");
    }

    for (int i = 0; i < WIDTH; i++) {
        printf("#");
    }
    printf("\n");
}

void generateFood() {
    srand(time(NULL));
    food.x = rand() % (WIDTH - 2);
    food.y = rand() % (HEIGHT - 2);
}

void moveSnake() {
    for (int i = snakeLength - 1; i > 0; i--) {
        snake[i] = snake[i - 1];
    }

    switch (direction) {
        case 1:
            snake[0].x++;
            break;
        case 2:
            snake[0].x--;
            break;
        case 3:
            snake[0].y--;
            break;
        case 4:
            snake[0].y++;
            break;
    }

    if (snake[0].x == food.x && snake[0].y == food.y) {
        snakeLength++;
        generateFood();
    }
}

int checkCollision() {
    if (snake[0].x < 0 || snake[0].x >= WIDTH - 2 || snake[0].y < 0 || snake[0].y >= HEIGHT - 2) {
        return 1;
    }
    for (int i = 1; i < snakeLength; i++) {
        if (snake[0].x == snake[i].x && snake[0].y == snake[i].y) {
            return 1;
        }
    }
    return 0;
}

void changeDirection() {
    if (kbhit()) {
        char ch = getch();
        switch (ch) {
            case 'd':
                if (direction != 2) direction = 1;
                break;
            case 'a':
                if (direction != 1) direction = 2;
                break;
            case 'w':
                if (direction != 4) direction = 3;
                break;
            case 's':
                if (direction != 3) direction = 4;
                break;
        }
    }
}

int main() {
    snake[0].x = 5;
    snake[0].y = 5;
    generateFood();

    while (1) {
        system("cls");
        drawBoard();
        moveSnake();
        if (checkCollision()) {
            printf("Game Over!\n");
            break;
        }
        changeDirection();
        Sleep(100);
    }

    return 0;
}    
