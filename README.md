// swapnil ingale
// jspm wagholi
// cse 2025

#include <bits/stdc++.h>
#include <iostream>
#include <stdlib.h>
#include <time.h>
using namespace std;
int pos[2];
int mat[3][3];
int k = 0;
string name;
int flag;

void matrix_genrate()
{

    int n = 8;
    int num[n], i, j;

    for (i = 0; i < n; ++i)
    {
        num[i] = i + 1;
    }

    srand(time(NULL));

    int lastIndex = n - 1, index;

    for (int i = 0; i < 3; ++i)
    {
        for (int j = 0; j < 3; ++j)
        {
            if (lastIndex >= 0)
            {
                index = rand() % (lastIndex + 1);

                mat[i][j] = num[index];

                num[index] = num[lastIndex--];
            }
        }
    }

    mat[3 - 1][3 - 1] = 0;

    for (int i = 0; i < 3; i++)
    {
        for (int j = 0; j < 3; j++)
        {
            cout << mat[i][j] << "  ";
        }

        cout << endl;
    }
}
void position(int arr[][3], int n)
{
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < n; ++j)
        {
            if (arr[i][j] == 0)
            {
                pos[0] = i;
                pos[1] = j;
            }
        }
    }
}

void print(int mat[][3], int n)
{
    for (int i = 0; i < n; ++i)
    {
        for (int j = 0; j < n; ++j)
        {
            cout << mat[i][j] << " ";
        }

        cout << endl;
    }
}

void play(int arr[][3], int n)
{
    char x;

    cout << "Enter button : ";
    cin >> x;

    switch (x)
    {
    case 'u':
        if (pos[0] >= 0 && pos[1] >= 0 && pos[0] < 3 && pos[1] < 3)
        {
            swap(mat[pos[0]][pos[1]], mat[pos[0] - 1][pos[1]]);
        }
        else
        {
            cout << "position is not in matrix" << endl;
        }

        break;

    case 'd':
        if (pos[0] >= 0 && pos[1] >= 0 && pos[0] < 3 && pos[1] < 3)
        {
            swap(mat[pos[0]][pos[1]], mat[pos[0] + 1][pos[1]]);
        }
        else
        {
            cout << "position is not in matrix" << endl;
        }

        break;

    case 'l':
        if (pos[0] >= 0 && pos[1] >= 0 && pos[0] < 3 && pos[1] < 3)
        {
            swap(mat[pos[0]][pos[1]], mat[pos[0]][pos[1] - 1]);
        }
        else
        {
            cout << "position is not in matrix" << endl;
        }

        break;

    case 'r':
        if (pos[0] >= 0 && pos[1] >= 0 && pos[0] < 3 && pos[1] < 3)
        {
            swap(mat[pos[0]][pos[1]], mat[pos[0]][pos[1] + 1]);
        }
        else
        {
            cout << "position is not in matrix" << endl;
        }

        break;

    default:
        if (x != 'u' && x != 'r' && x != 'd' && x != 'l')
        {
            k++;

            cout << endl;

            cout << name << " you are enter wrong button : " << k << " times out of 3" << endl
                 << endl;

            if (k == 3)
            {
                exit(0);
            }
        }
    }
}

int cheack_win(int mat[][3], int n)
{
    int i, j;
    i = 0;

    while (i < n)
    {
        j = 0;
        while (j < n)
        {
            if (mat[i][j] > mat[i][j + 1] && j < n - 1)
            {
                // cout << "fir" << i << j << endl;
                return 0;
            }

            if (j == (n - 1))
            {
                if (mat[i][j] > mat[i + 1][j - 2] && i != n - 1)
                {
                  // cout << "sec" << i << j << endl;
                    return 0;
                }
            }

            j++;
        }

        i++;
    }

    return 1;
}

int main()
{
    cout << "Enter name : ";
    cin >> name;

    cout << endl;

    matrix_genrate();

    while (1)
    {
        position(mat, 3);
        cout << endl;
        // cout << pos[0] << " " << pos[1] << endl;

        play(mat, 3);
        cout << endl;
        print(mat, 3);
        flag = cheack_win(mat, 3);

        if (flag == 1)
        {
            cout << endl <<  name << " you win " << endl << endl;
            exit(0);
        }
        else
        {
           // cout << name << " you loss " << endl;
           // exit(0);
        }
    }

    return 0;
}
