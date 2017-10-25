#include<iostream>
#include<cstdio>//使用c语言的库，方便主函数的格式输入
#include<queue>
using namespace std;
typedef struct node//定义节点类
{
  int key;
  struct node *leftchild,*rightchild;//每个结点有数据还有左右指针
}bstnode,*bst;//声明结构的对象，以及这个结构体的指针，用于申请新的结构单元
bool bstinsert(bstnode* &p,int element)
{
  if(p==NULL)//处理空树，传进来的直接作为根结点
  {
      p=new bstnode;
      p->key=element;
      p->leftchild=p->rightchild=NULL;
      return true;
  }
  
  if(element<p->key)
    return bstinsert(p->leftchild,element);//传进来的数值小于根结点的数值，则在左子树增加这个结点
  if(element>=p->key)
    return bstinsert(p->rightchild,element);//传进来的数值大于等于根结点的数值，则在右子树增加这个结点
}

void leveltraverse(bstnode* root)//层次遍历二叉搜索树
{
  if(root==NULL)
    return;//如果是空树，直接返回
  queue<bstnode*> que;//队列，队列的元素类型是结构指针
  que.push(root);//根结点入队
  while(!que.empty())
  {
    root=que.front();//用root记录队列的第一个元素
    que.pop();//弹出队列的第一个元素
    cout<<root->key<<" ";//将队列第一个元素对应的值输出
    if(root->leftchild!=NULL)
      que.push(root->leftchild);//左孩子入队
    if(root->rightchild!=NULL)
      que.push(root->rightchild);//右孩子入队
  }
  cout<<endl;

}
int main()
{
  int pass;
  cin>>pass;//pass表示要进行测试的组数
  while(pass--)
  {
    bstnode *t;//根指针
    t=NULL;
    int number;
    cin>>number;
    bstinsert(t,number);//先插入第一个元素
    while(scanf(",%d",&number))//按照严格的格式输入，构建二叉树
    {
      bstinsert(t,number);
    }
    leveltraverse(t);//层次遍历二叉树
  }
  
  
}
