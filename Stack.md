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
Status InitStack(SqStack &S){
//构造一个空栈
	S.base = (SElemType *)malloc((STACK_INIT_SIZE) * sizeof(SElemType));
	if(!S.base) return ERROR;
	S.top=S.base;
	S.stacksize=STACK_INIT_SIZE;
	return OK;
}
```
### 2.插入值为e的元素
```C++
Status Push(SqStack &S,SElemType e){
//元素e入栈
  SElemType * newbase;
	if((S.base-S.top) >=S.stacksize){
		newbase=(SElemType *)realloc
			(S.base,(S.stacksize+STACKINCREMENT)*sizeof(SElemType));
		if(!newbase) return ERROR;
		S.base=newbase;
		S.stacksize+=STACKINCREMENT;
	}
	*S.top++=e;
	return OK;
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
Status Pop(SqStack &S,SElemType &e){
//元素e出栈
	if(S.base==S.top) return ERROR;
	e=*--S.top;
	return OK;
}
```
### 5.判空
```C++
Status StackEmpty(SqStack S){
   //如果栈为空，则返回TRUE，否则返回FALSE
	if(S.base==S.top) 
		return TRUE;
	return FALSE;
}
```

### 6.十进制转化为八进制
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
### 7.判断括号是否匹配
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
