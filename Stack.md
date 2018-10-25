# 栈的顺序表储存
## 定义
```C++
typedef struct{
    Status *base;
    Status *top;
    int stacksize;
}SqStack;
```
## 相关函数
### 1.构造一个空栈
```C++
int InitStack(SqStack &S)
{
    S.base=(Status *)malloc(100*sizeof(Status));
    if(!S.base)return 0;
    S.top=S.base;
    S.stacksize=100;
    return 1;
}
```
### 2.插入值为e的元素
```C++
int Push(SqStack &S,Status e)
{
    if(S.top-S.base>=S.stacksize){
        S.base=(Status *)realloc(S.base,(S.stacksize+10)*sizeof(Status));
        if(!S.base)return 0;
        S.top=S.base+S.stacksize;
        S.stacksize+=10;
    }
    *S.top++=e;
    return 1;
}
```
### 3.查找栈顶元素
```C++
int Gettop(SqStack &S,Status &e)
{
    if(S.base==S.top)return 0;
    e=*(S.top-1);
    return 1;
}
```
### 4.删除栈顶元素返回删除值
```C++
int Pop(SqStack &S,Status &e)
{
    if(S.base==S.top)return 0;
    e=*(--S.top);
    return 1;
}
```
### 5.十进制转化为八进制
```C++
void conversion()
{
    SqStack S;
    int e,N;
    InitStack(S);
    cout<<"输入十进制数N=";
    cin>>N;
    cout<<"输出"<<N<<"的八进制数为：";
    while(N){
        Push(S,N%8);
        N=N/8;
    }
    while(S.top!=S.base){
        Pop(S,e);
        cout<<e;
    }
    cout<<endl;
}
```
### 6.判断括号是否匹配
```C++
void BMatching()
{
    SqStack S;
    InitStack(S);
    char c,i;
    int chose=0;
    cout<<"【请输入一串符号,输入“#”时结束输入。】"<<endl;
    do{
      cin>>c;
      switch(c)
      {
        case '(':
        case '{':
        case '[':
            Push(S,c);
            break;
        case ')':
            Gettop(S,i);
            if(i!='('||Gettop(S,i)==0)
                chose=1;
            else
                Pop(S,c);
            break;
        case '}':
            Gettop(S,i);
            if(i!='{'||Gettop(S,i)==0)
                chose=1;
            else
                Pop(S,c);
            break;
        case ']':
            Gettop(S,i);
            if(i!='['||Gettop(S,i)==0)
                chose=1;
            else
                Pop(S,c);
            break;
        default:
            break;
      }
      if(c=='#')break;
    }while(1);
    if(S.top!=S.base)chose=1;
    if(chose)cout<<"匹配失败!"<<endl;
    else cout<<"匹配成功!"<<endl;
}
```
