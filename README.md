#include <stdio.h>
#include <iostream>
#include <cstdlib>
#include <string.h>
#define _CRT_NO_WARNINGS
using namespace std;

int find_N(char* str, const char* fnd)
{
	int N = -1;
	for (int i = 0; i < int(strlen(str)); i++)
	{
		for (int j = 0; j < int(strlen(fnd)); j++)
		{
			if (j == strlen(fnd) - 1 && str[i + j] == fnd[j])
			{
				N = i;
				break;
			}
			if (str[i + j] == fnd[j])
			{
				continue;
			}
			else
			{
				break;
			}
		}
		if (N == i)
		{
			break;
		}
	}
	return N;
}

void sorting(char* str)
{
	const char rome_nums[8] = { 'M', 'D', 'C', 'L', 'X', 'V', 'I', '\0' };
	int begin = 0;
	int temporary = 0;
	for (int i = 0; i < int(strlen(rome_nums)); i++)
	{
		for (int j = 0; j < int(strlen(str)); j++)
		{
			if (str[j] != rome_nums[i])
			{
				continue;
			}
			if (j == 0 || str[j - 1] == rome_nums[i])
			{
				begin++;
				continue;
			}
			for (int k = j; k > begin; k--)
			{
				temporary = str[k];
				str[k] = str[k - 1];
				str[k - 1] = temporary;
			}
			begin++;
		}
	}
}

void reverse(char* str)
{
	for (int u = 0; u < int(strlen(str)) / 2; u++)
	{
		char temp;
		temp = str[u];
		str[u] = str[strlen(str) - u - 1];
		str[strlen(str) - u - 1] = temp;
	}
}

void zamena(char* str, const char* fnd, const char* chng, char* tmp)
{
	char str_c[100] = { 0 };
	str_c[0] = '\0';
	for (int i = 0; i < int(strlen(str)); i++)
	{
		str_c[i] = str[i];
	}
	int N = find_N(str_c, fnd);
	if (N == -1)
	{
		tmp[0] = 'q';
		return;
	}
	char end[100] = { 0 };
	end[0] = '\0';
	int end_check = strlen(str_c) - N - strlen(fnd);
	if (end_check > 0)
	{
		strcpy_s(end, 100, str_c);
		reverse(end);
		end[end_check] = '\0';
		reverse(end);
	}
	str_c[N] = '\0';
	strcat_s(str_c, 100, chng);
	if (end_check > 0)
	{
		strcat_s(str_c, 100, end);
	}
	for (int a = 0; a < int(strlen(str_c)); a++)
	{
		str[a] = str_c[a];
	}
	str[strlen(str_c)] = '\0';
}
void summa(char* x1, char* x2, char* tmp)
{
	int counter = 1;
	while (counter != 0)
	{
		zamena(x1, "IV", "IIII", tmp);
		zamena(x1, "IX", "VIIII", tmp);
		zamena(x1, "XL", "XXXX", tmp);
		zamena(x1, "XC", "LXXXX", tmp);
		zamena(x1, "CD", "CCCC", tmp);
		zamena(x1, "CM", "DCCCC", tmp);
		zamena(x2, "IV", "IIII", tmp);
		zamena(x2, "IX", "VIIII", tmp);
		zamena(x2, "XL", "XXXX", tmp);
		zamena(x2, "XC", "LXXXX", tmp);
		zamena(x2, "CD", "CCCC", tmp);
		zamena(x2, "CM", "DCCCC", tmp);

		zamena(x1, "M", "DD", tmp);
		zamena(x1, "D", "CCCCC", tmp);
		zamena(x1, "C", "LL", tmp);
		zamena(x1, "L", "XXXXX", tmp);
		zamena(x1, "X", "VV", tmp);
		zamena(x1, "V", "IIIII", tmp);
		zamena(x2, "M", "DD", tmp);
		zamena(x2, "D", "CCCCC", tmp);
		zamena(x2, "C", "LL", tmp);
		zamena(x2, "L", "XXXXX", tmp);
		zamena(x2, "X", "VV", tmp);
		zamena(x2, "V", "IIIII", tmp);
		counter++;

		strcat(x1, x2);

		sorting(x1);
		tmp[0] = 'f';
		while (counter != 0) { zamena(x1, "IIIII", "V", tmp); if (tmp[0] == 'q') { counter = 0; } }
		counter++; tmp[0] = 'f';
		while (counter != 0) { zamena(x1, "VV", "X", tmp); if (tmp[0] == 'q') { counter = 0; } }
		counter++; tmp[0] = 'f';
		while (counter != 0) { zamena(x1, "XXXXX", "L", tmp); if (tmp[0] == 'q') { counter = 0; } }
		counter++; tmp[0] = 'f';
		while (counter != 0) { zamena(x1, "LL", "C", tmp); if (tmp[0] == 'q') { counter = 0; } }
		counter++; tmp[0] = 'f';
		while (counter != 0) { zamena(x1, "CCCCC", "D", tmp); if (tmp[0] == 'q') { counter = 0; } }
		counter++; tmp[0] = 'f';
		while (counter != 0) { zamena(x1, "DD", "M", tmp); if (tmp[0] == 'q') { counter = 0; } }
		counter++; tmp[0] = 'f';
		while(counter != 0) {zamena(x1, "VIIII", "IX", tmp); if (tmp[0] == 'q') { counter = 0; } }
		counter++; tmp[0] = 'f'; /////////////////////////////////////////////garjgraoihihrianhh
		while (counter != 0) { zamena(x1, "IIII", "IV", tmp); if (tmp[0] == 'q') { counter = 0; } }
		counter++; tmp[0] = 'f';
		while (counter != 0) { zamena(x1, "LXXXX", "XC", tmp); if (tmp[0] == 'q') { counter = 0; } }
		counter++; tmp[0] = 'f';
		while (counter != 0) { zamena(x1, "XXXX", "XL", tmp); if (tmp[0] == 'q') { counter = 0; } }
		counter++; tmp[0] = 'f';
		while (counter != 0) { zamena(x1, "DCCCC", "CM", tmp); if (tmp[0] == 'q') { counter = 0; } }
		counter++; tmp[0] = 'f';
		while (counter != 0) { zamena(x1, "CCCC", "CD", tmp); if (tmp[0] == 'q') { counter = 0; } }
	}
}

int check(char* x1, char* x2)
{
	int checker = 0;
	int temp1 = 0;
	int temp2 = 0;
	int temp3 = 0;
	int temp4 = 0;
	const char rome_nums[8] = { 'M', 'D', 'C', 'L', 'X', 'V', 'I', '\0' };
	// ПРОВЕРКА ПРОСТО ЧТО ВСЕ СИМВОЛЫ   _ РИМСКИЕ ЗНАКИ
	
	for (int i = 0; i<int(strlen(x1)); i++)
	{
		checker = 0;
		for (int j = 0; j<int(strlen(rome_nums)); j++)
		{
			if (x1[i] == rome_nums[j])
			{
				checker++;
			}
		}
		if (checker == 0) return 0;
	}
	checker = 0;
	for (int i = 0; i<int(strlen(x2)); i++)
	{
		checker = 0;
		for (int j = 0; j<int(strlen(rome_nums)); j++)
		{
			if (x2[i] == rome_nums[j])
			{
				checker++;
			}
		}
		if (checker == 0) return 0;
	}
	// x1
	checker = 0;
	int checker2 = 0;
	int checker3 = 0;
	int checker4 = 0;
	int checker5 = 0;

	for (int i = 0; i < int(strlen(x1)); i++)
	{
		if (x1[i] == 'I')
		{
			for (int j = i + 2; j < int(strlen(x1)); j++)
			{
				if (x1[j] == 'V' || x1[j] == 'X' || x1[j] == 'L' || x1[j] == 'C' || x1[j] == 'D' || x1[j] == 'M')
				{
					return 0;
				}
		    }
		}
		if (x1[i] == 'V')
		{
			for (int j = i + 2; j < int(strlen(x1)); j++)
			{
				if(x1[j] == 'X' || x1[j] == 'L' || x1[j] == 'C' || x1[j] == 'D' || x1[j] == 'M')
				{
					return 0;
				}
			}
		}
		if (x1[i] == 'X')
		{
			for (int j = i + 2; j < int(strlen(x1)); j++)
			{
				if (x1[j] == 'L' || x1[j] == 'C' || x1[j] == 'D' || x1[j] == 'M')
				{
					return 0;
				}
			}
		}
		if (x1[i] == 'L')
		{
			for (int j = i + 2; j < int(strlen(x1)); j++)
			{
				if (x1[j] == 'C' || x1[j] == 'D' || x1[j] == 'M')
				{
					return 0;
				}
			}
		}
		if (x1[i] == 'C')
		{
			for (int j = i + 2; j < int(strlen(x1)); j++)
			{
				if (x1[j] == 'D' || x1[j] == 'M')
				{
					return 0;
				}
			}
		}
	}
	
	if (x1[temp1] == 'I')
	{
		for (int i = 0; i<int(strlen(x1)); i++)
		{
			if (x1[i] != 'I')
			{
				while (x1[i])
				{
					if (x1[i] == 'I')
					{
						return 0;
					}
					i++;
				}
			}
		}
	}
	
	for (int i = 0; i<int(strlen(x1)); i++)
	{
		if (x1[i] == 'X' && (x1[i + 1] == 'D' || x1[i + 1] == 'M' ))
		{
			return 0;
		}
	} 
	
	for (int i = 0; i<int(strlen(x1)); i++)
	{
		if (x1[i] == 'V' && (x1[i + 1] == 'X' || x1[i + 1] == 'C' || x1[i + 1] == 'L' || x1[i + 1] == 'D' || x1[i + 1] == 'M'))
		{   
			return 0;
		}
	}
	checker2 = 0;
	checker5 = 0;
	
	for (int i = 0; i<int(strlen(x1)); i++)
	{
		if (x1[i] == 'I')
		{
			checker5 = i;
			checker5++;
			i++;
			for (int j = i; j < int(strlen(x1)); j++)
			{
				if ((x1[j] == 'L' || x1[j] == 'C' || x1[j] == 'D' || x1[j] == 'M') && checker5 != 0)
				{
					return 0;
				}
			}
		}
	}
	checker5 = 0;
	
	if (x1[temp1] != 'I')
	{
		for (int i = 1; i<int(strlen(x1)); i++)
		{
			if (x1[i] == 'I' && x1[i]==x1[i+1])
			{
				checker4++;
			}
			if (x1[i] == 'I' && x1[i] != x1[i + 1] && x1[i+1]!='\0')
			{
				if (checker4 > 0)
				{
					return 0;
				}
			}
		}
	}
	checker4 = 0;
	checker5 = 0;
	
	if (x1[temp1] == 'D')
	{
		int temp15 = temp1;
		for (int i = 1; i<int(strlen(x1)); i++)
		{
			if (x1[i] == 'D')
			{
				return 0;
			}
		}
	}
	if(x1[temp1]=='X')
	{ 
		int temp15 = temp1;
		while (x1[temp15] == 'X')
		{
			checker2++;
			temp15++;
			if ((x1[temp15 + 1] == 'D' || x1[temp15 + 1] == 'M' || x1[temp15 + 1] == 'C' ) && checker2 > 1)
			{
				return 0;
	     	}
	    }
    }
	for (int i = 0; i<int(strlen(x1)); i++)
	{
		if (x1[i]=='L' &&(x1[i+1] == 'C' || x1[i+1] == 'D' || x1[i] == 'M'))
		{
		 return 0;
		}
	}
	for (int i = 0; i<int(strlen(x1)); i++)
	{
		checker = 0;
		if (x1[i] == x1[i + 1])
		{
			temp2 = x1[i];
			checker++;
			temp3 = i;
			while (temp2 == x1[i + 1])
			{
				checker++;
				i++;
			}
		}
		if (checker >= 4 && (temp2 == 'I' || temp2 == 'X' || temp2 == 'C')) return 0;
		if (checker >= 2 && (temp2 == 'V' || temp2 == 'D' || temp2 == 'L')) return 0;
		if (x1[temp1] == 'V' && x1[temp1 + 1] != 'V')
		{
			for (int j = 1; j<int(strlen(x1)); j++)
			{
				if (x1[j] == 'V') return 0;
			}
		}
		if (x1[temp1] == 'L' && x1[temp1 + 1] != 'L')
		{
			for (int j = 1; j<int(strlen(x1)); j++)
			{
				if (x1[j] == 'L') return 0;
			}
		}
		if (x1[temp1] == 'X' && x1[temp1 + 1] != 'X')
		{
			for (int j = 1; j<int(strlen(x1)); j++)
			{
				if (x1[j] == 'X') return 0;
			}
		}
		if (x1[temp1] == 'I' && x1[temp1 + 1] == 'I' && x1[temp1 + 2] != 'I') return 0;
	}
	//x2
	 checker = 0;
     checker2 = 0;
     checker3 = 0;
	 checker4 = 0;
	 checker5 = 0;
	 temp1 = 0;
     checker5 = 0;
	 for (int i = 0; i < int(strlen(x2)); i++)
	 {
		 if (x2[i] == 'I')
		 {
			 for (int j = i + 2; j < int(strlen(x1)); j++)
			 {
				 if (x2[j] == 'V' || x2[j] == 'X' || x2[j] == 'L' || x2[j] == 'C' || x2[j] == 'D' || x2[j] == 'M')
				 {
					 return 0;
				 }
			 }
		 }
		 if (x2[i] == 'V')
		 {
			 for (int j = i + 2; j < int(strlen(x2)); j++)
			 {
				 if (x2[j] == 'X' || x2[j] == 'L' || x2[j] == 'C' || x2[j] == 'D' || x2[j] == 'M')
				 {
					 return 0;
				 }
			 }
		 }
		 if (x2[i] == 'X')
		 {
			 for (int j = i + 2; j < int(strlen(x2)); j++)
			 {
				 if (x2[j] == 'L' || x2[j] == 'C' || x2[j] == 'D' || x2[j] == 'M')
				 {
					 return 0;
				 }
			 }
		 }
		 if (x2[i] == 'L')
		 {
			 for (int j = i + 2; j < int(strlen(x2)); j++)
			 {
				 if (x2[j] == 'C' || x2[j] == 'D' || x2[j] == 'M')
				 {
					 return 0;
				 }
			 }
		 }
		 if (x2[i] == 'C')
		 {
			 for (int j = i + 2; j < int(strlen(x2)); j++)
			 {
				 if (x2[j] == 'D' || x2[j] == 'M')
				 {
					 return 0;
				 }
			 }
		 }
	 }
	 if (x2[temp1] == 'I')
	 {
		 for (int i = 0; i<int(strlen(x2)); i++)
		 {
			 if (x2[i] != 'I')
			 {
				 while (x2[i])
				 {
					 if (x2[i] == 'I')
					 {
						 return 0;
					 }
					 i++;
				 }
			 }
		 }
	 }
	 for (int i = 0; i<int(strlen(x2)); i++)
	 {
		 if (x2[i] == 'X' && (x2[i + 1] == 'D' || x2[i + 1] == 'M'))
		 {
			 return 0;
		 }
	 }
	 for (int i = 0; i<int(strlen(x2)); i++)
	 {
		 if (x2[i] == 'V' && (x2[i + 1] == 'X' || x2[i + 1] == 'C' || x2[i + 1]=='L' || x2[i+1]=='D' || x2[i+1]=='M'))
		 {
			 return 0; 
		 }
	 }

	for (int i = 0; i<int(strlen(x2)); i++)
		{
			 if (x2[i] == 'I')
			 {
				 checker5 = i;
				 checker5++;
				 i++;
				 for (int j = i; j < int(strlen(x2)); j++)
				 {
					 if ((x2[j] == 'L' || x2[j] == 'C' || x2[j] == 'D' || x2[j] == 'M') && checker5 != 0)
					 {
						 return 0;
					 }
				 }
			 }
		 }


	 if (x2[temp1] != 'I')
	 {
		 for (int i = 1; i<int(strlen(x2)); i++)
		 {
			 if (x2[i] == 'I' && x2[i] == x2[i + 1])
			 {
				 checker4++;
			 }
			 if (x2[i] == 'I' && x2[i] != x2[i + 1] && x2[i + 1] != '\0')
			 {
				 if (checker4 > 0)
				 {
					 return 0;
				 }
			 }
		 }
	 }
	 if (x2[temp1] == 'D')
	 {
		 for (int i = 1; i<int(strlen(x2)); i++)
		 {
			 if (x2[i] == 'D')
			 {
				 return 0;
			 }
		 }
	 }
	 if (x2[temp1] == 'X')
	{
		int temp15 = temp1;
		while (x2[temp15] == 'X')
		{
			checker2++;
			temp15++;
			if (x2[temp15 + 1] == 'D' || x2[temp15 + 1] == 'M' && checker2 > 1)
			{
				return 0;
			}
		}
	}
	 for (int i = 0; i<int(strlen(x2)); i++)
	 {
		if ((x2[i+1] == 'C' || x2[i+1] == 'D' || x2[i+1] == 'M') && x2[i]=='L')
	    {
		  return 0;
	    }
	 }
	 for (int i = 0; i<int(strlen(x2)); i++)
	{
		checker = 0;
		if (x2[i] == x2[i + 1])
		{
			temp2 = x2[i];
			checker++;
			temp3 = i;
			while (temp2 == x2[i + 1])
			{
				checker++;
				i++;
			}
		}
		if (checker >= 4 && (temp2 == 'I' || temp2 == 'X' || temp2 == 'C')) return 0;
		if (checker >= 2 && (temp2 == 'V' || temp2 == 'D' || temp2 == 'L')) return 0;
		if (x2[temp1] == 'V' && x2[temp1 + 1] != 'V')
		{
			for (int j = 1; j<int(strlen(x2)); j++)
			{
				if (x2[j] == 'V') return 0;
			}
		}
		if (x2[temp1] == 'L' && x2[temp1 + 1] != 'L')
		{
			for (int j = 1; j<int(strlen(x2)); j++)
			{
				if (x2[j] == 'L') return 0;
			}
		}
		if (x2[temp1] == 'X' && x2[temp1 + 1] != 'X')
		{
			for (int j = 1; j<int(strlen(x2)); j++)
			{
				if (x2[j] == 'X') return 0;
			}
		}
		if (x2[temp1] == 'I' && x2[temp1 + 1] == 'I' && x2[temp1 + 2] != 'I') return 0;
	}
	return 1;
}
int main()
{
loop:
	char tmp[3] = { 0 };
	tmp[0] = 'f';
	tmp[1] = '\0';
	setlocale(LC_ALL, "Russian");
	char x1[100];
	char x2[100];
	x1[0] = '\0';
	x2[0] = '\0';
	printf("Input first roman number: ");
	gets_s(x1);
	printf("\n");
	printf("Input second roman number: ");
	gets_s(x2);
	printf("\n");
	int u = 0;
	while (x1[u])
	{
		x1[u] = toupper(x1[u]);
		u++;
	}
	u = 0;
	while (x2[u])
	{
		x2[u] = toupper(x2[u]);
		u++;
	}
	if (check(x1, x2) == 0)
	{
		printf("Wrong entry\n");
		goto loop;
	}
	summa(x1, x2, tmp);
	printf("x1 + x2 = ");
	for (int l = 0; l < int(strlen(x1)); l++)
	{
		printf("%c", x1[l]);
	}
	printf("\n");
	printf("\n");
	int repeat = 123;
	printf("If you want to continue input 1, for exit anything (except 1) : ");
	scanf_s("%d", &repeat);
	printf("\n");
	getchar();
	if (repeat == 1)
	{
		goto loop;
	}
	else
	{
		return 0;
	}
}
