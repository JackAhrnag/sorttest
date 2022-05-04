# 목차

<br>
<ol>
<li>내용 및 사건사고</li>
<li>정렬에 따른 성능 분석 결과</li>
<li>그에 따른 그래프</li>
<li>경우에 따른 성능 분석 결과</li>
<li>그에 따른 그래프</li>
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

---

출처

<br>

시간측정 : https://blog.naver.com/ahalinux/220886076413  
버블 : https://dojang.io/mod/page/view.php?id=637  
선택, 삽입, 쉘 : https://gmlwjd9405.github.io/tags#algorithm  
힙 : https://reakwon.tistory.com/43  
퀵 : https://code-lab1.tistory.com/23  
