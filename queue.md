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
Status InitQueue (LinkQueue &Q){
	//构造一个空队列
	Q.front=Q.rear=(QueuePtr)malloc(sizeof(QNode));
	if(!Q.front) return ERROR;
	Q.front->next=NULL;
	return OK;
}```
### 2.判空
```C++
Status QueueEmpty(LinkQueue &Q){
//判断Q是否为空, 若为空，则输出TRUE，否则输出FALSE
	if(Q.front==Q.rear)
		return TRUE;
	return FALSE;
}
```
### 3.在队尾插入新的元素
```C++
Status EnQueue(LinkQueue &Q,QElemType e){
	//将元素e入队列
	QueuePtr p;
	p=(QueuePtr)malloc(sizeof(QNode));
	if(!p) return ERROR;
	p->data=e;
	p->next=NULL;
	Q.rear->next=p;
	Q.rear=p;
	return OK;
}
```
### 3.删除队头元素，并返回其值
```C++
Status DeQueue(LinkQueue &Q,QElemType &e){
	   //将元素e出队列
	QueuePtr p;
	if(Q.front==Q.rear)
		return ERROR;
	p=Q.front->next;
	e=p->data;
	Q.front->next=p->next;
	if(Q.rear==p)         
		Q.rear=Q.front;
	free(p);
	return OK;
}
```
### 4.遍历队列Q
```C++
Status QueueTraverse(LinkQueue Q){
	//遍历输出队列Q
	QueuePtr p;
	if(Q.front==Q.rear)
		cout<<"队列中没有元素"<<endl;
	else{
		p=Q.front->next;
		cout<<"队列元素为：";
		while(p){
			cout<<p->data<<"->";
			p=p->next;
		}
		cout<<endl;
	}
	return OK;
}
```
