---
title: 백준 14442 벽 부수고 이동하기 2
published: 2025-09-08
author: siaa
description: 백준 14442번 문제를 풀었어요
image: ''
tags: [""]
category: 'Algo'
draft: false
---
## 1. 문제 내용
   - **문제**: n x m 크기의 행렬이 주어지면 최대 K번 벽을 뚫어 이동할 수 있습니다. 이때 최소경로를 구합니다.
   - **입력**: 행렬크기인 n과 m, 벽을 뚫을 수 있는 횟수 k, 그리고 n x m 크기의 맵이 입력 됩니다.
   - **출력**: 최소경로를 출력합니다.

## 2. 내생각
   문제를 읽어보니 그래프 탐색 문제 같아 BFS를 돌립니다.
   
   이때 q큐에 x좌표, y좌표, 현재까지 거리, 벽을 뚫은 횟수를 저장하기 위해 구조체를 만들어 BFS를 돌리면 최단 거리를 구할 수 있을 것 입니다.

## 3. 코드작성
   `f()`: 이 함수에서 BFS를 돌리고 결과를 저장합니다.
```C
#include<stdio.h>
#include<queue>
using namespace std;
int n,m,k,p=-1;
int a[1001][1001]={};
int visit[11][1001][1001]={};
int dx[4]={1,-1,0,0};
int dy[4]={0,0,1,-1};
typedef struct abc{
	int x; // x좌표
	int y; // y좌표
	int c; // 벽을 뚫은 횟수
	int v; // 현재까지 거리
};
queue<abc> q;
abc now,n2;
void f(){
	while(q.empty()==0){
		now = q.front();
		q.pop();
		if(now.x==n-1&&now.y==m-1){
			p=now.v;
			return;
		}
		for(int i=0;i<=3;i++){
			n2.x=now.x+dx[i];
			n2.y=now.y+dy[i];
			n2.c=now.c;
			n2.v=now.v+1;
			if(n2.x==n-1&&n2.y==m-1){
				p=n2.v;
				return;
			}
			if(n2.x>=0&&n2.x<n&&n2.y>=0&&n2.y<m){
				if(a[n2.x][n2.y]==0){
					if(visit[n2.c][n2.x][n2.y]==0){
						visit[n2.c][n2.x][n2.y]=1;
						q.push(n2);
					}
				}
				else{
					if(n2.c!=0){
						if(visit[n2.c][n2.x][n2.y]==0){
                            n2.c=n2.c-1;
							visit[n2.c][n2.x][n2.y]=1;
							q.push(n2);
						}
					}
				}
			}
		}
	}
	return;
}
int main(void){
	abc b;
	scanf("%d %d %d",&n,&m,&k);
	b.x=0;
	b.y=0;
	b.c=k;
	b.v=1;
	visit[b.c][0][0]=1;
	for(int i=0;i<=n-1;i++){
		for(int j=0;j<=m-1;j++){
			scanf("%1d",&a[i][j]);
		}
	}
	q.push(b);
	f();
	printf("%d",p);
}
```

## 4. 문제 발생
   -**문제**: 시간 초과가 발생했습니다. queue에 계속 값이 들어가 생긴 문제인 것 같습니다.
   -**해결책**: `visit[][][]`배열에서 중복이 잘걸렸는지 확인합니다.

## 5. 코드 수정
   44행에서 **n2.c**의 값을 `visit[][][]`에서 중복 확인을 한 후 바꾸어서 생긴 문제 였습니다.

   그래서 **n2.c**의 값을 바꾼후 중복확인을 하도록 수정 했습니다.
```c
#include<stdio.h>
#include<queue>
using namespace std;
int n,m,k,p=-1;
typedef struct abc{
	int x;
	int y;
	int c;
	int v;
};
int a[1001][1001]={};
int visit[11][1001][1001]={};
int dx[4]={1,-1,0,0};
int dy[4]={0,0,1,-1};
queue<abc> q;
abc now,n2;
void f(){
	while(q.empty()==0){
		now = q.front();
		q.pop();
		if(now.x==n-1&&now.y==m-1){
			p=now.v;
			return;
		}
		for(int i=0;i<=3;i++){
			n2.x=now.x+dx[i];
			n2.y=now.y+dy[i];
			n2.c=now.c;
			n2.v=now.v+1;
			if(n2.x==n-1&&n2.y==m-1){
				p=n2.v;
				return;
			}
			if(n2.x>=0&&n2.x<n&&n2.y>=0&&n2.y<m){
				if(a[n2.x][n2.y]==0){
					if(visit[n2.c][n2.x][n2.y]==0){
						visit[n2.c][n2.x][n2.y]=1;
						q.push(n2);
					}
				}
				else{
					if(n2.c!=0){
						n2.c=n2.c-1;
						if(visit[n2.c][n2.x][n2.y]==0){
							visit[n2.c][n2.x][n2.y]=1;
							q.push(n2);
						}
					}
				}
			}
		}
	}
	return;
}
int main(void){
	abc b;
	scanf("%d %d %d",&n,&m,&k);
	b.x=0;
	b.y=0;
	b.c=k;
	b.v=1;
	visit[b.c][0][0]=1;
	for(int i=0;i<=n-1;i++){
		for(int j=0;j<=m-1;j++){
			scanf("%1d",&a[i][j]);
		}
	}
	q.push(b);
	f();
	printf("%d",p);
}
```
   맞았습니다!!