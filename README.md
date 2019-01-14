
<!-- TOC -->

1. [**数据结构**](#数据结构)
   1. [第一章:*数据结构的相关概念及定义*](#第一章数据结构的相关概念及定义)
   2. [第二章：*线性表*](#第二章线性表)
      1. [1. 顺序表](#1-顺序表)
      2. [2. 链表](#2-链表)
   3. [第三章：*栈、队列、串*](#第三章栈队列串)
      1. [1. 栈](#1-栈)
      2. [2. 队列](#2-队列)
      3. [3. 串](#3-串)
   4. [第四章：*树*](#第四章树)
      1. [1. 二叉树](#1-二叉树)
         1. [重要成员函数实现：先序遍历建立二叉树](#重要成员函数实现先序遍历建立二叉树)
         2. [重要成员函数实现：先序序列，中序序列构建二叉树](#重要成员函数实现先序序列中序序列构建二叉树)
         3. [重要成员函数实现：统计二叉树节点值、深度、个数、](#重要成员函数实现统计二叉树节点值深度个数)
         4. [重要成员函数实现：先序遍历二叉树（递归）](#重要成员函数实现先序遍历二叉树递归)
         5. [重要成员函数实现：先序遍历（非递归）](#重要成员函数实现先序遍历非递归)
   5. [第五章：*图*](#第五章图)
   6. [第六章：*查找*](#第六章查找)
   7. [第七章：*排序*](#第七章排序)
      1. [1. 直接插入排序](#1-直接插入排序)
      2. [2. 折半插入排序](#2-折半插入排序)
      3. [3. 希尔排序](#3-希尔排序)
      4. [4. 冒泡排序](#4-冒泡排序)
      5. [5. 快速排序](#5-快速排序)
      6. [6. 选择排序](#6-选择排序)
      7. [7. 堆排序](#7-堆排序)

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

```C++
   ADT List
   {
   Data:
   Operation:
       InitList(&L)
       CreateList(&L)
       ListEmpty(L)
       ListLength(L)
       LocateElem(L,e)
       PriorElem(L,cur_e,&pre_e)
       NextElem(L,cur_e,&pre_e)
       ListInsert(&L,i,e)
       ListDelete(&L,i,&e)
       GetElem(L,i,&e)
       ListTraverse(L)
       DestroyList(&L)
   }//ADT List
```

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

> 访问顺序表中任意元素的时间都相等，具有这一特点的存储结构称为随机存取结构。

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

```C++
template <class ElemType>
void LinkList<ElemType>::Inverse()
{
  LinkNode<ElemType *p, *q, *s;
  p=head->next;
  q=p->next;
  while(p&&q)
  {
     s=q->next;
     q->next=p;
     p=q;
     q=s;
  }
  tail=head->next;
  tail->next =NULL;
  head->next=p;
};

```

> - 删除重复节点

```C++
template <class ElemType>
void LinkList<ElemType>::LinkDel()
{
    //让p指针指向第一个有效结点
    LinkNode<ElemType> *p=head->next;
    //p指针所指结点的位置:设置位置变量(包括下面的Q是为了能调用删除函数)
    int locationP=1;
    while(p)
    {
        LinkNode<ElemType> *q=p->next;
        int e,locationQ=locationP+1;
        while(q)
        {
            bool mark=0;
            if(p->data==q->data)
            {
                //如果q的下一个结点不是NULL的话,则让它指向下一个结点
                q=q->next;
                mark=1;
                //删除重复的结点(位置为locationQ)
                Delete(e,locationQ);
            }
            if(!mark)
            {
                q=q->next;
                //q指针所指结点的位置(与q同步)
                locationQ++;
            }
        }
        p=p->next;
        locationP++;
    }
}
```

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
private:                 //顺序栈类的数据成员
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

> ignore

## 第四章：*树*

***
### 1. 二叉树

> 二叉树链表:

```C++
template<class ElemType>
class BinaryTree
{
public:
    BinaryTree():m_root(NULL){} // 构造函数
    ~BinaryTree(){_Destroy(m_root);}   //析构函数
    BinaryTree(const BinaryTree &rhs){m_root = _Copy (rhs.m_root);}//拷贝构造
    BinaryTree& operator=(const BinaryTree &rhs);  //赋值重载
    void Exchange(){_Exchange(m_root);}   //交换左右子树
    int CountOdd(){return _CountOdd(m_root);}  //计算二叉树中的奇数结点个数
    int CountNum(){return _CountNum(m_root);}  //计算二叉树中的结点个数
    int CountLeaf(){return _CountLeaf(m_root);}  //计算二叉树中树叶结点个数
    void Create1(ElemType ch[],const ElemType &endChar);//按以先序次序输入结点值的方式建立二叉树的接口函数
    void Create2(ElemType ch1[],ElemType ch2[],int ); //以二叉树的先序和中序次序建立二叉树的接口函数
    void Clear(){_Destroy(m_root);}//置空二叉树
    bool IsEmpty() const{return m_root == NULL;}//判断二叉树是否为空
    BTNode<ElemType>* Root() const{return m_root;} //返回根结点的指针
    BTNode<ElemType>* Locate(ElemType &e){return _Locate (m_root, e);}//返回二叉树T中元素值为e的结点的指针
    int Depth(){return _Depth(m_root);}  // 求二叉树深度
    BTNode<ElemType>* Parent(BTNode<ElemType> *p){return _Parent(m_root, p);}//返回结点的双亲结点
    BTNode<ElemType>* LeftChild(BTNode<ElemType> *p){return p->lchild;}//返回结点的左孩子结点
    BTNode<ElemType>* RightChild(BTNode<ElemType> *p){return p->rchild;}//返回结点的右孩子结点
    BTNode<ElemType>* LeftSibling (BTNode<ElemType> *p);//返回结点的左兄弟结点
    BTNode<ElemType>* RightSibling (BTNode<ElemType> *p); //返回结点的右兄弟结点
    void PreorderTraverse (void (*visit)(const ElemType &));  //先序递归遍历二叉树的接口函数
    void PreorderTraverseNonRecursive (void (*visit)(const ElemType &));//先序非递归遍历二叉树的接口函数
    void InorderTraverse (void (*visit)(const ElemType &));  //中序递归遍历二叉树的接口函数
    void PostorderTraverse (void (*visit)(const ElemType &));  //后序递归遍历二叉树的接口函数
    void PreoderTraverseNonRecursive(void (*visit)(const ElemType &));//先序非递归遍历二叉树的接口函数
    void InorderTraverseNonRecursive (void (*visit)(const ElemType &));//中序非递归遍历二叉树的接口函数
    void LevelTraverse (void (*visit)(const ElemType &e)); //层序遍历二叉树
    bool InsertChild(BTNode<ElemType> *p,const int &, BinaryTree<char> &);//有条件插入
    void DeleteChild (BTNode<ElemType> *p, int which);     //有条件删除
private:         //私有数据成员
    BTNode<ElemType> *m_root;                            //二叉树根结点指针
    void _Exchange(BTNode<ElemType> *);     //交换二叉树中每个结点的左右子树
    int _CountLeaf(BTNode<ElemType> *);             //计算二叉树中树叶结点个数
    int _CountOdd(BTNode<ElemType> *);             //计算二叉树中结点值为奇数的结点个数
    int _CountNum(BTNode<ElemType> *);      //计算二叉树中的结点个数
    BTNode<ElemType>* _Copy( BTNode<ElemType>* );    //复制二叉树
    void _Create1(BTNode<ElemType>* &, ElemType ch[],const ElemType &,int &);//按先序次序输入结点值的方式建立二叉树
    void _Create2(BTNode<ElemType> * &,ElemType ch1[],ElemType ch2[],int ,int ,int &); //已知二叉树的先序遍历次序及中序遍历次序，建立二叉树T
    void _Destroy(BTNode<ElemType>* &);                //销毁二叉树
    int _Depth(BTNode<ElemType>* );                    // 求二叉树的深度
    BTNode<ElemType>* _Locate(BTNode<ElemType>*, const ElemType &);// 返回二叉树中元素值为e的结点的指针
    BTNode<ElemType>* _Parent (BTNode<ElemType>*, BTNode<ElemType>*);//返回e结点的双亲结点指针
    void _PreorderTraverse(BTNode<ElemType>* ,void (*visit)(const ElemType &e));//先序递归遍历二叉树
    void _InorderTraverse(BTNode<ElemType>* ,void (*visit)(const ElemType &e));//中序递归遍历二叉树
    void _PostorderTraverse(BTNode<ElemType>* ,void (*visit)(const ElemType &e));//后序递归遍历二叉树
};
```
#### 重要成员函数实现：先序遍历建立二叉树
```C++
void Create1(ElemType ch[],const ElemType &endChar);//按以先序次序输入结点值的方式建立二叉树的接口函数

template<class ElemType>
void BinaryTree<ElemType>::Create1(ElemType ch[],const ElemType & c)        //ch[]记录变通后的先序遍历序列，c为指定特殊字符
{
    int i = 0;
    _Create1(m_root, ch, c, i);   // i 是先序序列数组ch[]中的位置指示器，初值为0
}
template<class ElemType>
void BinaryTree<ElemType>::_Create1(BTNode<ElemType> * &T,ElemType ch[],const ElemType &c,int &i)
{
     if (ch[i] == c)            //c为特殊数据用以标示空指针
        T=NULL;
    else
    {
        T = new BTNode<ElemType>;
        T->data = ch[i];
        _Create1(T->lchild, ch, c, ++i);
        _Create1(T->rchild, ch, c, ++i);
    }
}
```

#### 重要成员函数实现：先序序列，中序序列构建二叉树

```C++
template <class ElemType>
void BinaryTree<ElemType> ::Create2(ElemType ch1[],ElemType ch2[],int n) //n记录二叉树中的结点个数，即遍历序列的长度
{
    int i = 0;
    _Create2( m_root,ch1,ch2,0,n-1,i); //i初值为0
}

template<class ElemType>
void BinaryTree<ElemType> :: _Create2(BTNode<ElemType> * &T,ElemType ch1[],ElemType ch2[],int low,int high,int &k)
 //传值后,low=0, high=n-1均记录ch2[] 数组中的位置下标。k初值是0,k记录ch1[]中根结点的位置下标，
{
    int i;
    if(low > high)
        T=NULL;
    else
    {
        T=new BTNode<ElemType>;
        T->data=ch1[k];                               //  ch1[]为先序序列，ch2[]为中序序列，k记录ch1[]中根结点的位置下标
        for ( i = low;i <= high&&ch2[i] != ch1[k];i++) ;   //  i记录ch2[]中的根结点所在的位置下标
        if(ch2[i] == ch1[k])
        {
            k++;
            _Create2(T->lchild,ch1,ch2,low,i-1,k);     // k记录下一个子树根结点的位置下标
            _Create2(T->rchild,ch1,ch2,i+1,high,k);             // k记录下一个子树根结点的位置下标
        }
    }
}
```

#### 重要成员函数实现：统计二叉树节点值、深度、个数、

```C++
int CountNum(){return _CountNum(m_root);}  //计算二叉树中的结点个数

//计算二叉树中的结点个数
template<class ElemType>
int BinaryTree<ElemType>:: _CountNum(BTNode<ElemType> *T)
{
    int sum=0;
    if(T==NULL) return 0;
    else sum+=1;
    return sum+_CountNum(T->lchild)+_CountNum(T->rchild);
}
```

#### 重要成员函数实现：先序遍历二叉树（递归）

```C++
// 先序递归遍历二叉树的接口函数
template <class ElemType>
void BinaryTree <ElemType>::PreorderTraverse(void (*visit)(const ElemType &e))
{
    _PreorderTraverse(m_root, visit);
}
//先序递归遍历二叉树
template <class ElemType>
void BinaryTree<ElemType> ::_PreorderTraverse(BTNode<ElemType>* T,void (*visit)(const ElemType &e))
{
    if (T){
        visit(T->data);
        _PreorderTraverse(T->lchild,visit);
        _PreorderTraverse(T->rchild,visit);
    }
}
```

#### 重要成员函数实现：先序遍历（非递归）

```C++
//先序遍历二叉树的非递归算法(利用栈)
template <class ElemType>
void BinaryTree<ElemType>::PreoderTraverseNonRecursive(void (*visit)(const ElemType &elem)){
    SqStack<BTnode<ElemType> *> S(5);
    S.Push(m_root);                 //根指针进栈
    while(!S.Empty()){
        BTnode<ElemType> *p;
        p=S.Top();
        while(p){
            visit(p->Data);
            p=p->Lchild;
            S.Push(p);
        }
        S.Pop();                    //空指针退栈(左右都在这退)
        if(!S.Empty()){
            p=S.Top();
            S.Pop();
            S.Push(p->Rchild);
        }
    }
}
```

## 第五章：*图*

## 第六章：*查找*
***


## 第七章：*排序*

***
### 1. 直接插入排序

>

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
    //自定义增长序列
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

```C++
    //rewite  shell_sort
    //自然增长序列
    tempalte<class ElemType>
    void ShellSort(ElemType data[],int n)
    {
        int i,index,key;
        for (int step=n/2;step > 0;step/=2)
        {
            for (index = step;index < n;index++)
            {
                key = data[index];
                for (i = index-step;i>=0 && data[i] > key;i-=step)
                {
                    data[i+step] = data[i];
                }
                data[i+step] = key;
            }
        }
    }
```

### 4. 冒泡排序

```C++
    //BubbleSort_base
    template<class ElemType>
    void BubbleSort(ElemType data[], int n)
    {
        for (int i=0;i < n;i++)
        {
            for (int j = i + 1;j < n - 1;j++)
            if (data[i]>data[j])
                Swap(data[i],data[j]);
        }
    }
```

```C++
    //BubbleSort_better
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
    int Partition(ElemType data[], int low, int high)//划分序列
    {
        ElemType pivot = data[low];
        while(low < high)
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
    void QuickSort(ElemType data[],int begin,int end)//递归实现
    {
        if (begin > end)
            return;
        int pivot = Partition(data,begin,end);
        QuickSort(data ,begin ,pivot-1);
        QuickSort(data, pivot+1,end);
    }
    template<class ElemType>
    void QuickSort(ElemType data[],int n)//初始
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
   //堆排序的核心是建堆,传入参数为数组，根节点位置，数组长度
    void Heap_build(int data[],int root,int length)
    {
        int lchild = root*2+1;//根节点的左子结点下标
        if (lchild < length)//左子结点下标不能超出数组的长度
        {
            int flag = lchild;//flag保存左右节点中最大值的下标
            int rchild = lchild+1;//根节点的右子结点下标
            if (rchild < length)//右子结点下标不能超出数组的长度(如果有的话)
            {
                if (data[rchild] > data[flag])//找出左右子结点中的最大值
                {
                    flag = rchild;
                }
            }
            if (data[root] < data[flag])
            {
                //交换父结点和比父结点大的最大子节点
                Swap(data[root],data[flag]);
                //从此次最大子节点的那个位置开始递归建堆
                Heap_build(a,flag,length);
            }
        }
    }
    void Heap_sort(int data[],int len)
    {
        for (int i = len/2; i >= 0; --i)//从最后一个非叶子节点的父结点开始建堆
        {
            Heap_build(a,i,len);
        }
        for (int j = len-1; j > 0; --j)//j表示数组此时的长度，因为len长度已经建过了，从len-1开始
        {
            Swap(data[0],data[j]);//交换首尾元素,将最大值交换到数组的最后位置保存
            Heap_build(a,0,j);//去除最后位置的元素重新建堆，此处j表示数组的长度，最后一个位置下标变为len-2
        }
    }
```