# 排序

[排序算法参考1](https://blog.csdn.net/li1669852599/article/details/108505986)
[排序算法参考2](https://blog.csdn.net/weixin_43207025/article/details/114902065)

排序算法经过长时间演变，大体可以分为两类：内排序和外排序。

在排序过程中，全部记录存放在内存，则成为内排序；如果排序过程中需要使用外存，则称为外排序，本文讲的都属于内排序。

## 内排序

### 分类：

- （1）插入排序：直接插入排序、二分法插入排序、希尔排序
- （2）选择排序：直接选择排序、堆排序
- （3）交换排序：冒泡排序、快速排序
- （4）归并排序
- （5）基数排序
- （5）计数排序
- （5）桶排序

| 排序方法   | 时间复杂度(平均)	 | 时间复杂度(最坏)	 | 时间复杂度(最好)	 | 空间复杂度	    | 稳定性	 | 复杂性  |
|:-------|:-----------|:-----------|:-----------|:----------|:-----|:-----|
| 直接插入排序 | 	O(n2)     | 	O(n2)     | 	O(n)	     | O(1)      | 	稳定	 | 简单   |
| 希尔排序   | 	O(nlog2n) | 	O(n2)	    | O(n1.3)    | 	O(1)	    | 不稳定  | 	较复杂 |
| 直接选择排序 | O(n2)      | O(n2)      | O(n2)      | O(1)      | 不稳定  | 简单   | 
| 堆排序    | O(nlog2n)  | O(nlog2n)  | O(nlog2n)  | O(1)      | 不稳定  | 较复杂  | 
| 冒泡排序   | O(n2)      | O(n2)      | O(n)       | O(1)      | 稳定   | 简单   | 
| 快速排序   | O(nlog2n)  | O(n2)      | O(nlog2n)  | O(nlog2n) | 不稳定  | 较复杂  |
| 归并排序   | O(nlog2n)  | O(nlog2n)  | O(nlog2n)  | O(n)      | 稳定   | 较复杂  |
| 基数排序   | O(d(n+r))  | O(d(n+r))  | O(d(n+r))  | O(n+r)    | 稳定   | 较复杂  | 

## 一、插入排序
•思想：每步将一个待排序的记录，按其顺序码大小插入到前面已经排序的字序列的合适位置，直到全部插入排序完为止。
•关键问题：在前面已经排好序的序列中找到合适的插入位置。
•方法： 
### (1). 直接插入排序

插入排序的最好情况是数组已经有序，此时只需要进行n-1次比较，时间复杂度为O(n)
最坏情况是数组逆序排序，此时需要进行n(n-1)/2次比较以及n-1次赋值操作（插入）
平均来说插入排序算法的复杂度为O(n2)
空间复杂度上，直接插入法是就地排序，空间复杂度为(O(1))

### (2). 二分插入排序

最坏情况：每次都在有序序列的起始位置插入，则整个有序序列的元素需要后移，时间复杂度为O(n2)
最好情况：待排序数组本身就是正序的，每个元素所在位置即为它的插入位置，此时时间复杂度仅为比较时的时间复杂度，为O(log2n)
平均情况：O(n2)
空间复杂度上，二分插入也是就地排序，空间复杂度为(O(1))。

### (3). 希尔排序

增量排序的时间复杂度依赖于所取增量序列的函数，但是到目前为止还没有一个最好的增量序列.有人在大量的实验后得出结论;当n在某个特定的范围后希尔排序的比较和移动次数减少至n^1.3
不管增量序列如何取值，都应该满足最后一个增量值为1。
有文献指出，当增量序列为d[k]=2^(t-k+1)时，希尔排序的时间复杂度为O(n^1.5), 其中t为排序趟数。
空间复杂度上，二分插入也是就地排序，空间复杂度为(O(1))。

### 1.直接插入排序
(1) 基本思想:

> 每步将一个待排序的记录，按其顺序码大小插入到前面已经排序的字序列的合适位置（从后向前找到合适位置后），直到全部插入排序完为止。
> （是一种最简单的排序方法，其基本操作是将一条记录插入到已排好的有序表中，从而得到一个新的、记录数量增1的有序表。）

(2)实例

(3)python实现

```python
def InsertSort(list_):
    for i in range(1,len(list_)):           #从列表的第二个元素开始找
        j = i-1                             #先定位第i个元素的前一个元素
        if list_[j] > list_[i]:             #如果前一个元素比第i个元素大
            temp = list_[i]                 #前一个元素比i元素大，所以i元素需要往前插入，故先把list_[i]赋值给一个临时变量
            list_[j+1] = list_[j]           #i元素插入后，其前一个元素即j元素肯定向后位移一位
            # 继续往前寻找,如果有比临时变量大的数字,则后移一位,直到找到比临时变量小的元素或者达到列表第一个元素
            j -= 1
            while j >= 0 and list_[j] > temp:
                list_[j+1] = list_[j]
                j -= 1
            list_[j+1] = temp     #只要找到比temp小的元素，就将temp插入到其后一位(原本其后面一位元素已经右移走掉了)，
                                  #或者i元素前面所有元素都比它大，则j循环到-1时，temp被赋值给了list_[0]即达到列表首位
    return list_
```

c实现:
```c
public static int[] insertSort(int[] arr) {
    if (arr.length == 0) {
        return arr;
    }

    for (int i = 0; i < arr.length - 1; i++) {
        int current = arr[i + 1];
        int preIndex = i;
        while (preIndex >= 0 && arr[preIndex] > current) {
            arr[preIndex + 1] = arr[preIndex];
            preIndex--;
        }
        arr[preIndex + 1] = current;
    }
    return arr;
}

```

### 2.二分插入排序

(1)基本思想

> 二分法插入排序的思想和直接插入一样，只是找合适的插入位置的方式不同，这里是按二分法找到合适的位置，可以减少比较的次数。

(2)实例

(3)python实现

> 二分排序算法只对于事先排好序的算法有效故在使用二分排序算法之前要对样本序列进行排序，具体可描述为以下步骤：
> 
>1.从第一个元素开始，该元素可以被认为已经被排序
> 
> 2.取出下一个元素，在已经排序好的元素序列中(即该被取出元素之前的所有元素)二分查找到第一个比它小的元素的位置
> 
> 3.将被取出元素插入到该元素的位置后
> 
> 4.重复

### 3.希尔排序
(1)基本思想:
> 希尔排序又叫“缩小增量排序”，先取一个小于n的整数d1作为第一个增量，把文件的全部记录分成d1个组。所有距离为d1的倍数的记录放在同一个组中。
> 
> 先在各组内进行直接插入排序，然后取第二个增量d2。其是插入排序改良的算法，希尔排序步长从大到小调整，
> 
> 第一次循环后面元素逐个和前面元素按间隔步长进行比较并交换，直至步长为1，步长选择是关键。

(2)实例

(3)python实现

```python
def ShellSort(list_):
    dk = int(len(list_))                                    #dk是增量,即步长
    while dk > 0:                                           
        dk = dk//2                                          #增量递减
        for i in range(dk):                                 #对应增量的该轮排序进行中
            for j in range(i,int(len(list_)),dk):
                temp = list_[j]
                while j > 0 and list_[j-dk] > temp:
                    list_[j] = list_[j-dk]
                    j -= dk
                list_[j] = temp
    return list_
```

C实现:
```c
public static int[] shellSort(int[] arr) {
    int len = arr.length;
    int gap = len / 2;
    while (gap > 0) {
        int temp;
        for (int i = gap; i < len; i++) {
            int preIndex = i - gap;
            temp = arr[i];
            // 寻找前面已排序队列中比temp大的，向后移动，这里和插入排序一直，只是间距不一样
            while (preIndex >= 0 && arr[preIndex] > temp) {
                arr[preIndex + gap] = arr[preIndex];
                preIndex -= gap; 
            }
            arr[preIndex + gap] = temp;
        }
        gap /= 2;
    }
    return arr;
}

```

## 二、选择排序
•思想：每趟从待排序的记录序列中选择关键字最小的记录放置到已排序表的最前位置，直到全部排完。
•关键问题：在剩余的待排序记录序列中找到最小关键码记录。
•方法： 

### (1). 直接选择排序

选择排序第一轮内循环比较n-1次，然后是n-2次、n-3次........最后一轮内循环比较1次，共(n-1)+(n-2)+....+3+2+1=(n-1+1)
n/2=n^2/2，其时间复杂度为O(n2)
空间复杂度就是在交换元素时那个临时变量所占的内存空间，空间复杂度为O(1)

### (2). 堆排序

堆排序的时间复杂度主要由两部分组成：`初始化建堆`和`每次弹出堆顶元素后重新建堆`的过程
- 初始化建堆过程的时间复杂度O(n) ：假设堆的高度为k，则从倒数第二层右边的节点开始，这一层的节点都要进行子节点比较然后选择是否交换，倒数第三层类似，一直到第一层(
即层数从k-1到1)；那么总的时间为(2^(i-1))*(k-i)，其中i表示第i层(范围是k-1到1)，2^(i-1)表示该层上有多少元素，(k-i)
表示子树上要比较的次数，即S = 2^(k-2)*1 + 2^(k-3)*2 + 2^(k-4)*3 + ... + 2^1*(k-2) + 2^0*(k-1)，使用错位相减法(
用常数2来辅助转换，两边都乘以2再减去原等式)得到S = 2^(K-1) + 2^(K-2) + 2^(K-3) + ... + 2 - (K-1)
，忽略最后一项常数项就是等比数列，即S=2^k-2-(k-1)=2^k-k-1，又因为k为完全二叉树的深度，所以有 2^k <= n < 2^k-1，可以认为k =
logn，综上所述S = n - logn -1，所以时间复杂度为O(n)

- 弹出堆顶元素后重建堆过程的时间复杂度O(nlogn)：循环n-1次，每次都从跟节点往下循环查找所以每一次时间都是logn，总时间为(n-1)*
logn = nlogn - logn , 故堆排序的时间复杂度为`O(n) + O(nlogn) = O(nlogn)`

- 堆排序是接地排序，所以空间复杂度为常数O(1)

### 1.直接选择排序
(1)基本思想：

> 在要排序的一组数中，选出最小的一个数与第一个位置的数交换；然后在剩下的数当中再找最小的与第二个位置的数交换，如此循环到倒数第二个数和最后一个数比较为止。

(2)实例

(3)c实现

```c
public static int[] selectSort(int[] arr) {
    if (arr.length == 0) {
        return arr;
    }

    for (int i = 0; i < arr.length; i++) {
        int minIndex = i;
        for (int j = i; j < arr.length; j++) {
            if (arr[j] < arr[minIndex]) {
                minIndex = j;
            }
        }
        int tmp = arr[i];
        arr[i] = arr[minIndex];
        arr[minIndex] = tmp;
    }
    return arr;
}

```

### 2.堆排序
(1)基本思想：

> 堆排序是一种树形选择排序，是对直接选择排序的有效改进。

堆的定义下：具有n个元素的序列 （h1,h2,…,hn),当且仅当满足（hi>=h2i,hi>=2i+1）或（hi<=h2i,hi<=2i+1） (i=1,2,…,n/2)
时称之为堆。在这里只讨论满足前者条件的堆。由堆的定义可以看出，堆顶元素（即第一个元素）必为最大项（大顶堆）。完全二叉树可以很直观地表示堆的结构。堆顶为根，其它为左子树、右子树。
（可以延伸到前序遍历、中序遍历、后序遍历）

思想：初始时把要排序的数的序列看作是一棵顺序存储的二叉树，调整它们的存储序，使之成为一个堆，这时堆的根节点的数最大。然后将根节点与堆的最后一个节点交换。然后对前面(n-1)
个数重新调整使之成为堆。依此类推，直到只有两个节点的堆，并对它们作交换，最后得到有n个节点的有序序列。从算法描述来看，堆排序需要两个过程，一是建立堆，二是堆顶与堆的最后一个元素交换位置。
所以堆排序有两个函数组成。一是建堆的渗透函数，二是反复调用渗透函数实现排序的函数。

> 难点有:
> 
> (1)如何把一个序列生成大根堆
> 
> (2)输出堆顶元素后，如何使剩下的元素生成一个大根堆

(2)实例


(3)实现

python实现:
```python
def max_heapify(heap,heapSize,root):  # 调整列表中的元素并保证以root为根的堆是一个大根堆
    '''
    给定某个节点的下标root，这个节点的父节点、左子节点、右子节点的下标都可以被计算出来。
    父节点：(root-1)//2
    左子节点：2*root + 1
    右子节点：2*root + 2  即：左子节点 + 1
    '''
    left = 2*root + 1
    right = left + 1
    larger = root
    if left < heapSize and heap[larger] < heap[left]:
        larger = left
    if right < heapSize and heap[larger] < heap[right]:
        larger = right
    if larger != root:  # 如果做了堆调整则larger的值等于左节点或者右节点的值，这个时候做堆调整操作
        heap[larger], heap[root] = heap[root], heap[larger]
        # 递归的对子树做调整
        max_heapify(heap, heapSize, larger)
 
def build_max_heap(heap):  # 构造一个堆，将堆中所有数据重新排序
    heapSize = len(heap)
    for i in range((heapSize -2)//2,-1,-1):  # 自底向上建堆
        max_heapify(heap, heapSize, i)
 
def heap_sort(heap):  # 将根节点取出与最后一位做对调，对前面len-1个节点继续进行堆调整过程。
    build_max_heap(heap)
    # 调整后列表的第一个元素就是这个列表中最大的元素，将其与最后一个元素交换，然后将剩余的列表再递归的调整为最大堆
    for i in range(len(heap)-1, -1, -1):
        heap[0], heap[i] = heap[i], heap[0]
        max_heapify(heap, i, 0)
    return heap
```

java实现:
```c
public static void heapSort(int[] arr) {
    for (int i = (arr.length / 2) - 1; i >= 0; i--) {
        adjust(arr, i, arr.length);
    }

    for (int i = 0; i < arr.length; i++) {
        swap(arr, 0, arr.length - 1 -i);
        adjust(arr, 0, arr.length - 1 - i);
    }
}

private static void adjust(int[] arr, int index, int len) {
    int leftIndex = 2 * index + 1;
    int rightIndex = 2 * index + 2;
    int bigIndex = index;

    if (leftIndex < len && arr[bigIndex] < arr[leftIndex]) {
        bigIndex = leftIndex;
    }

    if (rightIndex < len && arr[bigIndex] < arr[rightIndex]) {
        bigIndex = rightIndex;
    }

    if (bigIndex != index) {
        swap(arr, index, bigIndex);
        adjust(arr, bigIndex, len);
    }
}

private static void swap(int[] arr, int i, int j) {
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
}
```

C实现:
```c
void heapSort(int array[], int n)
{
    int i;
    for (i=n/2;i>0;i--)
    {
        HeapAdjust(array,i,n);//从下向上，从右向左调整
    }
    for( i=n;i>1;i--)
    {
        swap(array, 1, i);
        HeapAdjust(array, 1, i-1);//从上到下，从左向右调整
    }
}
void HeapAdjust(int array[], int s, int n )
{
    int i,temp;
    temp = array[s];
    for(i=2*s;i<=n;i*=2)
    {
        if(i<n&&array[i]<array[i+1])
        {
            i++;
        }
        if(temp>=array[i])
        {
            break;
        }
        array[s]=array[i];
        s=i;
    }
    array[s]=temp;
}
void swap(int array[], int i, int j)
{
    int temp;
 
    temp=array[i];
    array[i]=array[j];
    array[j]=temp;
}
```

## 三、交换排序
•思想：利用交换元素的位置进行排序，每次两两比较待排序的元素，直到全部排完。
•关键问题：排序时要厘清需要进行几轮排序。
•方法：
### (1). 冒泡排序

最坏情况：冒泡排序要进行n-1轮排序循环，每轮排序循环中序列都是非正序的，则每轮排序循环中要进行n-i次比较(1<=i<=n-1)
，即其外循环执行n-1次，内循环最多执行n次，最少执行1次，由于内循环执行次数是线性的，故内循环平均执行(n+1)
/2次，时间复杂度计算为((n-1)(n+1))/2=(-1)/2 ，时间复杂度为O(n2)
最好情况：待排序数组本身就是正序的，一轮扫描即可完成排序，此时时间复杂度仅为比较时的时间复杂度，为O(n)
平均情况：O(n2)
空间复杂度就是在交换元素时那个临时变量所占的内存空间，最优的空间复杂度就是开始元素顺序已经排好了，则空间复杂度为0，
最差的空间复杂度就是开始元素逆序排序了，则空间复杂度为O(n)，平均的空间复杂度为O(1)

### (2). 快速排序

最好情况：是每轮划分都将待排序列正好分为两部分，那么每部分需要的时间为上一轮的1/2。如果排序n个元素的序列，其递归树深度为[logn]
+1即仅需递归logn次，需要总时间为T(n)的话，第一次需要扫描整个序列，做n次比较，然后将序列一分为二，这两部分各自还需要T(n/2)
的时间，依次划分下去：T(n) = 2*T(n/2)+n T(n) = 2*(2*(T(n/4)+n/2)+n = 4*T(n/4)+2n 等等，且T(1) = 0，所以T(n) = n*T(1) + n*
logn = O(nlogn)

最坏情况：当待排序列为有序序列(正序或倒序)，每次划分后得到的情况是一侧有1个元素，另一侧是其余元素，则最终要进行n-1轮循环，且第i次循环要进行n-i次比较，总比较次数为n-1 +
n-2 + ... + 1 = n(n-1)/2，即时间复杂度为O(n2)

### 1.冒泡排序
(1)基本思想

> 在要排序的一组数中，对当前还未排好序的范围内的全部数，自上而下对相邻的两个数依次进行比较和调整，让较大的数往下沉，较小的往上冒。即：每当两相邻的数比较后发现它们的排序与排序要求相反时，就将它们互换。依次比较相邻的两个数，将小数放在前面，大数放在后面。即在第一轮比较中：首先比较第1个和第2个数，将小数放前，大数放后；然后比较第2个数和第3个数，将小数放前，大数放后，如此继续，直至比较最后两个数，将小数放前，大数放后。重复第一轮的步骤，直至全部排序完成。

(2)实例

(3)python实现

第一轮比较完成后，确保了最后一个数是数组中最大的一个数，所以第二轮比较时，最后一个数不参与比较；

第二轮比较完成后，倒数第二个数也一定是数组中第二大的数，所以第三轮比较时，最后两个数不参与比较；

依次类推，每一轮需要比较的次数-1；

```c
/**
 * 冒泡排序
 */
public static int[] bubbleSort(int[] array) {
    if (array.length == 0)
        return array;
    for (int i = 0; i < array.length; i++)
        for (int j = 0; j < array.length - 1 - i; j++)
            if (array[j + 1] < array[j]) {
                int temp = array[j + 1];
                array[j + 1] = array[j];
                array[j] = temp;
            }
    return array;
}
```


### 2.快速排序
(1)基本思想

> 选择一个基准元素,通常选择第一个元素或者最后一个元素,通过一轮扫描，将待排序列分成两部分,一部分比基准元素小,一部分大于等于基准元素,
> 此时基准元素在其排好序后的正确位置,然后再用同样的方法递归地排序划分的两部分，直到各区间只有一个数。

(2)实例

(3)python实现

```c
void quicksort(int a[], int left, int right) {
    int i, j, t, privotkey;
    if (left > right)   //（递归过程先写结束条件）
        return;
 
    privotkey = a[left]; //temp中存的就是基准数（枢轴）
    i = left;
    j = right;
    while (i < j) {
        //顺序很重要，要先从右边开始找（最后交换基准时换过去的数要保证比基准小，因为基准选取数组第一个数）
        while (a[j] >= privotkey && i < j) {
            j--;
        }
        a[i] = a[j];
        //再找左边的
        while (a[i] <= privotkey && i < j) {
            i++;
        }
        a[j] = a[i];
    }
    //最终将基准数归位
    a[i] = privotkey;
 
    quicksort(a, left, i - 1);//继续处理左边的，这里是一个递归的过程
    quicksort(a, i + 1, right);//继续处理右边的 ，这里是一个递归的过程
}
```

```c
/**
 * 
 * @param arr
 * @param low 传入数组起始下标，一般为0
 * @param high 传入数组终止下标，一般为 arr.length - 1
 */
public static void quickSort(int[] arr, int low, int high) {
    if (low < high) {
        int mid = partition(arr, low, high);
        quickSort(arr, low, mid - 1);
        quickSort(arr, mid + 1, high);
    }
}

private static int partition(int[] arr, int low, int high) {
    int key = arr[low];
    while (low < high) {
        while (low < high && arr[high] >= key) {
            high--;
        }
        swap(arr, low, high);
        while (low < high && arr[low] <= key) {
            low++;
        }
        swap(arr, low, high);
    }
    return low;
}

private static void swap(int[] arr, int i, int j) {
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
}
```

## 四、归并排序
时间复杂度：归并排序主要分为拆分和对有序数组进行排序，拆分操作的时间复杂度为logn，排序的复杂度为n，所以归并排序的时间复杂度为O(nlogn)

归并排序的空间复杂度就是那个临时数组和递归时压如栈的数据占用的空间：n + logn，所以空间复杂度为O(n)

(1)基本思想:

> 归并（Merge）排序法是将两个（或两个以上）有序表合并成一个新的有序表，即把待排序序列分为若干个子序列，每个子序列是有序的。然后再把有序子序列合并为整体有序序列。
> 
> 归并排序中第二步，对两个有序数组排序法则非常简单，同时对两个数组的第一个位置比较大小，将小的放入一个空数组，然后被放入空数组的那个位置的指针往后移一个，
> 
> 然后继续和另一个数组的上一个位置进行比较，以此类推。直到最后任何一个数组先出栈完，就将另外一个数组里的所有元素追加到新数组后面。

归并排序和快速排序有那么点异曲同工之妙:
- 快速排序：是先把数组粗略的排序成两个子数组，然后递归再粗略分两个子数组，直到子数组里面只有一个元素，那么就自然排好序了，可以总结为先排序再递归；
- 归并排序：先什么都不管，把数组分为两个子数组，一直递归把数组划分为两个子数组，直到数组里只有一个元素，这时候才开始排序，让两个数组间排好序，依次按照递归的返回来把两个数组进行排好序，到最后就可以把整个数组排好序。

(2)实例

java实现:
```c
/**
 * @param arr 归并数组
 * @param low 传入数组起始下标，一般为0
 * @param high 传入数组终止下标，一般为 arr.length - 1
 */
public static void mergeSort(int[] arr, int low, int high) {
    if (low < high) {
        int mid = low + (high - low) / 2;
        mergeSort(arr, low, mid);
        mergeSort(arr, mid + 1, high);
        merge(arr, low, mid, high);
    }
}

private static void merge(int[] arr, int low, int mid, int high) {
    int[] help = new int[high - low + 1];
    int left = low;
    int right = mid + 1;

    int index = 0;
    while (left <= mid && right <= high) {
        if (arr[left] < arr[right]) {
            help[index++] = arr[left++];
        } else {
            help[index++] = arr[right++];
        }
    }

    while (left <= mid) {
        help[index++] = arr[left++];
    }

    while (right <= high) {
        help[index++] = arr[right++];
    }

    for (int i = 0; i < help.length; i++) {
        arr[low + i] = help[i];
    }
}
```

C递归实现:

```c
void merging(int *list1, int list1_size, int *list2,  int list2_size)
{
    int i=0, j=0, k=0, m=0;
    int temp[MAXSIZE];
 
    while(i < list1_size && j < list2_size)
    {
        if(list1[i]<list2[j])
        {
            temp[k++] = list1[i++];
        }
        else
        {
            temp[k++] = list2[j++];
        }
    }
    while(i<list1_size)
    {
        temp[k++] = list1[i++];
    }
    while(j<list2_size)
    {
        temp[k++] = list2[j++];
    }
 
    for(m=0; m < (list1_size+list2_size); m++)
    {
        list1[m]=temp[m];
    }
}
//如果有剩下的，那么说明就是它是比前面的数组都大的，直接加入就可以了 
void mergeSort(int array[], int n)
{
    if(n>1)
    {
        int *list1 = array;
        int list1_size = n/2;
        int *list2 = array + n/2;
        int list2_size = n-list1_size;
 
        mergeSort(list1, list1_size);
        mergeSort(list2, list2_size);
 
        merging(list1, list1_size, list2, list2_size);
    }
}
//归并排序复杂度分析：一趟归并需要将待排序列中的所有记录  
//扫描一遍，因此耗费时间为O(n),而由完全二叉树的深度可知，  
//整个归并排序需要进行[log2n],因此，总的时间复杂度为  
//O(nlogn),而且这是归并排序算法中平均的时间性能  
//空间复杂度：由于归并过程中需要与原始记录序列同样数量级的  
//存储空间去存放归并结果及递归深度为log2N的栈空间，因此空间  
//复杂度为O(n+logN)  
//也就是说，归并排序是一种比较占内存，但却效率高且稳定的算法 
```

C迭代实现:

```c
void MergeSort(int k[],int n)  
{  
    int i,next,left_min,left_max,right_min,right_max;  
    //动态申请一个与原来数组一样大小的空间用来存储
    int *temp = (int *)malloc(n * sizeof(int));  
    //逐级上升，第一次比较2个，第二次比较4个，第三次比较8个。。。  
    for(i=1; i<n; i*=2)  
    {  
        //每次都从0开始，数组的头元素开始  
        for(left_min=0; left_min<n-i; left_min = right_max)  
        {  
            right_min = left_max = left_min + i;  
            right_max = left_max + i;  
            //右边的下标最大值只能为n  
            if(right_max>n)  
            {  
                right_max = n;  
            }  
            //next是用来标志temp数组下标的，由于每次数据都有返回到K，  
            //故每次开始得重新置零  
            next = 0;  
            //如果左边的数据还没达到分割线且右边的数组没到达分割线，开始循环  
            while(left_min<left_max&&right_min<right_max)  
            {  
                if(k[left_min] < k[right_min])  
                {  
                    temp[next++] = k[left_min++];  
                }  
                else  
                {  
                    temp[next++] = k[right_min++];  
                }  
            }  
            //上面循环结束的条件有两个，如果是左边的游标尚未到达，那么需要把  
            //数组接回去，可能会有疑问，那如果右边的没到达呢，其实模拟一下就可以  
            //知道，如果右边没到达，那么说明右边的数据比较大，这时也就不用移动位置了  
 
            while(left_min < left_max)  
            {  
                //如果left_min小于left_max，说明现在左边的数据比较大  
                //直接把它们接到数组的min之前就行  
                k[--right_min] = k[--left_max];   
            }  
            while(next>0)  
            {  
                //把排好序的那部分数组返回该k  
                k[--right_min] = temp[--next];        
            }  
        }  
    }  
}  
//非递归的方法，避免了递归时深度为log2N的栈空间，
//空间只是用到归并临时申请的跟原来数组一样大小的空间，并且在时间性能上也有一定的提升，
//因此，使用归并排序是，尽量考虑用非递归的方法。
```

## 五、基数排序
时间复杂度：给定n个d位数(即d个关键码，关键码的取值范围为r)，基数排序需要比较元素的每一位，则复杂度为O(d(n+r))
，其中一轮循环分配时间复杂度为O(n)，一轮循环收集时间复杂度为O(r)，共需要d次循环来进行分配收集，即时间复杂度为O(d(n+r))

(1)基本思想

> 将所有待比较数值（正整数）统一为同样的数位长度，数位较短的数前面补零。然后，从最低位开始，依次进行一次排序。这样从最低位排序一直到最高位排序完成以后,数列就变成一个有序序列。

(2)实例


