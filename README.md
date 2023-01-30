# find-numbers
#c
첫번째줄에 자연수 입력 그수만큼 숫자를 입력하고 두번째줄에 자연수 입력 그수만큼 숫자를 입력하고 두번째 줄과 첫번째 줄을 비교하면서 두번째 줄에 있는 수가 첫번째  줄에 있다면 1을 없다면 0을 출력하는 프로그램을 작성해보자! 
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
int i,j,n=0,a[100],N=0,A[100]; //내풀이  
int check(int A[],int a[],int j,int n){
	int i;
	for(i=0;i<n;i++){
		if(A[j]==a[i]){
			return 1;
		}
	}
	return 0;
}


int main(){
	int i,j,n=0,a[100],N=0,A[100];
	scanf("%d",&n);
	for(i=0;i<n;i++){
		scanf("%d ",&a[i]);
	}
	scanf("%d",&N);
	for(j=0;j<N;j++){
		scanf("%d",&A[j]);
	}
	j=0;
	while(1){
		if(j==N){
			break;
		}
		else{
		    check(A,a,j,n);
		    if(check(A,a,j,n) == 1){
			    printf("1\n");
				}
		    else{
			    printf("0\n");
				}
			j+=1;
		}
	}
	return 0;
}

#이진탐색트리를 이용해보자
특징
먼저, 루트 노드의 키와 찾고자 하는 값을 비교한다. 찾고자 하는 값이라면 탐색을 종료한다.
두번째, 찾고자 하는 값이 루트 노드의 키보다 작다면 왼쪽 서브 트리로 탐색을 진행한다.
세번째, 찾고자 하는 값이 루트노드의 키보다 크다면 오른쪽 서브트리로 탐색을 진행한다. 
위 과정을 찾고자 하는 값을 찾을 때까지 반복해서 진행한다. 
만약 값을 찾지 못한다면 그대로 종료한다.
typedef struct TreeNode {
	int data;
	struct TreeNode* left, * right;
}TreeNode;


TreeNode* inserts(TreeNode* node, int data)
{
	if (node == NULL){
		TreeNode* tmp = (TreeNode*)malloc(sizeof(TreeNode));
		tmp->data = data; tmp->left = tmp->right = NULL;
		return tmp;}
	if (data < node->data) node->left = inserts(node->left, data);
	else node->right = inserts(node->right, data);
	return node;
}


TreeNode* finds(TreeNode* node, int data)
{
	if (node == NULL) return NULL;
	if (node->data==data) return node;
	else if (node->data > data) return finds(node->left, data);
	else return finds(node->right, data);
}


int main()
{
	TreeNode* Root = NULL,*tmp = NULL;
	int i,n,m,data;
	scanf("%d", &n);
	for (i = 0; i < n; i++){
	scanf(" %d", &data);
	Root = inserts(Root, data);}
	scanf(" %d", &m);
	for (i = 0; i < m; i++){
		scanf(" %d", &data);
		tmp = finds(Root, data);
		if (tmp==NULL) printf("0\n");
		else printf("1\n");}
	return 0;
}
