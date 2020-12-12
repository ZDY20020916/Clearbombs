#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#include <windows.h>
#include <math.h>
#include <conio.h>
#include <string.h>
#define MAX 100

void Controller(int *choice)//做出选择
{
    char a[MAX],*pstr,b[2]="1",c[2]="0";
    int ret1,ret2;
    pstr=a;
    printf("欢迎来到扫雷小游戏！！！！！\n");
    printf("1.开始/继续游戏！！！！！\n");
    printf("0.结束游戏。\n");
    printf("请输入您的选择！！！！！\n");
    fflush(stdin);
    gets(pstr);
    ret1=strcmp(pstr,b);
    ret2=strcmp(pstr,c);
    while(ret1!=0&&ret2!=0)
    {
        fflush(stdin);
        printf("对不起!您输入的有误！请重输！\n");
        fflush(stdin);
        gets(pstr);
        ret1=strcmp(pstr,b);
        ret2=strcmp(pstr,c);
    }
    *choice= atoi(pstr);
}

void initializer(int *a,int *b,int *c)//设置地图参数
{
    int ret;
    printf("请定制您的游戏地图！！！！！\n");
    printf("第一步，请输入地图行数。(输入5--50之间的正整数！)\n");
    ret=scanf("%d",a);
    while(ret!=1||*a<5||*a>60)
    {
        fflush(stdin);
        printf("对不起！输入存在错误！请重输！\n");
        ret=scanf("%d",a);
    }
    printf("第二步，请输入地图列数。(输入5--50之间的正整数！)\n");
    ret=scanf("%d",b);
    while(ret!=1||*b<5||*b>60)
    {
        fflush(stdin);
        printf("对不起！输入存在错误！请重输！\n");
        ret=scanf("%d",b);
    }
    printf("第三步，请输入地雷个数。(雷数别太多（必须小于行X列）！)\n");
    ret=scanf("%d",c);
    while(ret!=1||*c<0||*c>((*b)*(*a)))
    {
        fflush(stdin);
        printf("对不起！输入存在错误！请重输！\n");
        ret=scanf("%d",c);
    }
    printf("定制成功！\n");
}

void InitializetheMap(int r,int l,char (*map)[MAX][MAX][2])
{
    int i,j;
    char a[2]={"*"};
    for(i=0;i<r;i++)
    {
        for(j=0;j<l;j++)
        {
            strcpy((*map)[i][j],a);
        }
    }
}

void MaketheMap1(int bomb,int R,int L,int r,int l,char map[MAX][MAX][2])
{
    int i,j;
    printf("\n     剩余雷数:%d\n\n",bomb);
    printf("     ");
    for(i=0;i<l;i++)
    {
        printf("---");
    }
    printf("\n");
    for(i=0;i<r;i++)
    {
        if(i+1==R)
        {
            printf("    |");
            for(j=0;j<l;j++)
            {
                if(j+1==L)
                {
                    SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE),FOREGROUND_GREEN|FOREGROUND_INTENSITY|BACKGROUND_GREEN);
                    printf(" %s ",map[i][j]);
                    SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE),7);
                }
                else
                {
                    if(atoi(map[i][j])==1)
                    {
                        SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE),1);
                        printf(" %s ",map[i][j]);
                        SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE),7);
                    }
                    else if(atoi(map[i][j])==2)
                    {
                        SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE),2);
                        printf(" %s ",map[i][j]);
                        SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE),7);
                    }
                    else if(atoi(map[i][j])==3)
                    {
                        SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE),3);
                        printf(" %s ",map[i][j]);
                        SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE),7);
                    }
                    else if(atoi(map[i][j])==4)
                    {
                        SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE),5);
                        printf(" %s ",map[i][j]);
                        SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE),7);
                    }
                    else if(atoi(map[i][j])==5)
                    {
                        SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE),6);
                        printf(" %s ",map[i][j]);
                        SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE),7);
                    }
                    else if(atoi(map[i][j])==6)
                    {
                        SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE),6);
                        printf(" %s ",map[i][j]);
                        SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE),7);
                    }
                    else if(atoi(map[i][j])==7)
                    {
                        SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE),6);
                        printf(" %s ",map[i][j]);
                        SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE),7);
                    }
                    else if(atoi(map[i][j])==8)
                    {
                        SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE),6);
                        printf(" %s ",map[i][j]);
                        SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE),7);
                    }
                    else if(strcmp(map[i][j],"B")==0)
                    {
                        SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE),4);
                        printf(" %s ",map[i][j]);
                        SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE),7);
                    }
                    else
                    {
                        printf(" %s ",map[i][j]);
                    }
                }
            }
            printf("|");
            printf("\n");
        }
        else
        {
            printf("    |");
            for(j=0;j<l;j++)
            {
                if(atoi(map[i][j])==1)
                {
                    SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE),1);
                    printf(" %s ",map[i][j]);
                    SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE),7);
                }
                else if(atoi(map[i][j])==2)
                {
                    SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE),2);
                    printf(" %s ",map[i][j]);
                    SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE),7);
                }
                else if(atoi(map[i][j])==3)
                {
                    SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE),3);
                    printf(" %s ",map[i][j]);
                    SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE),7);
                }
                else if(atoi(map[i][j])==4)
                {
                    SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE),5);
                    printf(" %s ",map[i][j]);
                    SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE),7);
                }
                else if(atoi(map[i][j])==5)
                {
                    SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE),6);
                    printf(" %s ",map[i][j]);
                    SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE),7);
                }
                else if(atoi(map[i][j])==6)
                {
                    SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE),6);
                    printf(" %s ",map[i][j]);
                    SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE),7);
                }
                else if(atoi(map[i][j])==7)
                {
                    SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE),6);
                    printf(" %s ",map[i][j]);
                    SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE),7);
                }
                else if(atoi(map[i][j])==8)
                {
                    SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE),6);
                    printf(" %s ",map[i][j]);
                    SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE),7);
                }
                else if(strcmp(map[i][j],"B")==0)
                {
                    SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE),4);
                    printf(" %s ",map[i][j]);
                    SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE),7);
                }
                else
                {
                    printf(" %s ",map[i][j]);
                }
            }
            printf("|");
            printf("\n");
        }
    }
    printf("     ");
    for(i=0;i<l;i++)
    {
        printf("---");
    }
    printf("\n");
}

void MaketheMap2(int r,int l,int map[MAX][MAX])
{
    int i,j;
    printf("\n\n\n");
    printf("   ");
    for(i=0;i<30;i++)
    {
        printf("---");
    }
    printf("\n");
    for(i=1;i<r+1;i++)
    {
        printf("   ");
        for(j=1;j<l+1;j++)
        {
            if(map[i][j]==1)
            {
                SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE),4);
                printf(" %d ",map[i][j]);
                SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE),7);
            }
            else
            {
                printf(" %d ",map[i][j]);
            }
        }
        printf("\n");
    }
}

void SettheBombs(int r,int l,int bomb,int (*map)[MAX][MAX])//布置地雷
{
    int r2,l2,count=0;
    srand(time(NULL));
    while(count<bomb)
    {
        count++;
        r2=rand()%r+1;
        l2=rand()%l+1;
        while((l2==r2&&count<=((4*r*l)/5))||(*map)[r2][l2]==1)
        {
            r2=rand()%r+1;
            l2=rand()%l+1;
        }
        (*map)[r2][l2]=1;
    }
}

int CleartheBombs(int *R,int *L,int a,int b,char (*map1)[MAX][MAX][2],int (*map2)[MAX][MAX],void (*calculate)(int a1,int r1,int b1,int l1,char (*map11)[MAX][MAX][2],int (*map21)[MAX][MAX]))//扫雷
{
    int ret;
    char M;
    printf("\n光标右移按F，左移按A；上移按S，下移按D。\n点击无雷处请按J，排除有雷处请按K！\n");
    fflush(stdin);
    M=getch();
    switch (M)
        {
            case 'A':
                {
                    if(*L>1)
                    {
                        *L=*L-1;
                    }
                    ret=2;
                    break;
                }
            case 'F':
                {
                    if(*L<b)
                    {
                        *L=*L+1;
                    }
                    ret=2;
                    break;
                }
            case 'S':
                {
                    if(*R>1)
                    {
                        *R=*R-1;
                    }
                    ret=2;
                    break;
                }
            case 'D':
                {
                    if(*R<a)
                    {
                        *R=*R+1;
                    }
                    ret=2;
                    break;
                }
            case 'J':
                {
                    if((*map2)[*R][*L]==0)
                    {
                        (*calculate)(a,*R,b,*L,map1,map2);
                        ret=2;
                    }
                    else
                    {
                        ret=0;
                    }
                    break;
                }
            case 'K':
                {
                    if((*map2)[*R][*L]==1)
                    {
                        strcpy((*map1)[*R-1][*L-1],"B");
                        ret=1;
                    }
                    else
                    {
                        ret=0;
                    }
                    break;
                }
            default:
                {
                    ret=2;
                    break;
                }
        }
    return ret;
}

void CalculateNB(int a,int r,int b,int l,char (*map1)[MAX][MAX][2],int (*map2)[MAX][MAX])//计算雷数
{
    int count=0;
    char symbol[2];
    if(r!=0&&l!=0)
    {
        count=(*map2)[r][l-1]+(*map2)[r-1][l-1]+(*map2)[r-1][l]+(*map2)[r-1][l+1]+(*map2)[r][l+1]+(*map2)[r+1][l+1]+(*map2)[r+1][l]+(*map2)[r+1][l-1];
        if(count!=0)
        {
            sprintf(symbol,"%d",count);
            strcpy((*map1)[r-1][l-1],symbol);
        }
        else
        {
            strcpy((*map1)[r-1][l-1]," ");
            if(strcmp((*map1)[r-1][l-2],"*")==0)
            {
                CalculateNB(a,r,b,(l-1),map1,map2);
            }
            if(strcmp((*map1)[r-2][l-2],"*")==0)
            {
                CalculateNB(a,(r-1),b,(l-1),map1,map2);
            }
            if(strcmp((*map1)[r-2][l-1],"*")==0)
            {
                CalculateNB(a,(r-1),b,l,map1,map2);
            }
            if(strcmp((*map1)[r-2][l],"*")==0)
            {
                CalculateNB(a,(r-1),b,(l+1),map1,map2);
            }
            if(strcmp((*map1)[r-1][l],"*")==0)
            {
                CalculateNB(a,r,b,(l+1),map1,map2);
            }
            if(strcmp((*map1)[r][l],"*")==0)
            {
                CalculateNB(a,(r+1),b,(l+1),map1,map2);
            }
            if(strcmp((*map1)[r][l-1],"*")==0)
            {
                CalculateNB(a,(r+1),b,l,map1,map2);
            }
            if(strcmp((*map1)[r][l-2],"*")==0)
            {
                CalculateNB(a,(r+1),b,(l-1),map1,map2);
            }
        }
    }
}

int main()
{
    int map2[MAX][MAX],r=10,l=10,bomb=10,choice=0,count=0,ret,R=1,L=1;
    char map1[MAX][MAX][2];
    Controller(&choice);
    while(choice!=0)
    {
        count=0;
        memset(map2,0,sizeof(map2));
        system("cls");
        printf("游戏开始！！！！！\n");
        fflush(stdin);
        initializer(&r,&l,&bomb);
        system("cls");
        printf("设置地图中，请稍后......\n");
        InitializetheMap(r,l,&map1);
        SettheBombs(r,l,bomb,&map2);
        while(count<bomb)
        {
            system("cls");
            MaketheMap1((bomb-count),R,L,r,l,map1);
            ret=CleartheBombs(&R,&L,r,l,&map1,&map2,CalculateNB);
            if(ret==1)
            {
                count++;
            }
            else if(ret==2)
            {
                count=count;
            }
            else
            {
                printf("游戏失败！！！！！\n");
                MaketheMap2(r,l,map2);
                printf("\n\n\n");
                Controller(&choice);
                count=10000;
            }
        }
        if(count==bomb)
        {
            printf("\n\n\n");
            printf("通关！！！！！\n");
            printf("\n");
            Controller(&choice);
        }
        R=1;
        L=1;
    }
    printf("欢迎再次游戏！\n");
    return 0;
}

