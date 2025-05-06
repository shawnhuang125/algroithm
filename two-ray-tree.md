# 二元樹
- **建立完全二元樹**
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
int main(){
	struct node* head = NULL;
	addnode(&head,3);
	addnode(&head,2);
	addnode(&head,1);
	addnode(&head,8);
	addnode(&head,6);
	PreOrdershowtree(head);
	printf("\n");
	PostOrdershowtree(head);
	printf("\n");
	InOrdershowtree(head);
	printf("\n");
	return 0;
} 
```
- **前置,中置與後置法印出完全二元樹**
```
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
```
### 二元搜尋樹
- **建立二元搜尋樹**
- 邏輯
	1. 如果data > head且子節點不為空那就繼續往右子節點造訪,直到右子節點的右子節點指標為空,創建新節點並填入data
  	2. 如果data < head且子節點不為空那就繼續往左子節點造訪,直到左子節點的左子節點指標為空,創建新節點並填入data
```
#include<stdio.h>
#include<stdlib.h>
struct node {
    int data;
    struct node* L;
    struct node* R;
};
struct node* addnode(struct node* head,int data){
    if(head == NULL){
        struct node* newnode = (struct node*)malloc(sizeof(struct node));
        newnode->data = data;
        newnode->L = NULL;
        newnode->R = NULL;
        return newnode;
    }
    if(data > head->data){//如果data>root就檢查右子節點是否為空
            head->R = addnode(head->R,data);
    }
    if(data < head->data){//如果data<root就檢查左子節點是否為空
            head->L = addnode(head->L,data);
    }
    return head;//從樹根更新整顆二元樹
}

int main(){
    struct node* root = NULL;//建立ROOT節點
    root = addnode(root,12);
    root = addnode(root,18);
    root = addnode(root,75);
    root = addnode(root,83);
    root = addnode(root,49);
    root = addnode(root,32);
    return 0;
```
- **建立查找指定值的函式**
```
void findout(struct node* head,int data){
    if(head==NULL){
        printf("no data here.\n");
        return;
    }  
    printf("Checking node: %d\n", head->data);
    if(head->data ==data){
        printf("find it.\n");//如果dat跟root的dat是一樣的就結束並輸出已找到
        return;
    }   
    if(head->data > data){
        findout(head->L,data); //如果data小於head節點的data那就繼續往左邊查找
    }else{
        findout(head->R,data);//如果data大於head節點的data那就繼續遞迴找右節點
    }
}
```
