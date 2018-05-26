#include<stdio.h>
#include<stdlib.h>
#include<math.h>
#include<string.h>
#include<time.h>
#define LEN sizeof(struct student)

struct student{				//定义一个结构体 
	char num[1000];
	char name[1000];
	char age[1000];
	char c_score[1000]; 
	char english_score[1000]; 
	char math_score[1000]; 
	struct student*next;
};
struct usingdata{
	char num[1000];
	char root[1000];
	struct usingdata *next;
};
struct usingdata *heads;
struct student *head;		//头结点 
void check();    //登陆 
int menu();      //总目录 
void luru();     //数据录入 
void xr();       
void xg();      //修改 
void cr();      //插入 
void sc();      //删除 
int cx_menu();   //插入子目录 
void cx(); 
void cx1();
void cx2();
void cx3();
int tj_menu();   //添加子目录 
void tj();
void tj1();
void tj2();
void tj3();
int px_menu();   //排序子目录 
void px();
void px1();
void px2();
void px3();

//用户登录
void xinjianli()
{
	struct usingdata *p = heads;
	while(p->next)
	p = p->next;
	while(1)
	{
		struct usingdata *pp; 
		pp = (struct usingdata*)malloc(sizeof(struct usingdata));
		memset(pp,0,sizeof(pp));
		printf("请输入你要新建的账号：");
		scanf("%s",pp->num);
		getchar();
		struct usingdata *q = heads;
		int flag = 1;
		while(q)
		{
			flag = 1;
			if(strcmp(q->num,pp->num) == 0)
			{
				printf("此账号已被创建，请重新创建\n");
				flag = 0;
				break;
			}
			q = q->next;
		}
		if(flag == 0)
		{
			continue;
		}
		printf("请输入你要建立的密码：");
		scanf("%s",pp->root);
		getchar(); 
		p->next = pp;
		pp->next = NULL;
		p = p->next;
		
		char cc[1000];
		printf("您是否需要继续？（请输入Y或N）\n");
		scanf("%s",&cc);
		while (strcmp(cc,"Y") != 0 && strcmp(cc,"N") != 0){
			printf("输入正确选项！\n"); 
			scanf("%s", &cc);
	    }
		if(cc[0] == 'Y')
		{
			while(getchar() != '\n');
			continue;
		} 
		else
		{
			while(getchar() != '\n');
			return;
		}
	}
}

void duqv()
{
	FILE *fp = NULL;
	if ((fp=fopen("学生.txt","r")) == NULL){
     	return;
    }
    else{
    	struct usingdata *q = NULL;
    	q = heads;
   		struct usingdata *p = NULL;
    	while (!feof(fp)){
    		p = (struct usingdata*)malloc(sizeof(struct usingdata));
    		if(p == NULL)
    			return;
    		memset(p,0,sizeof(struct usingdata));
    		fscanf(fp,"%s %s\n",q->num,q->root);
    		q->next = p;
    		q = p;
		}
	}
	fclose(fp);
}

int aaa(char *p,char *q)
{
	struct usingdata *m = heads;
	while(m)
	{
		if ((strcmp(p,m->num)==0) && (strcmp(q,m->root)==0))
		return 1;
		m = m->next;
	}
	return 0;
}

void check()
{
	heads = (struct usingdata*)malloc(sizeof(struct usingdata));
	memset(heads,0,sizeof(struct usingdata));
	duqv();
	char userName[256];//用户名 
	char userPWD[256];//密码  
	int i,sum;
	for(i = 1; i < 4; i++)        
	{  
	  //用户名和密码均为abcde 
	    printf("****             (用户名和密码均为abcde)         ****\n");  
	    printf("****             请输入您的用户名:               ****\n");  
	    gets(userName);  
	      
	    printf("****             请输入您的密码:                 ****\n");   
		int p = 0;  
		char ch; 
	 
		while((ch=getch())!='\r')
		{  
			if(ch==8)  
			{  
				putchar('\b');  
				putchar(' ');  
				putchar('\b');
				if(p>0)
				p--;  
			}  
			if(!isdigit(ch)&&!isalpha(ch))  
				continue;  
				putchar('*');  
				userPWD[p++]=ch; 
		}  
		userPWD[p]=0;
	    
	    if ((strcmp(userName,"abcde")==0) && (strcmp(userPWD,"abcde")==0))//验证用户名和密码  
	    {  
	        printf("\n*用户名和密码正确，显示主菜单*\n"); 
			Sleep(1000);
			char c[1000];
			printf("您是否需要新建账号？（请输入Y或N）\n");
			scanf("%s",&c);
			while (strcmp(c,"Y") != 0 && strcmp(c,"N") != 0){
				printf("输入正确选项！\n"); 
				scanf("%s", &c);
		    }
			if(c[0] == 'Y'){
				while(getchar() != '\n');
				xinjianli();
			}else {
				while(getchar() != '\n');
			}
	        return;  
	    }
		else if(aaa(userName,userPWD) == 1)
			return;
	    else  
	    {  
	        if (i < 3)  
	        {    
	            printf("\n用户名或密码错误，请重新输入!\n");  
	        }  
	        else  
	        {   
	            printf("\n您已连续3次将用户名或密码输错，系统将退出!\n");  
	            exit(1);   
	        }  
	    }  
	}  
}

int menu()
{
        char n[1000];
		int n1; 
        do{
        system("cls");
        printf("\t\t\t|-----------------------------------------------------|\n");
        printf("\t\t\t|          *****学生管理系统*****                     |\n");
        printf("\t\t\t|-----------------------------------------------------|\n");
        printf("\t\t\t|              1.学生成绩修改                         |\n");
        printf("\t\t\t|              2.学生成绩插入                         |\n");  
        printf("\t\t\t|              3.学生成绩删除                         |\n");
        printf("\t\t\t|              4.学生成绩查询                         |\n"); 
        printf("\t\t\t|              5.学生成绩统计                         |\n");
        printf("\t\t\t|              6.学生成绩排序                         |\n");
        printf("\t\t\t|              7.退出程序                             |\n");
        printf("\t\t\t-------------------------------------------------------\n");
        printf("请选择1-7：");
        scanf("%s", &n);
        n1 = atoi(n);
        }while(n1 < 0 || n1 > 7);
        return n1;
        
}

void gaiwenjian()
{
	FILE *fp = NULL;
	if((fp=fopen("学生.txt","w"))==NULL)
    {
        printf("文件出错，按任意键退出！");
        getch();
        exit(1); 
    }
    else
    {
    	struct usingdata *p = heads;
    	while(p)
    	{
    		fprintf(fp,"%s %s\n",p->num,p->root);
    		p = p->next;
		}
	}
}

int main(void)
{
	
	check();
	head = (struct student *)malloc(LEN);
	memset(head,0,LEN);
	luru();
	xr();
	int x = 1;
	while (x){
		switch (menu()){
			case 1:
				xg();
				break;
			case 2:
				cr();
				break;
			case 3:
				sc(); 
				break;
			case 4:
				cx(); 
				break;
			case 5:
				printf("\n\t\t\t|              6.学生成绩统计                         |\n");
				tj();
				break;
			case 6:
				printf("\n\t\t\t|              7.学生成绩排序                         |\n");
				px();
				break;
			case 7:
				printf("\n\t\t\t|                谢谢使用！                           |\n");
				gaiwenjian();
				exit(1);
		}
	}
	gaiwenjian();
} 

//学生信息录入（链表）  尾插法 
void luru() 
{ 
	system("CLS");
	printf("\n\t\t\t|                  学生成绩录入                    |\n");
	struct student *current, *prev;
	int num = 0;
	char ch;
	do {	
		num++;
		current = (struct student*)malloc(LEN);	
			
		printf("请输入学号(8位)：");
        scanf("%s",current->num);
        float num1 = atoi(current->num);
        while (num1 > 99999999 || num1 < 10000000){
	        printf("______________________\n");
	        printf("____请输入8位非负数___\n");
	        printf("_______________________\n");
	        printf("重新输入学号:\n ");scanf("%s",&current->num);
	        num1 = atof(current->num);
        }
        
        printf("请输入姓名：");
        scanf("%s",current->name);
        while (current->name[0] > 0){
            printf("________________________\n");
            printf("______姓名请输入汉字____\n");
            printf("______________________\n");
            printf("重新输入姓名: \n");scanf("%s",current->name);
        }
        
        printf("请输入年龄：");
        scanf("%s",current->age);
        int age1 = atoi(current->age);
        while (age1 < 0  || age1 > 100){
            printf("_________________________\n");
            printf("___年龄请输入1-100之间___\n");
            printf("_________________________\n");
            printf("重新输入年龄\n");
            printf("年龄: ");scanf("%s",&current->age);
            age1 = atoi(current->age);
        }
        
        printf("请输入c语言成绩：");
        scanf("%s",current->c_score);
        float c_score1 = atof(current->c_score);
        while (c_score1 < 1 || c_score1 > 100){
            printf("_________________________\n");
            printf("___成绩请输入1-100之间___\n");
            printf("_________________________\n");
            printf("重新输入成绩\n");
            printf("c语言: ");scanf("%s",&current->c_score);
            c_score1 = atof(current->c_score);
        } 
        
        printf("请输入英语成绩:");
        scanf("%s",current->english_score);
        float english_score1 = atof(current->english_score);
        while (english_score1 < 1 || english_score1 > 100){
            printf("_________________________\n");
            printf("___成绩请输入1-100之间___\n");
            printf("_________________________\n");
            printf("重新输入成绩\n");
            printf("英语成绩: ");scanf("%s",&current->english_score);
            english_score1 = atof(current->english_score);
        } 
        
		printf("请输入数学成绩:");
        scanf("%s",current->math_score);
        float math_score1 = atof(current->math_score);
        while (math_score1 < 1 || math_score1 > 100){
            printf("_________________________\n");
            printf("___成绩请输入1-100之间___\n");
            printf("_________________________\n");
            printf("重新输入成绩\n");
            printf("数学: ");scanf("%s",&current->math_score);
            math_score1 = atof(current->math_score);
        }
		if (head->next == NULL){
		   	head->next = current;
		} else {
		   	prev->next = current;
		}
		current->next = NULL;
		prev = current;
		printf("是否继续录入学生信息（Y/N）:\n");
		ch = getch();
		while (ch != 'N' && ch != 'Y'){
			ch = getch();
          }
	}while(ch == 'Y');
	printf("已建立%d个数据\n", num);
	Sleep(1000);
} 

// 数据的存储  
void xr()
{
    struct student *current;
    FILE*fp;
    if((fp=fopen("学生管理系统.txt","wt"))==NULL)
    {
        printf("文件出错，按任意键退出！");
        getch();
        exit(1); 
    }
    for(current = head->next; current != NULL; current=current->next)
    {
        fprintf(fp,"%s %s %s %s %s %s\n", current->num, current->name, current->age, current->c_score, current->english_score, current->math_score);
    }
    fclose(fp);
}

//对数据进行修改 
void xg()
{
	system("CLS");
	printf("\n\t\t\t|                 1.学生成绩修改                      |\n");
	struct student *current;
	char ch;
	char a[1000];
    printf("\n\t\t\t|              信息修改（Y）退出操作（N）             |\n");
    scanf("%s", a);
    while (strcmp(a,"Y") != 0 && strcmp(a,"N") != 0){
		printf("输入正确选项！\n"); 
		scanf("%s", &a);
    }
    
    if (a[0] == 'Y'){ 
		do{
		int flag = 0;
		printf("请输入要修改的学生学号(8位)：");
		char num[1000];
		scanf("%s", num);
		int num2 = atoi(num);
		while (num2 > 99999999 || num2 < 10000000){
	        printf("______________________\n");
	        printf("____请输入8位非负数___\n");
	        printf("_______________________\n");
	        printf("重新输入学号:\n ");
			scanf("%s",num);
			num2 = atoi(num);
        }
	
		for (current = head->next; current != NULL; current = current->next){
			int num1 = atoi(current->num);
			if(num1 == num2)
	        {
	            printf("\t\t已经查到改学生的信息\n");
	            flag=0;
	            break;
	        }
	        else
	            flag=1;  
		}
		if(flag==1)
	        printf("\t\t抱歉，没有查到该学生的信息\n");
	    if(flag==0)
	    {
	        printf("\t\t该学生的原信息如下\n");
		    printf("学生学号:%s\n", current->num);  
	        printf("学生姓名:%s\n",current->name);  
	        printf("学生年龄:%s\n",current->age);
	        printf("学生c语言成绩:%s\n",current->c_score); 
			printf("学生英语成绩:%s\n",current->english_score);
			printf("学生数学成绩:%s\n",current->math_score);
		    printf("\t\t请重新输入该学生的信息\n");	
		    printf("请输入学号(8位)：");
	        scanf("%s",&current->num);
	        int num1 = atoi(current->num);
	        while (num1 > 99999999 || num1 < 10000000){
		        printf("______________________\n");
		        printf("____请输入8位非负数___\n");
		        printf("_______________________\n");
		        printf("重新输入学号:\n ");scanf("%s",&current->num);
		        num1 = atoi(current->num);
	        }
	        
	        printf("请输入姓名：");
	        scanf("%s",&current->name);
	        while (current->name[0] > 0){
	            printf("________________________\n");
	            printf("______姓名请输入汉字____\n");
	            printf("______________________\n");
	            printf("重新输入姓名: \n");scanf("%s",current->name);
	        }
	        
	        printf("请输入年龄：");
	        scanf("%s",&current->age);
	        int age1 = atoi(current->age);
	        while (age1 < 0  || age1 > 100){
	            printf("_________________________\n");
	            printf("___年龄请输入1-100之间___\n");
	            printf("_________________________\n");
	            printf("重新输入年龄\n");
	            printf("年龄: ");scanf("%s",&current->age);
	            age1 = atoi(current->age);
	        }
	        
	        printf("请输入c语言成绩：");
	        scanf("%s",&current->c_score);
	        float c_score1 = atof(current->c_score);
	        while (c_score1 < 1 || c_score1 > 100){
                printf("_________________________\n");
                printf("___成绩请输入1-100之间___\n");
                printf("_________________________\n");
                printf("重新输入成绩\n");
                printf("c语言: ");scanf("%s",&current->c_score);
                c_score1 = atof(current->c_score);
	        } 
	        
	        printf("请输入英语成绩:");
	        scanf("%s",&current->english_score);
	        float english_score1 = atof(current->english_score);
	        while (english_score1 < 1 || english_score1 > 100){
                printf("_________________________\n");
                printf("___成绩请输入1-100之间___\n");
                printf("_________________________\n");
                printf("重新输入成绩\n");
                printf("英语成绩: ");scanf("%s",&current->english_score);
                english_score1 = atof(current->english_score);
            } 
            
			printf("请输入数学成绩:");
	        scanf("%s",&current->math_score);
	        float math_score1 = atof(current->math_score);
	        while (math_score1 < 1 || math_score1 > 100){
                printf("_________________________\n");
                printf("___成绩请输入1-100之间___\n");
                printf("_________________________\n");
                printf("重新输入成绩\n");
                printf("数学: ");scanf("%s",&current->math_score);
                math_score1 = atof(current->math_score);
            }
	        printf("\t\t该学生信息已修改\n");
	        xr();
		}
		printf("是否继续修改学生信息（Y/N）:");
			ch = getch();
			while (ch != 'N' && ch != 'Y'){
				ch = getch();
	          }
	    }while(ch == 'Y');
	      if (a[0] == 'N')
	      return;
	} 
}

//对数据进行插入 
void cr()
{
	system("CLS");
	printf("\n\t\t\t|                  2.学生成绩插入                    |\n");
	char a[1000];
    printf("\n\t\t\t|              信息插入（Y）退出操作（N）             |\n");
    scanf("%s", a);
    while (strcmp(a,"Y") != 0 && strcmp(a,"N") != 0){
		printf("输入正确选项！\n"); 
		scanf("%s", &a);
    }
    if (a[0] == 'Y'){ 
		struct student *current, *p;
		p = head;
		current = (struct student*)malloc(LEN);
        
		printf("请输入学号(8位)：");
        scanf("%s",current->num);
        int num1 = atoi(current->num);
        while (num1 > 99999999 || num1 < 10000000){
	        printf("______________________\n");
	        printf("____请输入8位非负数___\n");
	        printf("_______________________\n");
	        printf("重新输入学号:\n ");scanf("%s",&current->num);
	        num1 = atoi(current->num);
        }
        int num2 = atoi(p->next->num);
        if (num2 == num1){
        	free(current);
        	printf("你所插入的数据以已存在！请重新输入：\n");
        	Sleep(1000);
        	return;
		} 
    
        printf("请输入姓名：");
        scanf("%s",current->name);
        while (current->name[0] > 0){
            printf("________________________\n");
            printf("______姓名请输入汉字____\n");
            printf("______________________\n");
            printf("重新输入姓名: \n");scanf("%s",current->name);
        }
        
        printf("请输入年龄：");
        scanf("%s",current->age);
        int age1 = atoi(current->age);
        while (age1 < 0  || age1 > 100){
            printf("_________________________\n");
            printf("___年龄请输入1-100之间___\n");
            printf("_________________________\n");
            printf("重新输入年龄\n");
            printf("年龄: ");scanf("%s",&current->age);
            age1 = atoi(current->age);
        }
        
        printf("请输入c语言成绩：");
        scanf("%s",current->c_score);
        float c_score1 = atof(current->c_score);
        while (c_score1 < 1 || c_score1 > 100){
            printf("_________________________\n");
            printf("___成绩请输入1-100之间___\n");
            printf("_________________________\n");
            printf("重新输入成绩\n");
            printf("c语言: ");scanf("%s",&current->c_score);
            c_score1 = atof(current->c_score);
        } 
        
        printf("请输入英语成绩:");
        scanf("%s",current->english_score);
        float english_score1 = atof(current->english_score);
        while (english_score1 < 1 || english_score1 > 100){
            printf("_________________________\n");
            printf("___成绩请输入1-100之间___\n");
            printf("_________________________\n");
            printf("重新输入成绩\n");
            printf("英语成绩: ");scanf("%s",&current->english_score);
            english_score1 = atof(current->english_score);
        } 
        
		printf("请输入数学成绩:");
        scanf("%s",current->math_score);
        float math_score1 = atof(current->math_score);
        while (math_score1 < 1 || math_score1 > 100){
                printf("_________________________\n");
                printf("___成绩请输入1-100之间___\n");
                printf("_________________________\n");
                printf("重新输入成绩\n");
                printf("数学: ");scanf("%s",&current->math_score);
                math_score1 = atof(current->math_score);
            }
		current->next = head->next;
		head->next = current;
		printf("\t\t学生信息已存入\n");
		Sleep(1000);
	}
	xr();
}

//对数据进行删除 
void sc()
{
	system("CLS");
	printf("\n\t\t\t|                  3.学生成绩删除                     |\n");
	char a[1000];
    printf("\n\t\t\t|              信息修改（Y）退出操作（N）             |\n");
    scanf("%s", a); 
    while (strcmp(a,"Y") != 0 && strcmp(a,"N") != 0){
		printf("输入正确选项！\n"); 
		scanf("%s", &a);
    }
    
    if (a[0] == 'Y'){ 
		struct student *current;
		struct student *prev = head;
		int flag = 0, num;
		printf("\t\t请输入要删除的学生学号：");
	    scanf("%d",&num);
	
	    current = prev->next;
	    while (current != NULL){
	    	int num1 = atoi(current->num);
	    	if (num1 == num){
			prev->next = current->next;
			free(current); 
			}
			prev = current;
			current = current->next;
		}
		 
		printf("\t\t该学生信息已删除\n");
		Sleep(1000);
	}
    xr();
} 

//对数据进行查询 
int cx_menu()
{
	system("CLS");
    char n[1000];
    int n1;
    do{
    system("CLS");
    printf("\t\t__________________________________________________\n");
    printf("\t\t|                                                |\n");
    printf("\t\t|                   1.按学号查询                 |\n");
    printf("\t\t|                   2.按姓名查询                 |\n");
    printf("\t\t|                                                |\n");
    printf("\t\t|_____________________退出请按3__________________|\n");
    printf("\t\t请选择1-：");
    scanf("%s", n);
    n1 = atoi(n);
    }while(n1 < 1 || n1 > 3);
    return n1;  
}

void cx()
{
    system("CLS");
    char n[1000];
	do {
		switch(cx_menu()) {
			case 3:
			    return;
			case 1:
			    cx1();
			    break;
			case 2:
			    system("CLS");
			    cx2();
			    break;
			
		}
		printf("继续查询请按Y，退出请按N：");
		scanf("%s", n);
		while (strcmp(n,"Y") != 0 && strcmp(n,"N") != 0){
				printf("输入正确选项！\n"); 
				scanf("%s", n);
        	}
		}while(n[0] =='Y');
		if(n[0] == 'N')
		return;
}

//根据学号对数据查询 
void cx1()
{
	system("CLS"); 
	printf("\t\t|                      1.按学号查询                     |\n");
	char num[1000];
	struct student *current;
	printf("请输入你要查询的学生学号");
	scanf("%s", num);
	int num2 = atoi(num);
	while (num2 > 99999999 || num2 < 10000000){
        printf("______________________\n");
        printf("____请输入8位非负数___\n");
        printf("_______________________\n");
        printf("重新输入学号:\n ");scanf("%s",num);
    }
    
	current = head;
	while (current != NULL){
		int num1 = atoi(current->num);
		if (num1 == num2){
			printf("已找到此学生信息\n");  
	        printf("学生学号:%s\n", current->num);  
	        printf("学生姓名:%s\n",current->name);  
	        printf("学生年龄:%s\n",current->age);
	        printf("学生c语言成绩:%s\n",current->c_score); 
			printf("学生英语成绩:%s\n",current->english_score);
			printf("学生数学成绩:%s\n",current->math_score);
			return;
		}
		current = current->next;	 
	}
	printf("未找到此学生信息！\n");
	Sleep(1000); 
	xr();
}

//根据姓名对数据查询 
void cx2()
{
	system("CLS"); 
	printf("\t\t|                      2.按姓名查询                    |\n");
	char num[20];
	struct student *current;
	printf("请输入你要查询的学生姓名:");
	scanf("%s", num);
	while (num[0] > 0){
        printf("________________________\n");
        printf("______姓名请输入汉字____\n");
        printf("______________________\n");
        printf("重新输入姓名: \n");scanf("%s",current->name);
    }
	current = head;
	while (current != NULL){
		if (strcmp(current->name, num) == 0){
			printf("已找到此学生信息\n");  
	        printf("学生学号:%s\n", current->num);  
	        printf("学生姓名:%s\n",current->name);  
	        printf("学生年龄:%s\n",current->age);
	        printf("学生c语言成绩:%s\n",current->c_score); 
			printf("学生英语成绩:%s\n",current->english_score);
			printf("学生数学成绩:%s\n",current->math_score);
			return;
		}
		current = current->next;	 
	}
	printf("未找到此学生信息！\n");
	Sleep(1000); 
	xr();
}

//对数据进行统计 
int tj_menu()
{
	system("CLS");
    char n[1000];
    int n1;
    do{
    system("CLS");
    printf("\t\t_______________________________________________________\n");
    printf("\t\t|                                                      |\n");
    printf("\t\t|                      1.英语及格人数                  |\n");
    printf("\t\t|                      2.数学及格人数                  |\n");
    printf("\t\t|                   3.总分达到一定的人数               |\n");
    printf("\t\t|__________________________按4退出_____________________|\n");
    printf("\t\t请选择1-4：");
    scanf("%s", n);
    n1 = atoi(n);
    }while(n1 < 1 || n1 > 4);
    return n1;   
}

void tj()
{
	system("CLS");
    char n[1000];
	do {
		switch(tj_menu()) {
			case 4:
			    return;
			case 1:
			    tj1();
			    break;
			case 2:
			    system("CLS");
			    tj2();
			    break;
			case 3:
			    system("CLS");
			    tj3();
			    break;
		}
		printf("继续统计请按Y，退出请按N：");
		scanf("%s", n);
		while (strcmp(n,"Y") != 0 && strcmp(n,"N") != 0){
				printf("输入正确选项！\n"); 
				scanf("%s", n);
        	}
		}while(n[0] =='Y');
		if(n[0] == 'N')
		return;	
}

//英语及格统计 
void tj1()
{
	system("CLS");
	printf("\t\t|                        1.英语及格人数                    |\n");
	struct student *current;
	int n = 0;
	current = head;
	while (current != NULL){
		int english_score1 = atof(current->english_score);
		if (english_score1 >= 60){
			n++;
		}
		current = current->next;
	}
    printf("\t\t|____________________学生成绩统计_________________________|\n");
    printf("\t\t英语及格人数为%d\n", n); 
    printf("\t\t统计完毕\n");
	xr();  
}

//数学及格统计 
void tj2()
{
	system("CLS");
	printf("\t\t|                         2.数学及格人数                     |\n");
	struct student *current;
	int n = 0;
	current = head;
	while (current != NULL){
		int math_score1 = atof(current->math_score);
		if (math_score1 >= 60){
			n++;
		}
		current = current->next;
	}
    printf("\t\t|____________________学生成绩统计_________________________|\n");
    printf("\t\t数学及格人数为%d\n", n); 
    printf("\t\t统计完毕\n"); 
	xr(); 
}

//总分及格统计 
void tj3()
{
	system("CLS");
	printf("\t\t|                      3.总分达到一定的人数                  |\n");
	struct student *current;
	char m[1000];
	int m2;
	printf("想要统计总分在任意数以上的人数（总分在0-300之间）\n");
	scanf("%s", &m); 
	m2 = atoi(m);
	while (m2 < 1 || m2 > 300){
            printf("_________________________\n");
            printf("___总分请输入1-300之间___\n");
            printf("_________________________\n");
            printf("想要统计总分在任意数以上的人数（总分在0-300之间）\n");scanf("%s",&m);
            m2 = atoi(m);
    }
        
	int n = 0;
	current = head;
	while (current != NULL){
		int m1 = atof(current->english_score) + atof(current->math_score) + atof(current->c_score);
		if (m1 >= m2){
			n++;
		}
		current = current->next;
	}
    printf("\t\t|____________________学生成绩统计_________________________|\n");
    printf("\t\t总分达到%s以上的人为%d个\n", m, n); 
    printf("\t\t统计完毕\n");
	xr();  	
} 

//对数据进行排序 
int px_menu()
{
	system("CLS");
    char n[1000];
    int n1;
    do{
    system("CLS");
    printf("\t\t__________________________________________________________\n");
    printf("\t\t|                                                        |\n");
    printf("\t\t|                      1.英语成绩的升序                  |\n");
    printf("\t\t|                      2.英语成绩的降序                  |\n");
    printf("\t\t|                      3.总成绩的升序                    |\n");
    printf("\t\t|___________________________按4退出______________________|\n");
    printf("\t\t请选择1-4：");
    scanf("%s", n);
    n1 = atoi(n);
    }while(n1 < 1 || n1 > 4);
    return n1;   
}

void px()
{
	system("CLS");
    char n[1000];
	do {
		switch(px_menu()) {
			case 4:
			    return;
			case 1:
			    px1();
			    break;
			case 2:
			    system("CLS");
			    px2();
			    break;
			case 3:
			    system("CLS");
			    px3();
			    break;
		}
		printf("继续排序请按Y，退出请按N：");
		scanf("%s", n);
		while (strcmp(n,"Y") != 0 && strcmp(n,"N") != 0){
				printf("输入正确选项！\n"); 
				scanf("%s", n);
        	}
		}while(n[0] =='Y');
		if(n[0] == 'N')
		return;	
}

//按照英语成绩的升序 
void px1()
{
	system("CLS"); 
	printf("\t\t|                     1.英语成绩的升序                        |\n");
	struct student *current, *prev, *p, *q, *x, *y;
	p = NULL;
	q = head;
	if (q->next == NULL && q->next->next == NULL){
		return;
	}
	while (p != q->next->next){
		for (prev = q; prev->next->next != p; prev = prev->next){
			int score1 = atoi(prev->next->english_score);
			int score2 = atoi(prev->next->next->english_score);
			if (score1 > score2){
				x = prev->next;
				y = prev->next->next;
				prev->next = y;
				x->next = y->next;
				y->next = x;
			}
		}
		p = prev->next;
	}
    printf("\t\t                      英语成绩的升序                                   \n");
    printf("\t\t%10s%10s%10s%10s%10s%10s\n","学号","姓名","年龄","c语言","英语","数学");
    printf("\t\t--------------------------------------------------------------\n");
    for(current = q->next; current != NULL; current = current ->next)
    {
        printf("\t\t%10s%10s%10s%10s%10s%10s%\n", current->num, current->name, current->age, current->c_score, current->english_score, current->math_score);
    } 
	xr(); 
}

//按照英语成绩的降序
void px2()
{
	system("CLS");
	printf("\t\t|                   2.英语成绩的降序                     |\n");
	struct student *current, *prev, *p, *q, *x, *y;
	p = NULL;
	q = head;
	if (q->next == NULL && q->next->next == NULL){
		return;
	}
	while (p != q->next->next){
		for (prev = q; prev->next->next != p; prev = prev->next){
			int score1 = atoi(prev->next->english_score);
			int score2 = atoi(prev->next->next->english_score);
			if (score1 < score2){
				x = prev->next;
				y = prev->next->next;
				prev->next = y;
				x->next = y->next;
				y->next = x;
			}
		}
		p = prev->next;
	}
    printf("\t\t                      英语成绩的降序                                   \n");
    printf("\t\t%10s%10s%10s%10s%10s%10s\n","学号","姓名","年龄","c语言","英语","数学");
    printf("\t\t--------------------------------------------------------------\n");
    for(current = q->next; current != NULL; current = current ->next)
    {
        printf("\t\t%10s%10s%10s%10s%10s%10s%\n", current->num, current->name, current->age, current->c_score, current->english_score, current->math_score);
    } 	
    xr(); 
} 
 
//按照总成绩的升序 
void px3()
{
	system("CLS");
	printf("\t\t|                    3.总成绩的升序                       |\n");
	struct student *current, *prev, *p, *q, *x, *y;
	p = NULL;
	q = head;
	if (q->next == NULL && q->next->next == NULL){
		return;
	}
	while (p != q->next->next){
		for (prev = q; prev->next->next != p; prev = prev->next){
			int score1 = atoi(prev->next->english_score);
			int score2 = atoi(prev->next->math_score);
			int score3 = atoi(prev->next->c_score);
			int score4 = atoi(prev->next->next->english_score);
			int score5 = atoi(prev->next->next->math_score);
			int score6 = atoi(prev->next->next->c_score);
			if (score1 + score2 + score3 > score4 + score5 + score6){
				x = prev->next;
				y = prev->next->next;
				prev->next = y;
				x->next = y->next;
				y->next = x;
			}
		}
		p = prev->next;
	}
    printf("\t\t                      总成绩的升序                                   \n");
    printf("\t\t%10s%10s%10s%10s%10s%10s\n","学号","姓名","年龄","c语言","英语","数学");
    printf("\t\t--------------------------------------------------------------\n");
    for(current = q->next; current != NULL; current = current ->next)
    {
        printf("\t\t%10s%10s%10s%10s%10s%10s%\n", current->num, current->name, current->age, current->c_score, current->english_score, current->math_score);
    } 
    xr();
}

