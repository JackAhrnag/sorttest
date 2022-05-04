# 목차

<br>
<ol>
<li>내용 및 사건사고</li>
<li>정렬에 따른 성능 분석 결과</li>
<li>사용한 코드</li>
</ol>
<br>

###### 201901669 김현승

---

<br>

# 내용 및 사건사고

<br>

버블정렬, 선택정렬, 삽입정렬, 쉘정렬, 힙정렬, 퀵정렬의 성능을 분석 및 비교하는것이 이번 과제의 목적이다.  
그리고 성능을 분석하기 위해서는 우선 내가 직접 코드를 짜볼 필요가 있었다. 그리고 코드를 짜보았을 때 오류가 났다.

```

심각도	코드	설명	프로젝트	파일	줄	비표시 오류(Suppression) 상태	비표시 오류(Suppression) 상태
경고	C6262	함수에서 '65576'바이트의 스택을 사용하는데 이 크기가 /analyze:stacksize '16384'을(를) 초과합니다. 일부 데이터를 힙으로 이동하십시오.	컴퓨터알고리즘_201901669_김현승_버블시간측정	D:\대학 과제\컴퓨터알고리즘\컴퓨터알고리즘_201901669_김현승_버블시간측정\컴퓨터알고리즘_201901669_김현승_버블시간측정\소스.CPP	26		

```

오류라기 보다는 경고가 있었다. 디버깅을 하던 도중 코드가 멈췄는대, 뜬 오류나 경고는 이것 하나 뿐이기에 이것이 문제였을 것이라고 추측할 뿐이다.  
입력데이터 최대값을 2의 20승에서 2의 14승으로 줄였을 때 코드가 멈추는 일은 없었다. 때문에 기준값을 2의 14승으로 맞추고 분석하였다.

<br>

![예상결과](https://github.com/JackAhrnag/sorttest/blob/main/%EC%A0%95%EB%A0%AC%EC%97%90%20%EB%94%B0%EB%A5%B8%20%EC%98%88%EC%83%81%EC%8B%9C%EA%B0%84.jpg?raw=true)

<br>

알고리즘 시간 소비의 계산에 따른 예상결과는 위와 같다.

<br>

---

<br>

# '정렬'에 따른 성능 분석 결과

<br>

우선 입력데이터의 최소값을 2의 5승, 최대값을 2의 14승이라 정하고, 경우가 한 번 지나갈 때마다 1승이 늘어나는 방식으로 결과를 집계했다.  
또한 '입력데이터의 값이 정렬되어있는 경우', '입력데이터의 값이 무작위인 경우', '입력데이터의 값이 역정렬되어있는 경우' 들을 집계하였고, 집계데이터가 많으면 많을수록 결과값이 정확해진다 생각하여 하나의 경우당 3번씩 돌려보았다. 소수점은 기본 세자리 수 까지 집계했다. 그에따른 결과는 아래의 표와 같다.

<br>

![정렬에 따른 표](https://github.com/JackAhrnag/sorttest/blob/main/%EC%A0%95%EB%A0%AC%EC%97%90%20%EB%94%B0%EB%A5%B8%20%EC%8B%A4%EC%A0%9C%20%EC%86%8C%EB%B9%84%EC%8B%9C%EA%B0%84.jpg?raw=true)

<br>

그리고 위의 표에서 경우에 따른 평균을 낸 것이 아래와 같다.

<br>

![평균표](https://github.com/JackAhrnag/sorttest/blob/main/%EC%86%8C%EB%B9%84%20%EC%8B%9C%EA%B0%84%EC%9D%98%20%ED%8F%89%EA%B7%A0.jpg?raw=true)

<br>

위의 표를 눈대중으로 보았을 때  ``버블>선택>삽입>힙>쉘>퀵`` 순으로 평균적인 소비시간이 줄어든다는 것을 알 수 있고, 세가지 경우 중 역정렬이 무조건 가장 많은 시간을 소비하지는 않는다는 것을 알 수 있다. 이 결과는 위의 예상결과와는 다른 값을 보이는대, 아마 코드를 잘못짰을 수도 있다는 생각이 든다.

<br>

![image](https://user-images.githubusercontent.com/101371056/166661484-0dc37602-e31a-4bd6-b3aa-0259a5b3b428.png)

<br>

![image](https://user-images.githubusercontent.com/101371056/166661989-54f4fdb2-dab6-4865-bdc6-c762195c84f2.png)

<br>

평균적으로 퀵정렬이 가장 낮은 시간소비량을 나타내고 있으나, 선택정렬과 힙정렬이 경우에 따른 시간소비량이 그리 크게 차이가 나지 않는다는 것을 위의 그래프를 통해 알 수 있다.  
때문에 그래프만 보고 이를 분석하면 '어떻게든 가장 빠르게 문재를 해결해야 할 때' 는 퀵정렬로, '경우가 달라도 항상 일정한 빠르기를 원할 때'는 선택정렬과 힙정렬을(그 중에서도 힙정렬을)선택하면 된다는 것을 알아볼 수 있다.

---

<br>

# 사용한 코드

<br>

```
//
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

<br>

```
//선택
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <time.h>
#include <Windows.h>
# define SWAP(x, y, temp) ( (temp)=(x), (x)=(y), (y)=(temp) )
#define MAX_size 16384


void selection_sort(int list[], int n)
{
	int i, j, least, temp;

	for (i = 0; i < n - 1; i++)
	{
		least = i;

		for (j = i + 1; j < n; j++)
		{
			if (list[j] < list[least])
				least = j;
		}

		if (i != least)
		{
			SWAP(list[i], list[least], temp);
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

	//선택정렬(정렬이 되어있는 경우)
	printf("선택정렬(정렬o)\n");

	for (int i = 1; i <= 10; i++)
	{
		for (int j = 0; j < n; j++)
		{
			numArr[j] = j + 1;
		}

		start = clock();
		selection_sort(numArr, n);
		end = clock();

		res = (float)(end - start) / CLOCKS_PER_SEC;

		printf("2의 %d승 완료", i + 4);

		printf("\n걸린 시간 : %.3lf\n\n", res);

		n = n * 2;
	}
	n = 32;

	//선택정렬(정렬이 안되어있는 경우)
	printf("선택정렬(정렬x)\n");

	for (int i = 1; i <= 10; i++)
	{
		for (int j = 0; j < n; j++)
		{
			numArr[j] = rand();
		}

		start = clock();
		selection_sort(numArr, n);
		end = clock();

		res = (float)(end - start) / CLOCKS_PER_SEC;

		printf("2의 %d승 완료", i + 4);

		printf("\n걸린 시간 : %.3lf\n\n", res);

		n = n * 2;
	}
	n = 32;

	//선택정렬(역정렬이 되어있는 경우)
	printf("선택정렬(역정렬)\n");

	for (int i = 1; i <= 10; i++)
	{
		for (int j = 0; j < n; j++)
		{
			numArr[j] = n - j;
		}

		start = clock();
		selection_sort(numArr, n);
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

<br>

```
//삽입
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <time.h>
#include <Windows.h>
# define SWAP(x, y, temp) ( (temp)=(x), (x)=(y), (y)=(temp) )
#define MAX_size 16384


void insertion_sort(int list[], int n)
{
	int i, j, key;

	for (i = 1; i < n; i++)
	{
		key = list[i];

		for (j = i - 1; j >= 0 && list[j] > key; j--)
		{
			list[j + 1] = list[j];
		}

		list[j + 1] = key;
	}
}

int main()
{
	clock_t start, end;
	float res;
	int numArr[MAX_size];
	int n = 32;

	srand((unsigned int)time(NULL));

	//삽입정렬(정렬이 되어있는 경우)
	printf("삽입정렬(정렬o)\n");

	for (int i = 1; i <= 10; i++)
	{
		for (int j = 0; j < n; j++)
		{
			numArr[j] = j + 1;
		}

		start = clock();
		insertion_sort(numArr, n);
		end = clock();

		res = (float)(end - start) / CLOCKS_PER_SEC;

		printf("2의 %d승 완료", i + 4);

		printf("\n걸린 시간 : %.3lf\n\n", res);

		n = n * 2;
	}
	n = 32;

	//삽입정렬(정렬이 안되어있는 경우)
	printf("삽입정렬(정렬x)\n");

	for (int i = 1; i <= 10; i++)
	{
		for (int j = 0; j < n; j++)
		{
			numArr[j] = rand();
		}

		start = clock();
		insertion_sort(numArr, n);
		end = clock();

		res = (float)(end - start) / CLOCKS_PER_SEC;

		printf("2의 %d승 완료", i + 4);

		printf("\n걸린 시간 : %.3lf\n\n", res);

		n = n * 2;
	}
	n = 32;

	//삽입정렬(역정렬이 되어있는 경우)
	printf("삽입정렬(역정렬)\n");

	for (int i = 1; i <= 10; i++)
	{
		for (int j = 0; j < n; j++)
		{
			numArr[j] = n - j;
		}

		start = clock();
		insertion_sort(numArr, n);
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

<br>

```
/쉘
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <time.h>
#include <Windows.h>
# define SWAP(x, y, temp) ( (temp)=(x), (x)=(y), (y)=(temp) )
#define MAX_size 16384


void inc_insertion_sort(int list[], int first, int last, int gap)
{
	int i, j, key;

	for (i = first + gap; i <= last; i = i + gap)
	{
		key = list[i];

		for (j = i - gap; j >= first && list[j] > key; j = j - gap)
		{
			list[j + gap] = list[j];
		}

		list[j + gap] = key;
	}
}

void shell_sort(int list[], int n) {
	int i, gap;

	for (gap = n / 2; gap > 0; gap = gap / 2)
	{
		if ((gap % 2) == 0)
		{
			gap++;
		}

		for (i = 0; i < gap; i++)
		{
			inc_insertion_sort(list, i, n - 1, gap);
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

	//쉘정렬(정렬이 되어있는 경우)
	printf("쉘정렬(정렬o)\n");

	for (int i = 1; i <= 10; i++)
	{
		for (int j = 0; j < n; j++)
		{
			numArr[j] = j + 1;
		}

		start = clock();
		shell_sort(numArr, n);
		end = clock();

		res = (float)(end - start) / CLOCKS_PER_SEC;

		printf("2의 %d승 완료", i + 4);

		printf("\n걸린 시간 : %.3lf\n\n", res);

		n = n * 2;
	}
	n = 32;

	//쉘정렬(정렬이 안되어있는 경우)
	printf("쉘정렬(정렬x)\n");

	for (int i = 1; i <= 10; i++)
	{
		for (int j = 0; j < n; j++)
		{
			numArr[j] = rand();
		}

		start = clock();
		shell_sort(numArr, n);
		end = clock();

		res = (float)(end - start) / CLOCKS_PER_SEC;

		printf("2의 %d승 완료", i + 4);

		printf("\n걸린 시간 : %.3lf\n\n", res);

		n = n * 2;
	}
	n = 32;

	//쉘정렬(역정렬이 되어있는 경우)
	printf("쉘정렬(역정렬)\n");

	for (int i = 1; i <= 10; i++)
	{
		for (int j = 0; j < n; j++)
		{
			numArr[j] = n - j;
		}

		start = clock();
		shell_sort(numArr, n);
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

<br>

```
/
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <time.h>
#include <Windows.h>
# define SWAP(x, y, temp) ( (temp)=(x), (x)=(y), (y)=(temp) )
#define MAX_size 16384


void swap(int* a, int* b) {
	int temp = *a;
	*a = *b;
	*b = temp;
}
void heapify(int arr[], int here, int size) {
	int left = here * 2 + 1;
	int right = here * 2 + 2;
	int max = here;
	if (left < size && arr[left]>arr[max])
		max = left;
	if (right < size && arr[right]>arr[max])
		max = right;

	if (max != here) {
		swap(&arr[here], &arr[max]);
		heapify(arr, max, size);
	}
}

void buildHeap(int arr[], int size) {
	int i, j;
	for (i = size / 2 - 1; i >= 0; i--) {
		heapify(arr, i, size);
	}
}

void heap_sort(int arr[], int size) {
	int treeSize;
	buildHeap(arr, size);
	for (treeSize = size - 1; treeSize >= 0; treeSize--) {
		swap(&arr[0], &arr[treeSize]);
		heapify(arr, 0, treeSize);
	}
}

int main()
{
	clock_t start, end;
	float res;
	int numArr[MAX_size];
	int n = 32;

	srand((unsigned int)time(NULL));

	//힙정렬(정렬이 되어있는 경우)
	printf("힙정렬(정렬o)\n");

	for (int i = 1; i <= 10; i++)
	{
		for (int j = 0; j < n; j++)
		{
			numArr[j] = j + 1;
		}

		start = clock();
		heap_sort(numArr, n);
		end = clock();

		res = (float)(end - start) / CLOCKS_PER_SEC;

		printf("2의 %d승 완료", i + 4);

		printf("\n걸린 시간 : %.3lf\n\n", res);

		n = n * 2;
	}
	n = 32;

	//힙정렬(정렬이 안되어있는 경우)
	printf("힙정렬(정렬x)\n");

	for (int i = 1; i <= 10; i++)
	{
		for (int j = 0; j < n; j++)
		{
			numArr[j] = rand();
		}

		start = clock();
		heap_sort(numArr, n);
		end = clock();

		res = (float)(end - start) / CLOCKS_PER_SEC;

		printf("2의 %d승 완료", i + 4);

		printf("\n걸린 시간 : %.3lf\n\n", res);

		n = n * 2;
	}
	n = 32;

	//힙정렬(역정렬이 되어있는 경우)
	printf("힙정렬(역정렬)\n");

	for (int i = 1; i <= 10; i++)
	{
		for (int j = 0; j < n; j++)
		{
			numArr[j] = n - j;
		}

		start = clock();
		heap_sort(numArr, n);
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

<br>

```
//퀵
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <time.h>
#include <Windows.h>
# define SWAP(x, y, temp) ( (temp)=(x), (x)=(y), (y)=(temp) )
#define MAX_size 16384


void quick_sort(int arr[], int L, int R)
{
	int left = L, right = R;
	int pivot = arr[(L + R) / 2];
	int temp;
	do
	{
		while (arr[left] < pivot)
			left++;
		while (arr[right] > pivot)
			right--;
		if (left <= right)
		{
			temp = arr[left];
			arr[left] = arr[right];
			arr[right] = temp;
			left++;
			right--;
		}
	} while (left <= right);

	if (L < right)
		quick_sort(arr, L, right);

	if (left < R)
		quick_sort(arr, left, R);
}

int main()
{
	clock_t start, end;
	float res;
	int numArr[MAX_size];
	int n = 32;

	srand((unsigned int)time(NULL));

	//퀵정렬(정렬이 되어있는 경우)
	printf("퀵정렬(정렬o)\n");

	for (int i = 1; i <= 10; i++)
	{
		for (int j = 0; j < n; j++)
		{
			numArr[j] = j + 1;
		}

		start = clock();
		quick_sort(numArr, 0, n - 1);
		end = clock();

		res = (float)(end - start) / CLOCKS_PER_SEC;

		printf("2의 %d승 완료", i + 4);

		printf("\n걸린 시간 : %.3lf\n\n", res);

		n = n * 2;
	}
	n = 32;

	//퀵정렬(정렬이 안되어있는 경우)
	printf("퀵정렬(정렬x)\n");

	for (int i = 1; i <= 10; i++)
	{
		for (int j = 0; j < n; j++)
		{
			numArr[j] = rand();
		}

		start = clock();
		quick_sort(numArr, 0, n - 1);
		end = clock();

		res = (float)(end - start) / CLOCKS_PER_SEC;

		printf("2의 %d승 완료", i + 4);

		printf("\n걸린 시간 : %.3lf\n\n", res);

		n = n * 2;
	}
	n = 32;

	//퀵정렬(역정렬이 되어있는 경우)
	printf("퀵정렬(역정렬)\n");

	for (int i = 1; i <= 10; i++)
	{
		for (int j = 0; j < n; j++)
		{
			numArr[j] = n - j;
		}

		start = clock();
		quick_sort(numArr, 0, n - 1);
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
