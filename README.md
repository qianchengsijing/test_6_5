# test_6_5
#include <stdio.h>
//希尔排序
void ShellSort(int A[],int n){
	int i,d,j;
	for(d=n/2;d>=1;d=d/2)
		for(i=d+1;i<=n;++i)
			if(A[i] < A[i-d]){
				A[0] = A[i];
				for(j=i-d;j>0 && A[0]<A[j];j-=d)
					A[j+d] = A[j];
				A[j+d] = A[0];
			}
}
//冒泡排序
void swap(int &a,int &b){
	int temp;
	temp = a;
	a = b;
	b = temp;
}
void BubbleSort(int A[],int n){
	int i,j;
	for(i=0;i<n-1;i++){
		int flag = false;
		for(j=n-1;j>i;j--)
			if(A[j-1] > A[j]){
				swap(A[j-1],A[j]);
				flag = true;
			}
			if(flag == false)
				return;
	}
}
//快速排序
void QuickSort(int A[],int low,int high){
	if(low<high){
		int pivotpos = Partition(A,low,high);
		QuickSort(A,low,pivotpos-1);
		QuickSort(A,pivotpos+1,high);
	}
}
int Partition(int A[],int low,int high){
	int pivot = A[low];
	while(low<high){
		while(low<high && A[high]>=pivot)
			--high;
	    A[low] = A[high];
		while(low<high && A[low]<=pivot)
			++low;
		A[high] = A[low];
	}
	A[low] = pivot;
	return low;
}
//选择排序
//简单选择排序
void SelectSort(int A[],int n){
	int i,j,min;
	for(i=0;i<n-1;i++){
		min = i;
		for(j=i+1;j<n;j++)
			if(A[j] < A[min])
				min = j;
		if(min != i)
			swap(A[i],A[min]);
	}
}
//堆排序
//建立大根堆
void BuildMaxHeap(int A[],int len){
	for(int i=len/2;i>0;i--)
		HeadAdjust(A,i,len);
}
void HeadAdjust(int A[],int k,int len){
	A[0] = A[k];
	for(int i=2*k;i<=len;i*=2){
		if(i<len && A[i]<A[i+1])
			i++;
		if(A[0]>=A[i])
			break;
		else{
			A[k] = A[i];
			k = i;
		}
	}
	A[k] = A[0];
}
//调整堆
void HeapSort(int A[],int len){
	BuildMaxHeap(A,len);
	for(i=len;i>1;i--){
		swap(A[i],A[1]);
		HeadAdjust(A,1,i-1);
	}
}
