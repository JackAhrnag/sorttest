```
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <time.h>
#include <Windows.h>
#define MAX_size 16384


void bubble_sort(int arr[], int count)
{
	int temp;

	for (int i = 0; i < count; i++)
	{
		for (int j = 0; j < count - 1; j++)
		{
			if (arr[j] > arr[j + 1])
			{
				temp = arr[j];
				arr[j] = arr[j + 1];
				arr[j + 1] = temp;
			}
		}
	}
}

int main()
{
	clock_t start, end;
	float res;
	int numArr[MAX_size];
	int n = 32;

	srand((unsigned int)time(NULL));

	//버블정렬(정렬이 되어있는 경우)
	printf("버블정렬(정렬o)\n");

	for (int i = 1; i <= 10; i++)
	{
		for (int j = 0; j < n; j++)
		{
			numArr[j] = j + 1;
		}

		start = clock();
		bubble_sort(numArr, n);
		end = clock();

		res = (float)(end - start) / CLOCKS_PER_SEC;

		printf("2의 %d승 완료", i + 4);

		printf("\n걸린 시간 : %.3lf\n\n", res);

		n = n * 2;
	}
	n = 32;

	//버블정렬(정렬이 안되어있는 경우)
	printf("버블정렬(정렬x)\n");

	for (int i = 1; i <= 10; i++)
	{
		for (int j = 0; j < n; j++)
		{
			numArr[j] = rand();
		}

		start = clock();
		bubble_sort(numArr, n);
		end = clock();

		res = (float)(end - start) / CLOCKS_PER_SEC;

		printf("2의 %d승 완료", i + 4);

		printf("\n걸린 시간 : %.3lf\n\n", res);

		n = n * 2;
	}
	n = 32;

	//버블정렬(역정렬이 되어있는 경우)
	printf("버블정렬(역정렬)\n");

	for (int i = 1; i <= 10; i++)
	{
		for (int j = 0; j < n; j++)
		{
			numArr[j] = n - j;
		}

		start = clock();
		bubble_sort(numArr, n);
		end = clock();

		res = (float)(end - start) / CLOCKS_PER_SEC;

		printf("2의 %d승 완료", i + 4);

		printf("\n걸린 시간 : %.3lf\n\n", res);

		n = n * 2;
	}
	n = 32;

	return 0;
}
```

---

출처

<br>

시간측정 : https://blog.naver.com/ahalinux/220886076413
버블 : https://dojang.io/mod/page/view.php?id=637  
선택, 삽입, 쉘 : https://gmlwjd9405.github.io/tags#algorithm
힙 : https://reakwon.tistory.com/43
퀵 : https://code-lab1.tistory.com/23
