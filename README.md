# doubly-linked-list-operations
#include <stdio.h>
#include <stdlib.h>

struct node
{
struct node *prev;
int data;
struct node *next;
};

 struct node *add_first(struct node *head,int data);
 struct node *insert_b(struct node *head,int data);
 struct node *insert_e(struct node *head,int data);
 struct node *insert_pos(struct node *head,int data,int pos);
 struct node *del_b(struct node *head);
 struct node *del_e(struct node *head);
 struct node *del_pos(struct node *head,int pos);
 int find(struct node *head,int data);
 void traverse(struct node *head);
 
 
 int main()
 {
struct node *head=NULL;
int choice=0;
int data,pos;
while(choice!=9)
{
	printf("1.INSERT IN BEGINNING\n 2.INSERT IN END\n 3.INSERT AT SPECIFIED POSITION\n 4.DELETE IN BEGINNING\n 5.DELETE IN END\n 6.DELETE IN SPECIFIED POSITION\n7.SEARCHING\n8.TRAVERSING\n9.EXIT\n");
	printf("ENTER YOU CHOICE:");
	scanf("%d",&choice);
	switch(choice)
	{
		case 1:
		printf("enter data:");
		scanf("%d",&data);
		head=insert_b(head,data);
		break;
		
		case 2:
		printf("enter data:");
		scanf("%d",&data);
		head=insert_e(head,data);
		break;
		
		case 3:
		printf("enter data:");
		scanf("%d",&data);
		printf("enter position:");
		scanf("%d",&pos);
		head=insert_pos(head,data,pos);
		break;
		
		case 4:
		head=del_b(head);
		break;
		
		case 5:
		head=del_e(head);
		break;
		
		case 6:
		printf("enter position:");
		scanf("%d",&pos);
		head=del_pos(head,pos);
		break;
		
		case 7:
		printf("enter data:");
		scanf("%d",&data);
		pos=find(head,data);
		printf("%d\n",pos);
		break;
 
 		case 8:
 		traverse(head);
 		break;
 		
 		case 9:
 		exit(0);
 		break;
 		
 		default:
 		printf("ENTER A VALID CHOICE:");
 		scanf("%d",&choice);
 	}
 }
 
 return 0;
 }

struct node *add_first(struct node *head,int data)
{
struct node *temp=malloc(sizeof(struct node));
if(head==NULL)
{
	temp->prev=NULL;
	temp->data=data;
	temp->next=NULL;
	head=temp;
}
else
{
	insert_b(head,data);
}
return head;
}

 struct node *insert_b(struct node *head,int data)
{
struct node *temp=malloc(sizeof(struct node));
	temp->prev=NULL;
	temp->data=data;
	temp->next=head;
	head=temp;
return head;
}

struct node *insert_e(struct node *head,int data)
{
struct node *temp;
struct node *temp2=malloc(sizeof(struct node));
temp2->prev=NULL;
temp2->data=data;
temp2->next=NULL;
temp=head;
while(temp->next!=NULL)
{
	temp=temp->next;
}
temp2->prev=temp;
temp2->next=NULL;
temp->next=temp2;
return head;
}

struct node *insert_pos(struct node *head,int data,int pos)
{
struct node *temp=head;
struct node *temp2=NULL;
struct node *newel=malloc(sizeof(struct node));
newel->data=data;
while(pos!=1)
{
	temp=temp->next;
	pos--;
}
if(temp->next==NULL)//last node
{
	newel->next=NULL;
	newel->prev=temp;
	temp->next=newel;
}
else
{
temp2=temp->next;
temp->next=newel;
newel->prev=temp;
temp2->prev=newel;
newel->next=temp2;
}
return head;
}

struct node *del_b(struct node *head)
{
struct node *temp;
temp=head;
if(head==NULL)
{
	printf("list is empty");
}
else
{
	head=temp->next;
	free(temp);
	temp=NULL;
}
return head;
}
	
struct node *del_e(struct node *head)
{
struct node *temp;
temp=head;
if(head==NULL)
{
	printf("list is empty");
}
while(temp->next!=NULL)
{
	temp=temp->next;
}
temp->prev->next=NULL;
free(temp);
temp=NULL;
return head;
}

struct node *del_pos(struct node *head,int pos)
{
struct node *temp=head;
if(head==NULL)
{
	printf("list empty");
}
if(pos==1)
{
	head=head->next;
	if(head!=NULL)
	{
		head->prev=NULL;
	}
	free(temp);
	return head;
}
 for(int i=1;i<pos && temp!=NULL;i++)
 {
 	temp=temp->next;
 }
 if(temp==NULL)
 {
 printf("position is out of bounds");
 return head;
 }
 if(temp->prev != NULL)
 {
 temp->prev->next=temp->next;
 }
 if(temp->next!=NULL)
 {
 temp->next->prev=temp->prev;
 }
 free(temp);
 return head;
 }

int find(struct node *head,int data)
{
struct node *temp;
temp=head;
int pos=1;
while(temp!=NULL && temp->data!=data)
{
	temp=temp->next;
	pos++;
}
return pos;
}

void traverse(struct node *head)
{
struct node *ptr;
ptr=head;
if(head==NULL)
{
	printf("list is empty");
}
while(ptr!=NULL)
{
	printf("%d\n",ptr->data);
	ptr=ptr->next;
}
}
