INPUT CODE :
```cppp
#include <iostream>
using namespace std;

class Game {
private:
    char board[3][3];
    char turn;

public:
    Game() { resetGame(); }

    void resetGame() {
        char ch = '1';
        for(int i=0;i<3;i++)
            for(int j=0;j<3;j++)
                board[i][j] = ch++;
        turn = 'X';
    }

    void printBoard() {
        cout << "\n";
        for(int i=0;i<3;i++) {
            for(int j=0;j<3;j++)
                cout << board[i][j] << " ";
            cout << endl;
        }
    }

    bool makeMove(int choice) {
        int r = (choice-1)/3;
        int c = (choice-1)%3;

        if(board[r][c] != 'X' && board[r][c] != 'O') {
            board[r][c] = turn;
            return true;
        }
        return false;
    }

    bool checkWinner() {
        // rows & cols
        for(int i=0;i<3;i++) {
            if(board[i][0]==board[i][1] && board[i][1]==board[i][2])
                return true;
            if(board[0][i]==board[1][i] && board[1][i]==board[2][i])
                return true;
        }
        // diagonals
        if(board[0][0]==board[1][1] && board[1][1]==board[2][2])
            return true;
        if(board[0][2]==board[1][1] && board[1][1]==board[2][0])
            return true;

        return false;
    }

    void switchTurn() {
        turn = (turn == 'X') ? 'O' : 'X';
    }

    char getTurn() { return turn; }
};

int main() {
    Game g;
    int choice, moves = 0;

    while(true) {
        g.printBoard();
        cout << "\nPlayer " << g.getTurn() << ", enter position: ";
        cin >> choice;

        if(!g.makeMove(choice)) {
            cout << "Invalid move! Try again.\n";
            continue;
        }

        moves++;

        if(g.checkWinner()) {
            g.printBoard();
            cout << "\nPlayer " << g.getTurn() << " wins!\n";
            break;
        }

        if(moves == 9) {
            g.printBoard();
            cout << "\nGame Draw!\n";
            break;
        }

        g.switchTurn();
    }

    return 0;
}
```
OUTPUT:
1 2 3
4 5 6
7 8 9

Player X, enter position: 1
Player O, enter position: 5
Player X, enter position: 2
Player O, enter position: 8
Player X, enter position: 3

1 2 3
4 5 6
7 8 9

Player X, enter position: 1

X 2 3
4 5 6
7 8 9

Player O, enter position: 5

X 2 3
4 O 6
7 8 9

Player X, enter position: 2

X X 3
4 O 6
7 8 9

Player O, enter position: 8

X X 3
4 O 6
7 O 9

Player X, enter position: 3

X X X
4 O 6
7 O 9

Player X wins!
