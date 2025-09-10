---
title: 백준 1999 최대최소
published: 2025-08-26
author: siaa
description: '백준문제를 풀었어요'
image: ''
tags: []
category: 'Algo'
draft: false
---
2025년 8월 25일 22시 27분 백준 1999번 최대최소 문제를 풀었습니다.

다음 글은 **문제내용 - 내 생각 - 코드작성 - 문제발생 - 코드수정**의 순으로 작성되었습니다.

## 1. 문제내용
   - **문제**: NxN 크기의 행렬에서 BxB 크기의 부분행렬의 최댓값과 최솟값의 차이를 묻는 질문에 답변을 합니다.
   - **입력**: 첫째줄에는 N,B,K가 입력됩니다. 다음 N개의 줄에는 행렬이 주어지고 K개의 줄에는 질문들이 주어집니다.
   - **출력**: 문제들의 답을 출력합니다.

## 2. 내 생각
   행렬을 두 개 더 만들어 각각의 행렬의 성분에 해당 위치에서의 최댓값, 최솟값을 저장해 전처리를 합니다.
   
   이후 질문들이 주어지면 질문에 해당하는 성분의 값을 가져와 출력합니다.

## 3. 코드작성
   `f1()`: 각 성분에 부분행렬의 최솟값을 저장합니다.


   `f2()`: 각 성분에 부분행렬의 최댓값을 저장합니다.


   이렇게 함수를 만들어 코드를 작성해 제출했습니다.
```c
#include<stdio.h>
int n,b,k;
int a[251][251]={}; // 초기 행렬
int d[251][251]={}; //최솟값 행렬
int c[251][251]={}; // 최댓값 행렬
int min(int a,int b){
	if(a>b){
		return b;
	}
	else{
		return a;
	}
}
int max(int a,int b){
	if(a>b){
		return a;
	}
	else{
		return b;
	}
}
void f1(){
	int t;
	for(int i=0;i<n;i++){
		for(int j=0;j<n;j++){
			t=a[i][j];
			for(int h=0+i;h<b+i;h++){
				for(int l=0+j;l<b+j;l++){
					if(h<n&&l<n){
						t=min(t,a[h][l]);
					}
				}
			}
			d[i][j]=t;
		}
	}
}
void f2(){
	int t;
	for(int i=0;i<n;i++){
		for(int j=0;j<n;j++){
			t=a[i][j];
			for(int h=0+i;h<b+i;h++){
				for(int l=0+j;l<b+j;l++){
					if(h<n&&l<n){
						t=max(t,a[h][l]);
					}
				}
			}
			c[i][j]=t;
		}
	}
}
int main(void){
	int p,q;
	scanf("%d %d %d",&n,&b,&k);
	for(int i=0;i<n;i++){
		for(int j=0;j<n;j++){
			scanf("%d",&a[i][j]);
		}
	}
	f1();
	f2();
	for(int i=0;i<k;i++){
		scanf("%d %d",&p,&q);
		printf("%d\n",c[p-1][q-1]-d[p-1][q-1]);
	}
}
```
## 5. 문제발생
   - **문제**: 제출을 했더니 59%에서 시간초과가 났습니다. 반복문을 4중으로 썼더니 시간초과가 난 것 같습니다.
   - **해결책**: 4중으로 된 반복문을 3중으로 줄이기 위해서 우선 각 행에서 B개 만큼씩 확인해 성분에 최댓값, 최솟값을 저장하고 다시 열마다 확인해 최종 최댓값, 최솟값을 저장합니다.

## 6. 코드수정
   각 함수의 반복문을 수정해 다시 작성하고 제출했습니다.
```c
#include<stdio.h>
int n,b,k;
int a[251][251]={}; // 초기 행렬
int d[251][251]={}; // 최종 최솟값 행렬
int dd[251][251]={}; // 중간 저장(최소)
int c[251][251]={}; // 최종 최댓값 행렬
int cc[251][251]={}; // 중간 저장(최대)
int min(int a,int b){
	if(a>b){
		return b;
	}
	else{
		return a;
	}
}
int max(int a,int b){
	if(a>b){
		return a;
	}
	else{
		return b;
	}
}
void f1(){
	int t,l;
	for(int i=0;i<n;i++){
		for(int j=0;j<n;j++){
			t=a[i][j];
			for(int h=0+j;h<b+j;h++){
				if(h<n){
					t=min(t,a[i][h]);
				}
			}
			dd[i][j]=t;
		}
	}
	for(int i=0;i<n;i++){
		for(int j=0;j<n;j++){
			l=dd[i][j];
			for(int h=0+i;h<b+i;h++){
				if(h<n){
					l=min(l,dd[h][j]);
				}
			}
			d[i][j]=l;
		}
	}
}
void f2(){
	int t,l;
	for(int i=0;i<n;i++){
		for(int j=0;j<n;j++){
			t=a[i][j];
			for(int h=0+j;h<b+j;h++){
				if(h<n){
					t=max(t,a[i][h]);
				}
			}
			cc[i][j]=t;
		}
	}
	for(int i=0;i<n;i++){
		for(int j=0;j<n;j++){
			l=cc[i][j];
			for(int h=0+i;h<b+i;h++){
				if(h<n){
					l=max(l,cc[h][j]);
				}
			}
			c[i][j]=l;
		}
	}
}
int main(void){
	int p,q;
	scanf("%d %d %d",&n,&b,&k);
	for(int i=0;i<n;i++){
		for(int j=0;j<n;j++){
			scanf("%d",&a[i][j]);
		}
	}
	f1();
	f2();
	for(int i=0;i<k;i++){
		scanf("%d %d",&p,&q);
		printf("%d\n",c[p-1][q-1]-d[p-1][q-1]);
	}
}
```
   맞았습니다!!