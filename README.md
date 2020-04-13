#include <iostream>
#include <math.h>
using namespace std;
double niudun(double x1,double y1,double x2,double y2,double x)//牛顿插值公式代入
{
	double y = y1+((x-x1)*(y2-y1))/(x2-x1);
	return y;
}
int main()
{
	double yi[5][5];//定义第二个数组
	double er[10][10] = { 0 };//定义放大后数组
	for (int i = 0; i < 5; i++)//输入数组数据
	{
		for (int j = 0; j < 5; j++)
		{
			cin >> yi[i][j];
			er[2 * i][2 * j] = yi[i][j];
		}
	}
	for (int i = 0; i < 10; i++)
	{
		for (int j = 0; j < 10; j += 2)
		{
			if (er[i][j]== 0 && i != 9)
				er[i][j]=niudun(double(i - 1), er[i - 1][j], double(i + 1), er[i + 1][j], double(i));//内插
			if (er[i][j] == 0 && i == 9)
				er[i][j] = niudun(double(i - 2), er[i - 2][j], double(i -1), er[i - 1][j], double(i));//外插
		}
	}
	for (int i = 0; i < 10; i++)
	{
		for (int j = 0; j < 10; j++)
		{
			if (er[i][j] == 0 && i != 9)
				er[i][j] = niudun(double(j - 1), er[i ][j-1], double(j+1), er[i ][j+1], double(j));
			if (er[i][j] == 0 && i == 9)
				er[i][j] = niudun(double(j-2), er[i][j-2], double(j-1), er[i][j-1], double(j));
		}
	}
	for (int i = 0; i < 10; i++)//输出数据
	{
		for (int j = 0; j < 10; j++)
			cout << er[i][j] << " ";
		cout << endl;
	}
}
