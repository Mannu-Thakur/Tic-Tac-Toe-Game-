#include<iostream>
using namespace std;

char A[3][3] = {
    {'1', '2', '3'},
    {'4', '5', '6'},
    {'7', '8', '9'}
};
char turn = 'x';
int row, column;
bool draw = false;

void displayCode() {
    system("cls");  
    cout << "\n\n Tick Cross Game" << endl;
    cout << "\t\t Player1[X] \n \t\tPlayer2[O]" << endl;
    cout << " \t\t      |     |     " << endl;
    cout << " \t\t   " << A[0][0] << "  |  " << A[0][1] << "  |  " << A[0][2] << "  \n";
    cout << " \t\t _____|_____|_____" << endl;
    cout << " \t\t      |     |     " << endl;
    cout << " \t\t   " << A[1][0] << "  |  " << A[1][1] << "  |  " << A[1][2] << "  \n";
    cout << " \t\t _____|_____|_____" << endl;
    cout << " \t\t      |     |     " << endl;
    cout << " \t\t   " << A[2][0] << "  |  " << A[2][1] << "  |  " << A[2][2] << "  \n";
    cout << " \t\t      |     |     " << endl;
}

void playerTurn() {
    int choice;

    if (turn == 'x')
        cout << "Player1 [x] turn: ";
    else
        cout << "Player2 [0] turn: ";

    cin >> choice;

    switch (choice) {
        case 1: row = 0; column = 0; break;
        case 2: row = 0; column = 1; break;
        case 3: row = 0; column = 2; break;
        case 4: row = 1; column = 0; break;
        case 5: row = 1; column = 1; break;
        case 6: row = 1; column = 2; break;
        case 7: row = 2; column = 0; break;
        case 8: row = 2; column = 1; break;
        case 9: row = 2; column = 2; break;
        default:
            cout << "Invalid choice! Please try again." << endl;
            playerTurn();
            return;
    }

    if (A[row][column] != 'x' && A[row][column] != '0') {
        if (turn == 'x') {
            A[row][column] = 'x';
            turn = '0';
        } else {
            A[row][column] = '0';
            turn = 'x';
        }
    } else {
        cout << "Box already filled! Please try again." << endl;
        playerTurn(); 
    }

    displayCode();
}

bool gameOver() {
   
    for (int i = 0; i < 3; ++i) {
        if ((A[i][0] == A[i][1] && A[i][0] == A[i][2]) || (A[0][i] == A[1][i] && A[0][i] == A[2][i])) {
            return false;
        }
    }

    if ((A[0][0] == A[1][1] && A[0][0] == A[2][2]) || (A[0][2] == A[1][1] && A[0][2] == A[2][0])) {
        return false;
    }

    
    for (int i = 0; i < 3; ++i) {
        for (int j = 0; j < 3; ++j) {
            if (A[i][j] != 'x' && A[i][j] != '0') {
                return true;
            }
        }
    }

    draw = true;
    return false;
}

int main() {
    while (gameOver()) {
        displayCode();
        playerTurn();
    }

    if (turn == 'x' && !draw) {
        cout << "Player2 [0] wins!! Congrats!" << endl;
    } else if (turn == '0' && !draw) {
        cout << "Player1 [x] wins! Congrats!" << endl;
    } else {
        cout << "GAME DRAWN" << endl;
    }

    return 0;
}


