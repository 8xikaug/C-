[TOC]



## 一些语法

> doule类型的输入输出的区别
> printf("%f",…);
> scanf("%lf",…);



> Devc++调试：查看变量的值，要先添加查看才能在左边的调试框中显示
> 			或者在工具栏中把环境配置中的‘浏览debug变量’打开就行了



> srand(time(0))，srand是启用伪随机池，括号里面是自定义随机数的范围，使用time函数使随机更真实
> 相应要加上头文件#include <time.h>



> do while：不管while之后的条件是否满足都至少会执行一次循环体



> 如果有固定的次数，用for
> 如果必须要执行一次，用do while
> 其他情况用while



> 当有多重循环时，需要从内层跳到最外层时需要在每个循环分支后面加break，很麻烦，有个东西叫goto可以直接跳到最外层
> goto out;(这句放在内层循坏结尾)
> out:return 0;(放在最外层循环结尾)



> sizeof( )是运算符，给出某个类型或变量在内存中所占的字节数
>
> sizeof( )是静态运算符，括号里的运算做不了



> 逃逸字符
>
> \t:制表符
>
> \n:换行
>
> \b:回退一格（\b之后要有输入，eg：输入123\ba,输出12a)
>
> \r:回车



> ASCII码(0~9,a-z,A-Z)
> 大写字母变小写字母：A+'a'-'A'
> 小写字母变大写字母：a+'A'-'a'





---



## 判断是否为素数

```c
break:跳出循环
continue:跳过这一轮循环剩下的语句，执行下一轮循环
比如：（判断输入的数是否为素数）
#include <stdio.h>
int main(){
	int x;
	scanf("%d",&x);
	int i;
	int isprime=1;
	for(int i=2;i<x;i++){
		if(x%i==0){
		isprime=0;
		continue;
		}
        printf("%d\n",i);
	}
	if(isprime==1){
		printf("是素数\n");
	}
	else
	printf("不是素数\n");
	return 0;
}
```

## 1+1/2+1/3+1/4+……(下面是以连续加到10个数为例)

```c
#include <stdio.h>
int main(){
	double a=0.0;
	for(int i=1;i<=10;i++){
		a=a+1.0/i;//不能是1/i,因为除号两边都是整数，结果只能是整数
	}
	printf("%f",a);
	return 0;
}
```

## 1-1/2+1/3-1/4……

```c
①BY myself
#include <stdio.h>
int main(){
	double a=0;
	for(int i=1;i<=10;i++){
		if(i%2==0)
		a=a-1.0/i;
		else
		a=a+1.0/i;
	}
	printf("%lf",a);
	return 0;
}
②BY 翁恺
#include <stdio.h>
int main(){
	double a=0;
	double sign=1.0;
	for(int i=1;i<=10;i++){
		a=a+sign*1.0/i;
		sign=-sign;
	}
	printf("%f",a);
	return 0;
}
```

## 输入一个非负整数，正序输出每一位

```c
①BY myself
#include <stdio.h>
#include <math.h>
int main(){
	int a;
	printf("请输入一个非负整数：");
	scanf("%d",&a);
	int b=0,c,t=a;
	if(a==0)
	printf("%d ",a);
	while(a!=0){
		a=a/10;
		b++;//记录整数的位数
	}
	while(b!=0){
		c=pow(10,b);//10的b次方
		t=t%c;
		b--;
		printf("%d ",t/(c/10));
	}
	return 0;
}
②BY 翁恺
#include <stdio.h>
int main() {
    int a=7000;
    int b=1;
    int t=a;
    while(t>9){
    	t=t/10;
    	b=b*10;
	}
	printf("a=%d b=%d\n",a,b);
	do{
		int d=a/b;
		printf("%d ",d);
		a=a%b;
		b=b/10;
	}while(b>0);
    return 0;
}
```

## 求符合给定条件的整数集：

> ##### 输入一个小于10的正整数a，考虑从a开始的连续4个数，将他们组合成无重复的3位数，并且有小到大输出，每行6个数，且数之间用空格分开，行末不能有多余的空格

```c
#include <stdio.h>
int main(){
	int a,i,j,k;
	scanf("%d",&a);
	int count=0;
	for(i=a;i<=a+3;i++){
		for(j=a;j<=a+3;j++){
			for(k=a;k<=a+3;k++){
				if(i!=j&&i!=k&&j!=k){
					printf("%d%d%d",i,j,k);
					count++;
					if(count==6)//每行6个数
					{
						printf("\n");
						count=0;
					}
					else printf(" ");//数之间用空格分开
				}
			}
		}
	}
	return 0;
}
```

## 输入一个正整数a（3<=a<=7)，输出所有a为的水仙花数

```c
#include <stdio.h>
#include <math.h>
int main(){
	int a,b,c;
	int sum=0;
	printf("请输入一个大于三的正整数a，接下来会给您输出所有a位的水仙花数:");
	scanf("%d",&a);
	int e=pow(10,a);
	for(int i=e/10;i<=e-1;i++){//确定a位数的范围
		int j=i;
	while(j!=0){
		b=j%10;
		j=j/10;//逆序得到每一位
		c=pow(b,a);
		sum=sum+c;
		}
	if(sum==i){
		printf("%d\n",i);	
		sum=0;}
	else
		sum=0;			
	}
	return 0;
}
```

## 九九乘法表

```c
#include <stdio.h>
int main(){
	int a;
	scanf("%d",&a);
	for(int i=1;i<=a;i++){
		for(int j=1;j<=i;j++){
			printf("%d*%d=%d ",j,i,i*j);
		}
		printf("\n");
	}
	return 0;
}
```

## 统计给定范围内（m~n)的素数个数并求和

```c
#include <stdio.h>
int main(){
	int m,n;
	scanf("%d %d",&m,&n);
	int count =0;//统计素数个数	
	int sum=0;//求和
	for(int j=m;j<=n;j++){
		int isprime=1;//注意要放在循环里面
		for(int i=2;i<j;i++){//素数是一个大于1的自然数
			if(j%i==0){//除了1和它自身外，不能被其他自然数整除的数。
			isprime=0;
			break;
			}
		}
		if(isprime==1){
			printf("%d ",j);
			sum=sum+j;
			count++;
		}
	}
	printf("\n%d sum=%d",count,sum);
	return 0;
}
```

## 2/1+3/2+5/3+……

> ##### (从第2项起，每项的分子都是前一项分子与分母的和，分母都是前一项的分子)
>
> ##### 要求输入一个正整数N，输出前N项和

```c
#include <stdio.h>
#include <time.h>
int main(){
	int n;
	scanf("%d",&n);
	double a=2.0,b=1.0;
	int t;
	double x=2.0;
	for(int i=1;i<n;i++){
		t=a;
		a=a+b;
		b=t;
		x=x+a/b;
	}
	printf("%f",x);
	return 0;
}
```

---

----

---

## 函数原型声明

用来告诉编译器这个函数长什么样，这样能让main函数放在整个代码前面便于查看

eg：

```c
#include <stdio.h>

void sum(int begin,int end);//函数原型声明
	//括号里的函数名称也可省略，因为编译器只需要知道你定义的函数的类型就OK了，但为了方便阅读一般会保留

int main(){
    sum(20,30);//实参
    return 0;
}

void sum(int begin,int end){//函数定义 //形参
    int sum=0;
    for(int i=begin;i<=end;i++){
        sum=sum+i;
    }
    printf("%d到%d的和是：%d",begin,end,sum);
}
```

---

## 类型不匹配

- [ ] 调用函数时给的值与参数的类型可以不匹配是C语言传统上最大的漏洞
- [ ] 编译器总是悄悄替你把类型转换好，但很可能不是你所期望的
- [ ] c++/Java在这方面很严格

---

## 传值

- [ ] 传参只能传值给函数然后函数计算完返回一个结果或者不返回结果，没办法修改main里面定义的变量
- [ ] 局部变量在被调用后就消失了，除非用指针或者全局变量，不然没办法在函数里改变传过来的值
- [ ] 实参到形参的值传递是单向的
- [ ] 返回值只能返回一个，所以在需要返回两个结果时要用上指针

eg：

```c
下面这个代码无法进行a与b之间的交换
在 swap 函数中，参数 a 和 b 是通过值传递的，这意味着函数接收的是 a 和 b 的副本，而不是它们的原始值。因此，在函数内部对 a 和 b 的任何修改都不会影响到 main 函数中的 a 和 b。
#include <stdio.h>
void swap(int a,int b){
	int t=a;
	a=b;
	b=t;
}
int main(){
	int a=5;
	int b=6;
	swap(a,b);
	printf("a=%d,b=%d\n",a,b);
	return 0;
}
```

修改过后：

```c
#include <stdio.h>
void swap(int *a, int *b) {
    int t = *a;
    *a = *b;
    *b = t;
}

int main() {
    int a = 5;
    int b = 6;
    swap(&a, &b);  // 传递 a 和 b 的地址
    printf("a=%d,b=%d\n", a, b);
    return 0;
}
```

---

## 数组

### 数组统计个数

> 输入数量不确定的[0,9]范围内的整数，统计每一个数字出现的次数，输入-1表示结束

```c
#include <stdio.h>
int main(){
	const int number=10;//数组大小
	int i;
    int x;
    int count[number]={0};//定义数组并初始化（初始化这里和下面注释表达的意思一样）
    
//    for(i=0;i<number;i++){
//		count[i]=0;//考虑安全性要初始化数组
//    }
    
    scanf("%d",&x);
    while(x!=-1){
        if(x>=0&&x<=9){
            count[x]++;//数组参与运算
        }
		scanf("%d",&x);
    }
    //遍历数组输出
    for(i=0;i<number;i++){
        printf("%d出现了%d次\n",i,count[i]);
    }
    return 0;
}
```

### 数组的集成初始化

```c
int a[]={2,3,6,8,9};
```

### 数组的大小

```c
sizeof(a):给出整个数组所占字节数
sizeof(a[0]):给出数组中单个元素所占字节
sizeof(a)/sizeof(a[0])两者相除即为数组的单元个数
1.这样的代码，一旦修改了数组中初始的数据，不需要修改遍历的代码
```

### 数组的赋值

```c
不能把a数组直接赋给b数组
int a[]={2,3,6,8,9};
int b[]=a;×
只能通过循环遍历a数组赋值给b数组
正确代码如下：
for(i=0;i<length;i++){
    b[i]=a[i];
}
```

### 数组作为函数参数时：

- [ ] 不能再[ ]中给出数组大小
- [ ] 不能再利用sizeof来计算数组的元素个数
- [ ] 往往必须再用另一个参数来传入数组的大小

eg:

```c
int cz(int key,int a[],int length){
    int ret=-1;
    int i;
    for(i=0;i<length;i++){
        if(a[i]==key){
            ret=i;
            break;
        }
    }
    return ret;
}
```

### 用数组构造素数表

```c
构造max以内的素数表：
1.令x=2
2.将2x,3x,4x直到ix<max的数标记为非素数
3.令x为下一个没有被标记为非素数的数，重复2
#include <stdio.h>
int main(){
    const int max=25;
    int isprime[max];
    int i;
    int x;
    for(i=0;i<max;i++){
        isprime[i]=1;//初始化数组使其中的每个元素都为1
    }
    for(x=2;x<max;x++){
        if(isprime[x]){
            for(i=2;i*x<max;i++){
                isprime[i*x]=0;
            }
        }
    }
    for(i=2;i<max;i++){
        if(isprime[i]){
            printf("%d\t",i);
        }
    }
    printf("\n");
    return 0;
}

```

### 井字棋（0,1）

```c
#include <stdio.h>

int main() {
    int board[3][3] = {
        // 在这里初始化你的棋盘
        {0,1,1},
        {1,0,0},
        {1,0,1}
    };

    int result = -1; // 初始化结果为-1，表示尚未找到全为0或全为1的行或列

    // 检查行和列
    for (int i = 0; i < 3 && result == -1; i++) {
        int num_0 = 0, num_1 = 0;
        for (int j = 0; j < 3; j++) {
            // 检查行
            if (board[i][j] == 0) {
                num_0++;
            } else if (board[i][j] == 1) {
                num_1++;
            }
            // 检查列
            if (board[j][i] == 0) {
                num_0++;
            } else if (board[j][i] == 1) {
                num_1++;
            }
        }
        // 如果行或列全为0或全为1，则设置结果
        if (num_0 == 3 || num_1 == 3) {
            result = num_1 == 3 ? 1 : 0;
        }
    }

    // 输出结果
    printf("Result: %d\n", result);

    return 0;
}
为了简化代码并使用两重循环来检查行和列，我们可以合并行和列的检查逻辑。这样，我们不需要单独处理对角线，因为行和列的检查会覆盖所有可能的直线情况（包括主对角线和次对角线）
```

## 指针

- [ ] 指针就是保存那个&取地址符得到的其他变量的地址的那么一个变量

### `&`运算符

`&` 运算符用于==获取==变量的内存地址。所以，`&x` 会给出 `x` 的内存地址。

```c
int x = 10;
int address_of_x = &x;
```

### 指针

指针是一个特殊的变量，用于==存储==另一个变量的内存地址。指针变量的类型决定了它可以指向哪种类型的变量。

```c
int *p;  // p 是一个指向 int 类型的指针
```

### `*` 运算符

- [ ] #### **解引用**：当 `*` 用于指针变量前面时，它表示获取该<u>==指针指向的值==</u>

```c
int x = 10;
int *p = &x;
int value = *p;  // value 现在为 10，因为 *p 获取了 p 指向的值，即 x 的值
```

- [ ] #### **定义指针**：当 `*` 用于变量类型前面时，它表示这是一个指针

```c
int *p;  // p 是一个指向 int 类型的指针
```

### 指针应用

- 函数返回运算的状态，结果通过指针返回
- 常用的套路是让函数返回特殊的不属于有效范围内的值来表示出错
  - -1或0
- 但是当任何数值都是有效的可能结果时，就需要分开返回了：状态由函数的return来返回，实际的值由指针参数返回

```c
eg：两个整数做除法的例子
#include <stdio.h>
int divide(int a,int b,int *result){
    int ret=1;
    if(b==0)
        ret=0;
    else
        *result=a/b;
    return ret;
}

int main(){
    int a=5,b=2,c;
    if( divide(a,b,&c) ){
        printf("%d/%d=%d",a,b,c);
    }
    return 0;
}
```

### 指针与数组的关系

- [ ] #### 数组变量是特殊的指针

- 数组变量本身表达地址，所以
  - `int a[10];int *p=a[0];//不需要用&取地址运算符`
  - 但是数组的单元表达的是变量，需要用&取地址
    - `int *p1==&a[6];//传递单个数组元素的地址的时候要有取地址符哦 ，传递首地址可以不加取地址符`
- [ ]运算符可以对数组做，也可以对指针做：
  - `p[0]等价a[0]`
- *运算符可以对指针做，也可以对数组做：
  - `*a=25;`
- 数组变量是const的指针，所以不能被赋值（这也解释了前面为什么不能把a数组直接赋给b数组）
  - `int a[]等价于int * const a`

- [ ] #### 详细的关系

  ==1.==**指针指向数组的首地址**：当一个指针变量被初始化成数组名时，该指针变量就指向了数组的首地址，也就是数组第一个元素的地址。例如，对于数组char str[20]和指针char *ptr，当执行ptr = str;后，ptr就指向了str数组的首地址。

  ==2.==**通过指针访问数组元素**：指针可以像数组下标一样用来访问数组中的元素。例如，ptr[i]就表示数组str中第i个元素的地址所存储的值，这等价于str[i]。

  ==3.==**指针与数组的关系**：虽然指针可以指向数组的首地址，但指针并不等同于数组。指针是一个变量，可以存储地址并可以进行加减运算等操作，而数组是一个固定大小的数据结构，不能改变大小。因此，<u>可以说指针指向数组，但不能说数组就是指针。</u>

  ==4.==**指针与数组的结合**：由于指针可以指向数组的首地址，并且可以通过指针来访问数组元素，因此指针和数组在编程中经常结合使用。这种结合使得对数组的处理更加灵活和方便，可以通过指针来实现对数组的遍历、查找、排序等操作。

  总之，数组和指针的关系密切，指针可以指向数组的首地址并通过指针来访问数组元素，但指针并不等同于数组。在编程中，指针和数组经常结合使用，以实现更加灵活和方便的操作。

### 指针与const的爱恨纠葛

#### 指针是const

- 表示一旦得到了某个变量的地址，不能再指向其他变量（==指针不可修改==）

  - ```c
    int *const p=&i;//p是const
    *p=26;//ok,因为*p代表的是i的值，而i并不是const,也就是说i可以改变，进而*p也可以改变
    p++;//error,p是const不能改变`
    ```

  - 

#### 所指的是const

- 表示不能通过这个指针p去修改指向的变量i（==通过指针不可修改==）

  - ```c
    const int *p=&i;//p所指的那个int不是普通的int，是个const
    *p=26;//error，不能通过*p去改变i的值，相当于只读
    i=26;//ok;i可以赋值变成其他值
    p=&j;//ok，p也可以变去指向其他
    ```

##### 判断哪个被const了的标准就是看const在*前还是后

```c
int i;
const int *p1=&i;//通过指针不可修改
int const *p2=&i;//通过指针不可修改
int *const p3=&i;//指针不可修改
const在*前就是：通过指针不可修改
const在*后就是：指针不可修改
```

#### const数组

```c
const int a[]={1,2,3,4,5,6};
1.数组变量a[]已经是const的指针了，前面的const表示数组的每个单元都是const int
2.所以必须通过初始化进行赋值（就是在大括号里写出每个单元的值），因为无法改变里面的值了
```

##### 保护数组值

- 因为把数组传入函数时传递的是地址，所以那个函数内部可以修改数组的值
- 如果前提要求需要为了保护数组不被函数破坏，可以设置参数为const

```c
int sum(const int a[],int length);
```

