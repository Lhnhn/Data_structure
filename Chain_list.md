# 线性表的链式储存
## 定义
```C++
typedef struct LNode
{
    ElemType data;
    struct LNode *next;
}LNode,*LinkList;
```
## 各类函数的实现
### 1.建立链表
```C++
int Build(LinkList &head)
{
    int l,i;
    LinkList pt,prept;
    LinkList pl1=(LinkList)malloc(sizeof(LNode));
    if(!pl1)return 0;
    head=pl1;
    prept=pl1;
    pt=pl1;
    cout<<"链表长度l=";
    cin>>l;
    pl1->data=l;
    for(i=1;i<=l;i++)
    {
        pt=(LinkList)malloc(sizeof(LNode));
        if(!pt)return 0;
        cout<<"第"<<i<<"个节点存储data=";
        cin>>pt->data;
        prept->next=pt;
        prept=pt;
    }
    prept->next=NULL;
    return 1;

}
```
### 2.插入
```C++
int Insert(LinkList &head)
{
    LinkList pt=head,ipt=NULL;
    int n;
    cout<<"插入位置n=";
    cin>>n;
    ipt=(LinkList)malloc(sizeof(LNode));
    if(!ipt)return 0;
    cout<<"插入数据data=";
    cin>>ipt->data;
    pt=Find(pt,n-1);
    ipt->next=pt->next;
    pt->next=ipt;
    head->data++;
    return 1;
}
```
### 3.删除
```C++
int Delete(LinkList &head,int n)
{
    LinkList pt=Find(head,n),prept=Find(head,n-1);
    if(prept!=NULL)
    {
        prept->next=pt->next;
        free(pt);
    }
    else
        cout<<"删除节点错误";
    head->data--;
    return 1;
}
```
### 4.查找
```C++
LinkList Find(LinkList &head,int n)
{
    LinkList pt=head;
    if(n>head->data||n<=0)return NULL;
    int i;
    for(i=1;i<=n&&pt->next!=NULL;i++)
    {
        pt=pt->next;
    }
    return pt;
}
```
### 5.显示
```C++
void Show(LinkList head)
{
	LinkList p;
	p = head->next;
	while(p!=NULL)
	{
		cout<<p->data<<endl;
		p =p->next;
	}
}
```
