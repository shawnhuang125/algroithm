# pracetice1 code
### code(鏈結串列)不使用strdup
```
#include<stdio.h>
#include<stdlib.h>
#include<string.h>
struct node {
    char* st_name;
    char* st_id;
    int chinese;
    int english;
    int math;
    int total;
    struct node* next;

};
struct node* createnode(char* name, char* id, int chinese_grade, int english_grade, int math_grade){
    struct node* newnode = (struct node*)malloc(sizeof(struct node));
    // to check whether the node is created successfully
    if(newnode==NULL){
        printf("memory allocation failed!");
    }
    
    // insert student data inside the node
    newnode->st_name = name;
    newnode->st_id = id;
    newnode->chinese = chinese_grade;
    newnode->english = english_grade;
    newnode->math = math_grade;
    newnode->total = newnode->chinese+newnode->english+newnode->math;
    // intalize the point of the node to be NULL
    newnode->next = NULL;
    // return the hole newnode data
    return newnode;
}
struct node* addnode(struct node** head, char* name, char* id, int chinese_grade, int english_grade, int math_grade){
    struct node* newnode = createnode(name,id,chinese_grade,english_grade,math_grade);
    if(newnode==NULL){  printf("createnode failed");}
    // situation1: if the node is the head node
    if(*head==NULL){
        *head = newnode;
    }else{
        // situation2: if the node is not the head node
        struct node* temp = *head;
        while(temp->next!=NULL){
            temp = temp->next;
        }
        // add node after the last noe node
        temp->next = newnode;
    }
    return *head;
}
void printlink(struct node* head){
    struct node* temp = head;
    while(temp!=NULL){
        printf("student name: %s\tstudent ID: %s\nstudent chinese grade: %d\nstudent english grade: %d\nstudent Math grade: %d\nstudent total grade: %d\n",
            temp->st_name,temp->st_id,temp->chinese,temp->english,temp->math,temp->total
        );
        temp = temp->next;
    }
    printf("\n");
}
int main(){
    // initalize the head node
    struct node* head = NULL;
    int i=0,chinese_grade,english_grade,math_grade;
    char name[10],id[10];
    while(i!=3){
        printf("1. insert student data\n2. show data\n3. leave\nInsert:");
        scanf("%d",&i);
        if(i==1){
            //insert student data
            printf("Insert Student name:");
            scanf("%s",name);
            printf("Insert Student ID:");
            scanf("%s",id);
            printf("Insert Student Chinese Grade:");
            scanf("%d",&chinese_grade);
            printf("Insert Student English Grade:");
            scanf("%d",&english_grade);
            printf("Insert Student Math Grade:");
            scanf("%d",&math_grade);
            addnode(&head,name,id,chinese_grade,english_grade,math_grade);
        }else if(i==2){
            printlink(head);
        }else if(i==3){
            break;
            
        }else{
            printf("inesrt error!");
        }
    }
    return 0;
}
```
- 輸出(錯誤)

```
1. insert student data
2. show data
3. leave
Insert:1
Insert Student name:shawn
Insert Student ID:123456
Insert Student Chinese Grade:86
Insert Student English Grade:90
Insert Student Math Grade:72
1. insert student data
2. show data
3. leave
Insert:2
student name: shawn     student ID: 123456
student chinese grade: 86
student english grade: 90
student english grade: 90
student english grade: 90
student english grade: 90
student Math grade: 72
student english grade: 90
student english grade: 90
student Math grade: 72
student english grade: 90
student Math grade: 72
student english grade: 90
student Math grade: 72
student english grade: 90
student Math grade: 72
student english grade: 90
student Math grade: 72
student Math grade: 72
student total grade: 248
```
### code(鏈結串列)使用strdup
```
#include<stdio.h>
#include<stdlib.h>
#include<string.h>
struct node {
    char* st_name;
    char* st_id;
    int chinese;
    int english;
    int math;
    int total;
    struct node* next;

};
struct node* createnode(char* name, char* id, int chinese_grade, int english_grade, int math_grade){
    struct node* newnode = (struct node*)malloc(sizeof(struct node));
    // to check whether the node is created successfully
    if(newnode==NULL){
        printf("memory allocation failed!");
    }
    
    // insert student data inside the node
    newnode->st_name = strdup(name);
    newnode->st_id = strdup(id);
    newnode->chinese = chinese_grade;
    newnode->english = english_grade;
    newnode->math = math_grade;
    newnode->total = newnode->chinese+newnode->english+newnode->math;
    // intalize the point of the node to be NULL
    newnode->next = NULL;
    // return the hole newnode data
    return newnode;
}
struct node* addnode(struct node** head, char* name, char* id, int chinese_grade, int english_grade, int math_grade){
    struct node* newnode = createnode(name,id,chinese_grade,english_grade,math_grade);
    if(newnode==NULL){  printf("createnode failed");}
    // situation1: if the node is the head node
    if(*head==NULL){
        *head = newnode;
    }else{
        // situation2: if the node is not the head node
        struct node* temp = *head;
        while(temp->next!=NULL){
            temp = temp->next;
        }
        // add node after the last noe node
        temp->next = newnode;
    }
    return *head;
}
void printlink(struct node* head){
    struct node* temp = head;
    while(temp!=NULL){
        printf("student name: %s\tstudent ID: %s\nstudent chinese grade: %d\nstudent english grade: %d\nstudent Math grade: %d\nstudent total grade: %d\n",
            temp->st_name,temp->st_id,temp->chinese,temp->english,temp->math,temp->total
        );
        temp = temp->next;
    }
    printf("\n");
}
int main(){
    // initalize the head node
    struct node* head = NULL;
    int i=0,chinese_grade,english_grade,math_grade;
    char name[10],id[10];
    while(i!=3){
        printf("1. insert student data\n2. show data\n3. leave\nInsert:");
        scanf("%d",&i);
        if(i==1){
            //insert student data
            printf("Insert Student name:");
            scanf("%s",name);
            printf("Insert Student ID:");
            scanf("%s",id);
            printf("Insert Student Chinese Grade:");
            scanf("%d",&chinese_grade);
            printf("Insert Student English Grade:");
            scanf("%d",&english_grade);
            printf("Insert Student Math Grade:");
            scanf("%d",&math_grade);
            addnode(&head,name,id,chinese_grade,english_grade,math_grade);
        }else if(i==2){
            printlink(head);
        }else if(i==3){
            break;
            
        }else{
            printf("inesrt error!");
        }
    }
    return 0;
}
```
- 輸出(正確)
```
1. insert student data
2. show data
3. leave
Insert:1
Insert Student name:shawn
Insert Student ID:4131e002
Insert Student Chinese Grade:67
Insert Student English Grade:82
Insert Student Math Grade:64
1. insert student data
2. show data
3. leave
Insert:2
student name: shawn     student ID: 4131e002
student chinese grade: 67
student english grade: 82
student Math grade: 64
student total grade: 213
```
### code(結構陣列):
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
