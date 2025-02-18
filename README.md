# Algorithm
> 討論解決問題的方法論

> 介紹方法

### 練習1:輸入三個學生的國文英文數學資料,
  - 使用方法: 使用鏈結串列與結構陣列
  - 並輸出姓名,學號,各科成績及總分
  - 從小到大排列
  - 列出總分最高跟最低
  - 列出名次
- code(鏈結串列)
```
#include<stdio.h>
#include<stdlib.h>
struct node {
	char st_name;
	char st_id;
	int chinese;
	int english;
	int math;
	int total;
	struct node* next;
};
struct node* createnode(int subject, int data){
	int math,chinese,english;
	struct node* newnode = (struct node*)malloc(sizeof(struct node));
	if(newnode==NULL){
		printf("memory allocation error!\n");
	}
	newnode->math = 0;
    newnode->chinese = 0;
    newnode->english = 0;
	if(subject==math){
		printf("loading to add math\n");
		newnode->math = data;
	}else if(subject==chinese){
		printf("loading to add chinese\n");
		newnode->chinese = data;
	}else if(subject==english){
		printf("loading to add english\n");
		newnode->english = data;
	}
	newnode->next = NULL;
	return newnode;
}
struct node* addnode(struct node** head, char subject[10], int data){
	struct node* newnode = createnode(subject[10],data);
	if(*head==NULL){
		*head = newnode;
	}else{
		struct node* temp = *head;
		while(temp->next!=NULL){
			temp = temp->next;
		}
		*head = newnode;
	}
	return *head;
}
int showlink(struct node* head){
	struct node* temp = head;
	while(temp->next!=NULL){
		printf("student name: %s\tstudent ID: %s\tMath: %d\tEnglish: %d\tChinese: %d  --> \n",temp->st_name,temp->st_id,temp->math,temp->english,temp->chinese);
		temp = temp->next;
	}
	printf("\n");
	free(temp);
}

int main(){
	int insert,grade;
	char st_name[10],st_id[10],subject[10];
	struct node* head = NULL;
	while(insert!=5){
		printf("1.please insert student name and ID then the subject and the grade;\n2.show data;\n3.leave\n");
		printf("insert:");
		scanf("%d",&insert);
		if(insert == 1){
			printf("loading to insert student data\n");
        	printf("insert student name:");
        	scanf("%s", st_name); 
        	printf("inserted data:%s\n",st_name); 
        	printf("insert student ID:");
        	scanf("%s", st_id); 
        	printf("inserted data:%s\n",st_id); 
        	printf("choose an subject:");
        	scanf("%s",subject); 
        	printf("inserted data:%s\n",subject); 
        	printf("insert grade");
        	scanf("%d",&grade);
        	printf("inserted data:%d\n",grade);
			
			addnode(&head,subject,grade);
		}else if(insert == 2){
			showlink(head);
		}else if(insert == 3){
			printf("leaving....\n");
			break;
		}
		
	}
	return 0;
} 
```
- code(結構陣列):
```
#include<stdio.h>
#include<stdlib.h>
#define max 10
#define st_num 5
struct student {
    char st_name[max];
    char st_id[max];
    int chinese;
    int english;
    int math;
    int st_total;
    int st_average;

};
int main(){
    struct student students[st_num];
    int i,count=0;
    while(count <st_num){
        //最多輸入5個學生的資料
        printf("1. insert student data\n2. leave\nstudent max: %d\n",st_num);
        printf("please insert i:");
        scanf("%d",&i);
        if(i==1){
            //insert data
            printf("insert student name:");
            scanf("%s",students[count].st_name);
            printf("insert student ID:");
            scanf("%s",students[count].st_id);
            printf("insert student chinese grade:");
            scanf("%d",&students[count].chinese);
            printf("insert student English grade:");
            scanf("%d",&students[count].english);
            printf("insert student math grade:");
            scanf("%d",&students[count].math);
            students[count].st_total = students[count].chinese + students[count].english + students[count].math;
            students[count].st_average = (students[count].chinese + students[count].english + students[count].math)/3;
            count++;
        }else if(i==2){
            break;
        }else{
            printf("insert error!\n");
        }
    
    }
    
    //打印所有學生結果    
    for(int i = 0; i < count; i++) {
        printf("student name: %s\tstudent ID: %s\nstudent Chinese grade: %d\nstudent English grade: %d\nstudent Math grade: %d\nstudent total: %d\nstudent average: %d",
               students[i].st_name, students[i].st_id, students[i].chinese, students[i].english, students[i].math,students[i].st_total,students[i].st_average);
    }
    

    return 0;
}
```
