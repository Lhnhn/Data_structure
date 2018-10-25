# 队列的链式映像
## 定义
### 1.
```C++
typedef struct QNode{
    elemtype data;
    struct QNode *next;
}node,*Queue;
```
### 2.
```C++
typedef struct{
    Queue before;
    Queue rear;
}linkqueue;
```
## 各函数的实现
### 1.构造一个空队列
```C++
status initqueue(linkqueue &q){
    q.before=q.rear=(Queue)malloc(sizeof(node));
    if(!q.before){
        exit(OVERFLOW);
    }
    q.before->next=NULL;
    return OK;
}
```
### 2.在队尾插入新的元素
```C++
status enqueue(linkqueue &q,elemtype e){
    Queue p;
    p=(Queue)malloc(sizeof(node));
    if(!p){
        exit(OVERFLOW);
    }
    p->data=e;
    p->next=NULL;
    q.rear->next=p;
    q.rear=p;
    return OK;
}
```
### 3.删除队头元素，并返回其值
```C++
status dequeue(linkqueue &q,elemtype &e){
    Queue p;
    if(q.before==q.rear){
        return ERROR;
    }
    p=q.before->next;
    e=p->data;
    q.before->next=p->next;
    if(q.rear==p){
        q.rear=q.before;
    }
    free(p);
    return OK;
}
```
### 4.构造一个空栈
```C++
status initstack(Stack &s){
    s.base=(elemtype *)malloc(initsize*sizeof(elemtype));
    if(!s.base)
    {
        exit(OVERFLOW);
    }
    s.top=s.base;
    s.stacksize=initsize;
    return OK;
}
```
### 5.用e返回栈顶的值
```C++
status gettop(Stack s,elemtype &e){
    if(s.base==s.top){
        return ERROR;
    }
    e=*(s.top-1);
    return OK;
}
```
### 6.插入元素e为新的栈顶元素
```C++
status push(Stack &s,elemtype e){
    if(s.top-s.base>=initsize){
        elemtype newbase;
        newbase=(elemtype)realloc(s.base,(s.stacksize+size_add)*sizeof(elemtype));
        if(!newbase){
            exit(OVERFLOW);
        }
        s.top=s.base+s.stacksize;
        s.stacksize+=size_add;
    }
    *s.top++=e;
    return OK;
}
```
### 7.删除栈顶元素
```C++
status pop(Stack &s,elemtype &e){
    if(s.base==s.top){
        return ERROR;
    }
    e=*--s.top;
    return OK;
}
```
### 8.回文序列的判定
```C++
status palindrome_sequence(Stack &s,linkqueue &q){
    if(initstack(s)&&initqueue(q)){
        cout<<"栈构造成功！"<<endl;
        cout<<"队列构造成功！"<<endl;
    }
    else{
        cout<<"栈构造失败！"<<endl;
        cout<<"队列构造失败！"<<endl;
    }
    int t=0;
    elemtype e,e1,e2;
    cout<<"请输入需要判定的序列的长度：";
    cin>>t;
    cout<<"请输入需要判定的序列："<<endl;
    for(int i=0;i<t;i++){
        cin>>e;
        push(s,e);
        enqueue(q,e);
    }
    for(int j=0;j<t;j++){
        pop(s,e1);
        dequeue(q,e2);
        if(e1!=e2){
            return FALSE;
        }
    }
    return TRUE;
}
```
