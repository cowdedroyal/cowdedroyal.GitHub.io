# 数组形式实现堆栈

```c
#include <stdio.h>
#define MaxSize 10

typedef struct SNode *Stack;

struct SNode{
	char sign[MaxSize];
	int Top;
};

Stack Ptrs;


Stack MakeEmpty()
{
        Stack PtrS;
        PtrS = (Stack)malloc(sizeof(struct SNode));
        PtrS->Top=-1;
        return PtrS;
}

void Push(Stack Ptrs,char s)
{
	if(Ptrs->Top==MaxSize-1){
		return;
	}else{
		Ptrs->sign[++(Ptrs->Top)] = s;
	} 
}

char Pop(Stack Ptrs)
{
	if(Ptrs->Top==-1){
		return '?';
	}
	else{
		return(Ptrs->sign[(Ptrs->Top)--]);
	}
}

int rank(char a){
	switch (a){
		case '*': return 2;break;
		case '/': return 2;break;
		case '+': return 1;break;
		case '-': return 1;break;
		case '?': return 0;break;
	}
	
}

double count(double num[],char a,int i){
	double c,d;
	c = num[i];
	d = num[i-1];
	num[i]=0;
	num[i-1]=0;
	switch(a){
		case '*': return c*d;break;
		case '/': return d/c;break;
		case '+': return c+d;break;
		case '-': return d-c;break;
	}
}


int main()
{
	char str[100];
	char tempc;
	Ptrs=MakeEmpty();
	int i,j=0;
	double num[100];
	double co,temp;
	gets(str);
	for(i=0;str[i]!='\0';i++){
		if(str[i]=='*'||str[i]=='/'||str[i]=='+'||str[i]=='-'){
			tempc=Pop(Ptrs);
			if(tempc=='?'){
				Push(Ptrs,str[i]);
			}
			else{
				while(rank(tempc)>=rank(str[i])){
					co=count(num,tempc,--j);
					num[j-1]=co;
					tempc=Pop(Ptrs);
				}
				if(tempc!='?')
					Push(Ptrs,tempc);
				Push(Ptrs,str[i]);
			}
		}
		else{
			temp = (double)(str[i]-48);
			num[j++]=temp;
		}	
	}
	while((tempc=Pop(Ptrs))!='?'){
		co=count(num,tempc,--j);
		num[j-1]=co;
	}
//	for(i=0;i<10;i++){
//		printf("%f ",num[i]);
//	}
	printf("\n计算的结果是\n");
	printf("%f",co);
	return 0;
}
```

# 链表形式实现堆栈

```c
#include <stdio.h>
#define ElementType char

typedef struct SNode *Stack;

struct SNode{
	ElementType Data;
	struct SNode *Next;
};

Stack Ptrs;

Stack CreateStack(){
	Stack S;
	S= (Stack)malloc(sizeof(struct SNode));
	S->Next = NULL;
	return S;
}

int IsEmpty(Stack S)
{
	return (S->Next==NULL);
}

void Push(Stack Ptrs,char s)
{
	Stack Tmpcell;
	Tmpcell = (Stack)malloc(sizeof(struct SNode));
	Tmpcell->Data = s;
	Tmpcell->Next = Ptrs->Next;
	Ptrs->Next = Tmpcell;
}

ElementType Pop(Stack Ptrs)
{
	Stack Firstcell;
	ElementType TopElem;
	if(IsEmpty(Ptrs)){
		return '?';
	}else{
		Firstcell = Ptrs->Next;
		Ptrs->Next = Firstcell->Next;
		TopElem = Firstcell->Data;
		free(Firstcell);
		return TopElem;
	}
}

int rank(char a){
	switch (a){
		case '*': return 2;break;
		case '/': return 2;break;
		case '+': return 1;break;
		case '-': return 1;break;
		case '?': return 0;break;
	}
	
}

double count(double num[],char a,int i){
	double c,d;
	c = num[i];
	d = num[i-1];
	num[i]=0;
	num[i-1]=0;
	switch(a){
		case '*': return c*d;break;
		case '/': return d/c;break;
		case '+': return c+d;break;
		case '-': return d-c;break;
	}
}


int main()
{
	char str[100];
	char tempc;
	Ptrs=CreateStack();
	int i,j=0;
	double num[100];
	double co,temp;
	gets(str);
	for(i=0;str[i]!='\0';i++){
		if(str[i]=='*'||str[i]=='/'||str[i]=='+'||str[i]=='-'){
			tempc=Pop(Ptrs);
			if(tempc=='?'){
				Push(Ptrs,str[i]);
			}
			else{
				while(rank(tempc)>=rank(str[i])){
					co=count(num,tempc,--j);
					num[j-1]=co;
					tempc=Pop(Ptrs);
				}
				if(tempc!='?')
					Push(Ptrs,tempc);
				Push(Ptrs,str[i]);
			}
		}
		else{
			temp = (double)(str[i]-48);
			num[j++]=temp;
		}	
	}
	while((tempc=Pop(Ptrs))!='?'){
		co=count(num,tempc,--j);
		num[j-1]=co;
	}
//	for(i=0;i<10;i++){
//		printf("%f ",num[i]);
//	}
	printf("\n计算的结果是\n");
	printf("%f",co);
	return 0;
}
```

