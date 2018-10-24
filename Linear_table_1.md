## 1.线性表篇（顺序表示和实现）<br>
### 定义<br>
```C++
typedef struct
{
    Elemtype *elem;
    int length;
    int listsize;
}Sqlist;
```

### 各类函数实现<br>
1.构造线性表<br>
```C++
status Initlist_sq(Sqlist &L)
{
    int m;
    L.elem = (Elemtype *)malloc(list_length*sizeof(Elemtype));
    if(!L.elem)
        exit(OVERFLOW);
    cout<<"输入线性表的长度：";
    cin>>m;
    for(int i=0;i<m;i++)
    {
        cin>>L.elem[i];
    }
    L.length=m;
    L.listsize=list_length;
    return 1;
}
```
2.在第i个位置插入数据<br>
```C++
int insert_sq(Sqlist &L,int i,Elemtype e)
{
	  int m;
    Elemtype *newbase;
    if(i>L.listsize||i<0)return ERROR;
    if(L.length>=L.listsize)
    {
        newbase=(Elemtype*)malloc((L.listsize+10)*sizeof(Elemtype));
        if(!newbase)exit(OVERFLOW);
        L.elem=newbase;
        L.listsize+=list_add;
    }//如果长度不够申请新的；
    for(m=L.length;m>=i;m--){
		L.elem[m]=L.elem[m-1];
	}
    L.elem[i-1]=e;
    ++L.length;
    return 1;

}
```
3.在第i个位置删除数据并返回删除值<br>
```C++
int Delete_sq(Sqlist &L,int i,Elemtype &e)
{
    if(i<1||i>L.length)return 0;
    e=L.elem[i-1];
    for(;i<=L.length;i++)L.elem[i]=L.elem[i+1];
    L.length--;
    return 1;
}
```
4.查找e值在线性表第i个位置<br>
```C++
int Findemlem_sq(Sqlist L,int e)
{
    int i,j;
    j=0;
    for(i=0;i<L.length&&j==0;i++)
    {
        if(L.elem[i]==e)
        {
           j=i+1;
        }
    }
    return j;
}
```

  
