### 二元樹實作
```
#include<stdlib.h>
#include<stdio.h>
struct node {
	int data;
	struct node* L;
	struct node* R;
};
struct node* createnode(int data){
	struct node* newnode = (struct node*)malloc(sizeof(struct node));
	if(newnode==NULL)	printf("memory allocate error.");
	newnode->data = data;
	newnode->L = NULL;
	newnode->R = NULL;
	return newnode;
}
struct node* addnode(struct node** head, int data){
	struct node* newnode = createnode(data);
	if(*head == NULL){
		//如果只有頭節點的情況 
		*head = newnode; 
	}else{
		//如果除了節點以外還有其他節點的情況 
		struct node* queue[100];
		int front=0,rear=0;
		queue[rear] = *head;//把root放進queue最裡面 
		rear++;//把rear加一代表有一個root在裡面 
		while(rear> front){
			struct node* current = queue[front++];//這裡是取出所以front要加一 
			if(current->L==NULL){
				current->L = newnode;
				return *head;
			}else{
				//如果有節點就造訪下一個
				queue[rear] = current->L;
				rear++; 
			}
			if(current->R==NULL){
				current->R = newnode;
				return *head;
			}else{
				queue[rear] = current->R;
				rear++;
			}
		}
	}
	return *head;
}
void showtree(struct node* head){
	struct node* queue[100];
		int front=0,rear=0;
		queue[rear++] = head;//把root放進queue最裡面 
		int level = 0;
		while(rear> front){
			int size = rear - front;//每一層的節點數量
			printf("Level %d: ", level);
			for(int i=0;i<size;i++){
				struct node* current = queue[front++];//這裡是取出所以front要加一 
				printf("%d ",current->data);
				if(current->L!=NULL){//左子節點一定會檢查 
					queue[rear++] = current->L;
				}
				if(current->R!=NULL){//右子節點一定會檢查 
					queue[rear++] = current->R;
				}
			} 
			printf("\n");
			level++;
		}
}
void PreOrdershowtree(struct node* head){
	if(head== NULL)	return;
	printf("%d, ",head->data);
	PreOrdershowtree(head->L);
	PreOrdershowtree(head->R);
} 
void PostOrdershowtree(struct node* head){
	if(head== NULL)	return;
	PostOrdershowtree(head->L);
	PostOrdershowtree(head->R);
	printf("%d, ",head->data);
}
void InOrdershowtree(struct node* head){
	if(head== NULL)	return;
	InOrdershowtree(head->L);
	printf("%d, ",head->data);
	InOrdershowtree(head->R);
}
int main(){
	struct node* head = NULL;
	addnode(&head,3);
	addnode(&head,2);
	addnode(&head,1);
	addnode(&head,8);
	addnode(&head,6);
	showtree(head);
	return 0;
} 
```
