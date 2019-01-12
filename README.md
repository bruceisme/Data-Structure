
<!-- TOC -->

- [**数据结构**](#数据结构)
    - [第一章:*数据结构的相关概念及定义*](#第一章数据结构的相关概念及定义)
    - [第二章：*线性表*](#第二章线性表)
        - [1. 顺序表](#1-顺序表)
        - [2. 链表](#2-链表)
    - [第三章：*栈、队列、串*](#第三章栈队列串)
        - [1. 栈](#1-栈)
        - [2. 队列](#2-队列)
        - [3. 串](#3-串)
    - [第四章：*树*](#第四章树)
    - [第五章：*图*](#第五章图)
    - [第六章：*查找*](#第六章查找)
    - [第七章：*排序*](#第七章排序)
        - [1. 直接插入排序](#1-直接插入排序)
        - [2. 折半插入排序](#2-折半插入排序)
        - [3. 希尔排序](#3-希尔排序)
        - [4. 冒泡排序](#4-冒泡排序)
        - [5. 快速排序](#5-快速排序)
        - [6. 选择排序](#6-选择排序)
        - [7. 堆排序](#7-堆排序)

<!-- /TOC -->

# **数据结构**

```C++
    void main()
    {
        cout<<"hello,Markdown." <<endl;
        cout<<"hello,data structure."<<endl;
    }
```

## 第一章:*数据结构的相关概念及定义*

***

>1. 数据结构是指`逻辑`结构和物理结构两种，一般指`逻辑`结构
>2. 按结点关系分为4种逻辑结构：集合、线性、树形、图
>3. 数据结构储存方式：顺序、链式
>4. 计算算法`时间复杂度`
>5. 用尖括号表示有向关系<a,b>  用圆括号表示无向关系(a,b)


## 第二章：*线性表*

> 基本功能`增、删、改、查`
***
> 抽象数据类型ADT
>```c
>   ADT List
>   {
>   Data:
>   Operation:
>       InitList(&L)
>       CreateList(&L)
>       ListEmpty(L)
>       ListLength(L)
>       LocateElem(L,e)
>       PriorElem(L,cur_e,&pre_e)
>       NextElem(L,cur_e,&pre_e) 
>       ListInsert(&L,i,e)
>       ListDelete(&L,i,&e)
>       GetElem(L,i,&e)
>       ListTraverse(L)
>       DestroyList(&L)
>   }//ADT List
>```

***

### 1. 顺序表

>代码模板：
```c++
class SqList
{
public:
    SqList(int);
    SqList(const SqList<ElemType>&);
    ~SqList();
    void Produce(int);
    void Clear();
    bool Search(const ElemType& t, int& n);
    ElemType GetElem(int i) const;
    bool SetElem(ElemType e, int i);
    int LocateElem(const ElemType &);
    int LocatePrior(const ElemType &);
    int LocateNext(const ElemType &);
    bool Insert(const ElemType& r, int n);
    bool Delete(const int& n);
    ElemType Read(int n);
    bool Write(const ElemType& r, int n)
    void Traverse();
    void SizeExtender();
    void Inversion();
    void Order();
    SqList<ElemType> Combine(const SqList<ElemType> &A);
private:
    int length;
    int size;
    ElemType* elem;
    void CopyFrom(const SqList<ElemType>&);
};
```
>  访问顺序表中任意元素的时间都相等，具有这一特点的存储结构称为随机存取结构。

### 2. 链表

> 代码模板：
```C++
class LinkList: public List<ElemType>
{
public:
    LinkList();
    LinkList(const LinkList<ElemType>&);
    ~LinkList();
    bool IsEmpty()const {return len <= 0;}
    int  Length()const {return len;} 
    void Clear();  
    bool GetElem (ElemType&,int) const;
    bool SetElem( const ElemType&,int);
    int LocateElem(const ElemType&) const;
    int LocatePrior(const ElemType&) const;
    int LocateNext(const ElemType&) const ;
    bool Insert(const ElemType&, int);
    bool TailInsert(const ElemType&);
    bool Delete(ElemType&,int);
    void Traverse(void(*visit)(const ElemType&)) const;
    void Inverse();
    void LinkDel();
    LinkList<ElemType> operator=(const LinkList<ElemType>&);
private:
    int len;
    void CopyFrom(const LinkList<ElemType>&);
    LinkNode<ElemType> *head;
    LinkNode<ElemType> *tail;
};
```
> 单链表
> - <img src="./img/list_img1.jpg"  width="500">
> - 表头指针：存放单链表中第一个结点的地址的指针。【指向a0(带头结点时)或指向a1(不带头结点时)的指针，上图中的L】
> - 头结点：带头结点的单链表中L【上图中的a1之前的结点a0】
> - 开始结点：，又称首节点，存放单链表的第一个存放元素的结点。【a1】
> - 表尾结点：单链表中最后一个结点，表尾结点的指针域指针为空。【an】
> 
>  **重要操作代码实现**
> - 单链表就地逆置
>>```C++
>>template <class ElemType>
>>void LinkList<ElemType>::Inverse()
>>{
>>  LinkNode<ElemType>> *p, *q, *s;
>>  p=head->next;
>>  q=p->next;
>>  while(p&&q)
>>  {
>>     s=q->next;
>>     q->next=p;
>>     p=q;
>>     q=s;
>>  }
>>  tail=head->next;
>>  tail->next =NULL;
>>  head->next=p;
>>};
>>```
>- 删除重复节点
>> ```C++
>> template <class ElemType>
>> void LinkList<ElemType>::LinkDel()
>> {
>> //让p指针指向第一个有效结点
>> LinkNode<ElemType> *p=head->next;
>> //p指针所指结点的位置:设置位置变量(包括下面的Q是为了能调用删除函数)
>> int locationP=1;
>> while(p)
>> {
>>     LinkNode<ElemType> *q=p->next;
>>     int e,locationQ=locationP+1;
>>     while(q)
>>      {
>>          bool mark=0;
>>          if(p->data==q->data)
>>          {
>>              //如果q的下一个结点不是NULL的话,则让它指向下一个结点
>>              q=q->next;
>>              mark=1;
>>              //删除重复的结点(位置为locationQ)
>>              Delete(e,locationQ);
>>          }
>>          if(!mark)
>>          {
>>              q=q->next;
>>              //q指针所指结点的位置(与q同步)
>>              locationQ++;
>>          }
>>      }
>>      p=p->next;
>>      locationP++;
>> }
>> }
>> ```
***
>>双向链表

> 循环链表
> 
## 第三章：*栈、队列、串*

### 1. 栈
> 代码模板（顺序表实现）
```C++
class SqStack
{
public:
    SqStack(int m);
    ~SqStack();
    void Clear();
    bool Empty() const;
    int Length() const;
    ElemType & Top() const;
    void Push(const ElemType &e);
    void Pop();
    void Traverse1();    //新添加方法, 利用指针遍历栈中各元素;
    void Traverse2();    //新添加方法, 利用下标遍历栈中各元素;
private:                  //顺序栈类的数据成员
    ElemType *m_base;     //基地址指针
    int m_top;            //栈顶指针
    int m_size;           //向量空间大小
};
```
### 2. 队列
> 代码模板（顺序表实现）
```C++
class SqQueue
{
public:
    SqQueue(int m);
    ~SqQueue();
    void Clear();
    bool IsEmpty();
    int Length();
    ElemType GetHead();
    ElemType GetLast();
    void Append(ElemType e);
    void Remove();
    void Traverse();
private:
    ElemType *m_base;
    int m_front;
    int m_rear;
    int m_size;
};
```
### 3. 串
> d

## 第四章：*树*

## 第五章：*图*

## 第六章：*查找*

## 第七章：*排序*

***
### 1. 直接插入排序

```C++
    template<class ElemType>
    void InsertSort(ElemType data[],int n)
    {
        ElemType tmp;
        int i,j;
        for (i=1;i < n;i++)
        {
            if (data[i] > data[i-1])
                continue;
            tmp = data[i];
            data[i] = data[i -1];
            for (j =i-1 ; j>0 && data[j-1]>tmp;j--)
                data[j] = data[j-1];
            data[j] = tmp;
        }
    }
```
    
### 2. 折半插入排序

```C++
    template<class ElemType>
    void BInsertSort(ElemType data[],int n)
    {
        ElemType tmp;
        int i,j,mid,low,high;
        for (i = 1; i < n; i++)
        {
            tmp = data[i];
            low = 0;
            high = i-1;
            while (low<=high)
            {
                mid = (low+high)/2;
                if (tmp < data[mid])
                    high = --mid;
                else
                    low = ++mid;
            }
            for (j = i-1;j>=low;j--)
                data[j+1] = data[j];
            data[low] = tmp;
        }
    }
```

### 3. 希尔排序

```C++
    template<class ElemType>
    void ShellSort(ElemType data[], int increments[], int n, int incrementsLength)
    {
        int i, j, k;
        ElemType tmp;
        for(k = 0; k < incrementsLength; k++)
        {
            for (i = increments[k]; i < n; i++)
            {
                tmp = data[i];
                for (j = i;j >= increments[k]; j -= increments[k])
                {
                    if (tmp>=data[j - increments[k]])
                        break;
                    data[j] = data[j - increments[k]];
                }
                data[j] = tmp;
            }
        }
    }
```

### 4. 冒泡排序

```C++
    template<class ElemType>
    void BubbleSort(ElemType data[], int n)
    {
        int lastSwapIndex = n - 1;
        int i, j;
        for (i = lastSwapIndex; i > 0; i = lastSwapIndex)
        {
            lastSwapIndex = 0;
            for (j = 0; j < i; j++)
            {
                if (data[j] > data[j+1])
                {
                    Swap(data[j],data[j + 1]);
                    lastSwapIndex = j;
                }
            }
        }
    }
```

### 5. 快速排序

```C++
    template<class ElemType>
    int Partition(ElemType data[], int low, int high)
    {
        ElemType pivot = data[low];
        while(low<high)
        {
            while(low < high && data[high]>= pivot)
                high--;
            while(low < high && pivot >= data[low])
                low++;
            data[high] = data[low];
        }
        data[low] = pivot;
        return low;
    }

    template<class ElemType>
    void QuickSort(ElemType data[],int begin,int end)
    {
        if (begin > end)
            return;
        int pivot = Partition(data,begin,end);
        QuickSort(data ,begin ,pivot-1);
        QuickSort(data, pivot+1,end);
    }

    template<class ElemType>
    void QuickSort(ElemType data[],int n)
    {
        if (n < 2)
            return;
        QuickSort(data,0,n-1);
    }
```

### 6. 选择排序

```C++
    template<class ElemType>
    void SelectionSort(ElemType data[], int n)
    {
        int i,j,min;
        for (i = 0;i < n;i++)
        min = i
        {
            for (j = i + 1; j < n; j++)
                if (data[j] < data[min]) min = j;
        }
        Swap(data[i],data[min]);
    }
```

### 7. 堆排序
```C++
   template<class ElemType>
```