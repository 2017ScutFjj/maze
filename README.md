# maze
#include "stdafx.h"
#include <iostream>
#include <cstdlib>
#include <conio.h>
#include <string>
#include <time.h>
using namespace std;

int main()
{
	while (true)
	{
		srand((unsigned)time(NULL));
		int m1, n1, r;
		int win = 0;
		cout << " please input the size of the maze\n";
		cout << " [30 x 30 maybe the best :) ]\n";
		cout << " length:";
		cin >> m1;
		cout << " width:";
		cin >> n1;
		const int m = m1;
		const int n = n1;
		string ** a;  //save the maze
		a = new string *[m];
		for (int c = 0; c < m; c++)
		{
			a[c] = new string[n];
		}
		for (int i = 0; i < m; i++)  //create the maze(1)
		{
			for (int j = 0; j < n; j++)
			{
				if (i == 0)
				{
					a[i][j] = " *";
					continue;
				}
				else if (i == m - 1)
				{
					a[i][j] = " *";
					continue;
				}
				else if (j == 0)
				{
					a[i][j] = " *";
					continue;
				}
				else if (j == n - 1)
				{
					a[i][j] = " *";
					continue;
				}
				else
				{
					r = rand() % 2;
					if (r == 0)
						a[i][j] = "  ";
					else
						a[i][j] = " *";
				}
			}
		}
		r = rand() % (m - 2) + 1;
		int x1 = r;  // entrance's Y axis
		int y1 = 0;  // entrance's X axis
		a[x1][y1] = ">>";  // entrance's coordinate
		r = rand() % (m - 2) + 1;
		int x2 = r;  // exit's Y axis
		int y2 = n - 1;  // exit's X axis
		a[x2][y2] = ">>";  // exit's coordinate
		a[x2][y2 - 1] = "  ";
		a[x2][y2 - 2] = "  ";
		if (x2 != 1)
		{
			a[x2 - 1][y2 - 2] = "  ";
			a[x2 - 1][y2 - 3] = "  ";
			a[x2 - 1][y2 - 4] = "  ";
			if (x2 != 2)
			{
				a[x2 - 2][y2 - 2] = "  ";
				a[x2 - 2][y2 - 3] = "  ";
				a[x2 - 2][y2 - 4] = "  ";
				a[x2 - 1][y2 - 4] = "  ";
				a[x2 - 1][y2 - 5] = "  ";
				a[x2 - 1][y2 - 5] = "  ";
			}
		}
		if (x2 != m - 2)
		{
			a[x2 + 1][y2 - 2] = "  ";
			a[x2 + 1][y2 - 3] = "  ";
			a[x2 + 1][y2 - 4] = "  ";
		}
		int x3, y3;
		x3 = x1;
		y3 = y1 + 1;
		a[x3][y3] = "  ";
		int x4, y4;
		int t1 = 4 * (m + n) - 50;  // create some rules to create a nice maze
		int t2 = 0;
		int tw = 0;
		int ta = 0;
		int ts = 0;
		int td = 0;
		int t3 = t1 / 4 + 1;
		while (true)  // create the maze(2)
		{
			r = rand() % 4;
			if (t2 < t1)
			{
				r = rand() % 4;
				switch (r)
				{
				case 0:
					if (tw <= t3)
					{
						tw++;
						r = rand() % 2 + 2;
						x4 = x3;
						x3 -= r;
						if (x3 <= 0)
						{
							x3 = 1;
							a[x3][y3] = "  ";
							for (int q = x4 - 1; q > x3; q--)
								a[q][y3] = "  ";
							t2++;
							continue;
						}
						else
						{
							a[x3][y3] = "  ";
							for (int q = x4 - 1; q > x3; q--)
								a[q][y3] = "  ";
							t2++;
							continue;
						}
					}
					continue;
				case 1:
					if (ta <= t3)
					{
						ta++;
						r = rand() % 2 + 2;
						y4 = y3;
						y3 -= r;
						if (y3 <= 0)
						{
							y3 = 1;
							a[x3][y3] = "  ";
							for (int q = y4 - 1; q > y3; q--)
								a[x3][q] = "  ";
							t2++;
							continue;
						}
						else
						{
							a[x3][y3] = "  ";
							for (int q = y4 - 1; q > y3; q--)
								a[x3][q] = "  ";
							t2++;
							continue;
						}
					}
					continue;
				case 2:
					if (ts <= t3)
					{
						ts++;
						r = rand() % 2 + 2;
						x4 = x3;
						x3 += r;
						if (x3 >= m - 1)
						{
							x3 = m - 2;
							a[x3][y3] = "  ";
							for (int q = x4 + 1; q < x3; q++)
								a[q][y3] = "  ";
							t2++;
							continue;
						}
						else
						{
							a[x3][y3] = "  ";
							for (int q = x4 + 1; q < x3; q++)
								a[q][y3] = "  ";
							t2++;
							continue;
						}
					}
					continue;
				case 3:
					if (td <= t3)
					{
						td++;
						r = rand() % 2 + 2;
						y4 = y3;
						y3 += r;
						if (y3 >= n - 1)
						{
							y3 = n - 2;
							a[x3][y3] = "  ";
							for (int q = y4 + 1; q < y3; q++)
								a[x3][q] = "  ";
							t2++;
							continue;
						}
						else
						{
							a[x3][y3] = "  ";
							for (int q = y4 + 1; q < y3; q++)
								a[x3][q] = "  ";
							t2++;
							continue;
						}
					}
					continue;
				default:
					continue;
				}
			}
			else
				break;
		}
		int x = x1;
		int y = y1 + 1;
		a[x][y] = "0 ";
		char s;
		cout << " w <==> up\n";  // introduce how to control
		cout << " a <==> left\n";
		cout << " s <==> down\n";
		cout << " d <==> right\n";
		cout << " k <==> rebulid the maze\n";
		cout << " now please input any key to continue\n";
		s = _getch();
		while (true)
		{
			cout << " -";  // output the maze
			for (int o = 0; o < n - 1; o++)
			{
				cout << "--";
			}
			cout << "\n";
			for (int k = 0; k < n; k++)
			{
				for (int l = 0; l < n; l++)
				{
					cout << a[k][l];
				}
				cout << "\n";
			}
			cout << " -";
			for (int p = 0; p < n - 1; p++)
			{
				cout << "--";
			}
			cout << "\n";
			s = _getch();
			s = char(s);
			switch (s)  // get player's key
			{
			case 'w':
				if (a[x - 1][y] == " *")
				{
					system("cls");
					continue;
				}
				else
				{
					a[x][y] = "  ";
					x -= 1;
					a[x][y] = "0 ";
					system("cls");
					continue;
				}
			case 'a':
				if (a[x][y - 1] == " *")
				{
					system("cls");
					continue;
				}
				else
				{
					a[x][y] = "  ";
					y -= 1;
					a[x][y] = "0 ";
					system("cls");
					continue;
				}
			case 's':
				if (a[x + 1][y] == " *")
				{
					system("cls");
					continue;
				}
				else
				{
					a[x][y] = "  ";
					x += 1;
					a[x][y] = "0 ";
					system("cls");
					continue;
				}
			case 'd':
				if (a[x][y + 1] == " *")
				{
					system("cls");
					continue;
				}
				else
				{
					a[x][y] = "  ";
					y += 1;
					a[x][y] = "0 ";
					if (x == x2 && y == y2)
					{
						cout << " you pass the maze!\n";
						system("pause");
						for (int u = 0; u < m; u++)
							delete[] a[u];
						delete[]a;
						win = 1;  // judge do players pass the maze
						break;
					}
					system("cls");
					continue;
				}
			case 'k':
				break;
			default:
				continue;
			}
			break;
		}
		if (win == 1)
			break;
	}
    return 0;
}
