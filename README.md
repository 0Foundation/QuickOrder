# QuickOrder
伪算法思路:
9  0  8  10  -5  2  13  7 用快速排序升序排列
先整体考虑
思想:先找到某一个元素的确切位置,把整体分成两半,左一半按着同样的方法找到某一个元素的位置,
将左半部分分成两半,右边同理
递归

决定先确定第一个元素9 的位置,它应该在第六个位置

1.定义一个val,他表示准备找到位置的数字,也就是9:val=9
2.定义两个指针,low,high,分别指向首尾数字
3.high所指向的数字与val相比
	a.若high所指向的数字小于val将high指向的数字与
	  low指向的数字互换位置,然后high不再动
	b.若high所指向的数字大于val,则high指针向左边移
	  动,直到找到比val小的数字去换位置
为什么小于val互换位置,因为是升序排列,大数字在后面,小数字在前面
4.low所指向的数字与val相比
	a.若low所指向的数字大于val将low所指向的数字与
	  high所指向的数字互换位置,然后low不再动
	b.若low所指向的数字小于val,则low指针向右移动,
	  直到找到比val大的数字去换位置
5.直到low,high两个指针指向同一个位置,这个位置就是val应该在的位置


5  2  6  8  4  3  7  快速排序升序





程序演示:
#include <iostream>
#include <stdio.h>

using namespace std;
void QuickSort(int * a,int low,int high);
int Findpos(int * a ,int low ,int high);
int main()
{
    int a[6]={-22,1,0,-555,4,-93};
    int i;
    QuickSort(a,0,5);//第二个参数表示第一个元素的下标,第三个参数表示最后一个元素的下标
    for (i=0;i<6;i++)
    {
        printf("%d  ",a[i]);
    }
    printf("\n");
    return 0;
}
void QuickSort(int * a,int low,int high)
{
    int pos;//位置

    if(low<high)//low等于high就不用排了
    {
        pos=Findpos(a,low,high);//为决定找的元素找位置
        QuickSort(a,low,pos-1);
        QuickSort(a,pos+1,high);
    }
}
int Findpos(int * a ,int low ,int high)
{
    int val=a[low];
    while (low <high)//先要确定low是小于high的
    {
        while (low<high && a[high]>=val)//第一个条件是基本条件low要小于high,第二个只要high所指向的元素大于等于val,high向左移动
            --high;
        a[low]=a[high];//跳出上面的while循环证明找到了比val小的值,也就是a[high]<val,所以互换位置
        while (low <high && a[low]<=val)//low所指向的数字小于val
            ++low;
        a[high]=a[low];
    }
    //整个while都跳出来证明low =high,low和high指向了同一个数字
    a[low]=val;

    return low;//要返回的是位置,也就是low或者high,最后low=high,返回谁都一样
}
