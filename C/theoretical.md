# 基础1
1. C程序中定义的变量，代表内存中的一个存储单元。 T
2. 在C语言中，单目运算符需要**1**个操作数。
3. 程序总是从main 函数开始执行的 T
4. 假设赋值运算符的优先级比算术运算符高，执行以下程序段后，n的值为10。 T
    ```c
    int n; 
    n = 10 + 2;
    ```
5. 如果变量已经正确定义，则执行以下程序段后，x的值不变。F
    ```c
    if (x = 20) {
        y = 1;
    } else {
        y = 0;
    }  
    ```
6. 输入scanf匹配：&lf->double;"x=%lf"->也要输入'x='
7. 输入scanf记得 **'&'**
8. 要记得初始化
    执行以下程序段，sum的值是55 F
    ```c
    int i, sum;
    for (i = 1; i <= 10; i++){
        sum = sum + i;
    }
    ```
9. scanf自动分类(?)
若x是double型变量，n是int型变量，执行以下语句，并输入3  1.25后，x的值是1.25，n的值是3。
    ```c
    scanf("%d%lf",&n,&x);
    ```
1. for 循环本质
    ```c
    int i, sum;
    sum = 0;
    for (i = 1; i <= 10; i++){ //in the end i = 11
        sum = sum + i;
    }
    ```
    ```c
    int fahr;
    double celsius;   
    for (fahr = 121 ; fahr <= 125; fahr++) ;  //循环体执行了5次，结束时fahr=126
    celsius = 5.0 * (fahr - 32) / 9.0;
    printf("%4d%6.1f\n", fahr, celsius);
    ```
11. math.h库
    sqrt() fabs() pow() 
    exp(x) -> e**x
    log(x) -> lnx
    log10(x)

# 基础2

1. 在嵌套使用if语句时，C语言规定else总是**和之前与其最近的且不带else的if配对**
2. 设变量已正确定义，执行以下程序段，顺序输入三个字符'Q'，则输出Q。 F(三个“字符”，' and Q and ')
    ```c
    ch = getchar(); 
    putchar(ch); 
    ```
3. switch语句中 case后必须是常量表达式 ~~case op == '+'~~ ~~小数~~ 且**不能重复**！
    - 特殊的重复情况:k=12时会导致重复
    ```c
    n = 10;
    switch ( k ) {
        case n%3: printf("one");
        case n%4: printf("two");
        default: printf("zero");
    }
    ```
    switch('\\') ok
    ~~你会拼default吧~~
4. 坑人题
    ```c
    //写出以下程序段的运行结果。请注意，直接填单词，前后不要加空格等任何其他字符。
    mynumber = 38;
    scanf ("%d", &yournumber); 
    if(yournumber == mynumber){ 
        printf("Right");
    }
    if(yournumber > mynumber ){
        printf("Big");
    }else{ 
        printf("Small");
    }
    //输入38->RightSmall
    ```
    ```c
    int  a;
    scanf("%d", &a);
    if(a > 50)  printf("%d", a);
    if(a > 40)  printf("%d", a);
    if(a > 30)  printf("%d", a);    
    //input 46 -> 4646
    ```
    ```c
    for(num = 1; num <= 100; num++){ 
        s = 0;
        do{
        s = s + num % 10;
        num = num / 10;
        }while(num != 0);
        printf("%d\n", s); 
    }
    //循环内的num改变，导致循环错位啦
    ```
    ```c
    scanf ("%d", &m);
    is_prime = 1;
    limit = sqrt(m) + 1;
    for(i = 3; i <= limit; i += 2){ 
        if(m % i == 0){
            break; 
            is_prime = 0; 
        }
    }    
    //break 后面的不执行了， iput 25 -> 1
    ```
5. 用脑警告
    ```c
    int i, j, m, n; 
    scanf("%d", &n);
    m = n/2;
    for (i=m+1;i>0;i--) { //1
        for (j=1;j<=m+1-i;j++) //2 {
            printf (" ");
        }for (j = 1; j <= 2 * i - 1; j++){
            printf ("*");
        }printf ("\n");
    }
    for (i=2;i<=m+1;i++) { //3
        for (j=1;j<=m+1-i;j++) { //4
            printf (" ");
        }for (j = 1; j <= 2 * i - 1; j++){
            printf ("*");
        }printf ("\n");
    }

    input like->
    *****
     ***
      *
     ***
    *****

# 基础3-函数
1. 函数定义时的参数是形参（变量），调用时是实参（变量、常量、表达式）。
2. 函数结构
    
    ```c
    double cylinder(double r, double h), anotherfunc(int x); //声明
    int main(){
        double cylinder(a, b); //调用
        return 0;
    }
    double cylinder(double r, double h) { //定义
        ---
    }
    ```ignore this
    ```
    ```c
    double cylinder(double r, double h) { //定义
        ---
    }
    int main(){
        double cylinder(a, b); //调用
    }
    ```
3. 局部变量：在函数内定义作用在本函数内部，在复合语句内定义作用在复合语句内部。
4. 全局变量：在函数以外定义，作用从定义处到源文件结束（包括各个函数）;程序中，储存单元始终保持；没赋初值为0。
5. 局部变量与全局变量同名，局部变量优先
    ```c
    int x = 5, y = 6;
    void incxy( )
    {   
        x++;
        y++;
    }
    int main(void )
    {   
        int x = 3;
            
        incxy( ); //全局变量x=6，y=7
        printf("%d, %d\n", x, y); //由于局部变量优先，x取局部变量3
            
        return 0;
    }
    output->3, 7
    ```
6. 自动变量（普通局部变量）：auto int x
   - 调用时定义变量分配储存单元，结束时收回储存单元。
   - 没赋初值，为随机
    ```c
    fun(int a, int b, int c)
    {   c = a * b;  }
    int main(void)
    {
        int c;

        fun(2, 3, c);
        printf(“%d\n”, c);

        return 0;
    }
    output unsure
    ```
7. 静态局部变量 static 类型名 变量表
    - 作用范围：局部变量
    - 生命周期：全局变量
    - 没赋初值，为0；以后调用按前一次调用保留的值
    - 不能作用于其他函数（包括主函数）
    ```c
    double fact_s(int n){
        static double f = 1; //定义静态变量，第一次赋值为1
        f = f * n; //在上一次调用时的值上乘n
        return(f);
    }
    int main(){
        int n;
        scanf("%d", &n);
        for (int i = 1; i <= n; i++){
            printf("%3d!=%.0f\n",i,fact_s(i));
        }return 0;
    }
    ```
    ```c
        # include <stdio.h>
    int f(int n)
    {      static int k, s; //第一次调用后，s=3，在此基础上s+2+1=6

        n--;
        for(k=n; k>0; k--)
        s += k;
        return s;
    }
    int main(void)
    {      int k;

        k=f(3); //k=3
        printf("(%d,%d)", k, f(k));

        return 0;
    }

    output->(3,6)
    ```
8. 在C语言的函数定义中，如果不需要返回结果，就可以省略return语句。在C语言的函数定义中，如果省略了return语句，函数就~~无法~~返回主调函数。
9.  函数未被调用时，系统将不为形参分配内存单元
10. 实参和形参的个数必须相等，但类型不一定一致，float类型的实参可以传递给double类型的形参。
11. 在C语言程序中，若对函数类型未加显式说明，则函数的隐含类型为**int**
12. 实参与其对应的形参各占用独立的存储单元
13. 在函数调用Func(exp1 , exp2+exp3 , exp4*exp5)中，实参的数量是 （3）。 
14. 函数是一个完成特定工作的独立程序模块，包括**库函数**和**自定义函数**两种

# 基础4-数据类型和表达式
1. !(x>0||y>0) <=> !(x>0)&&!(y>0)
   only TRUE when x,y both <= 0
2. if sizeof(int) is 4, the max integer is **2<sup>31</sup>-1**
3. (z=0,(x=2)||(z=1),z)
    in (x=2)||(z=1), x=2 return 2, because of '||', z=1 won't be executed
    so ultimat output is **0**
4. c语言 三目 ：exp1 ? exp2 : exp3
5. 输出：k=11,k=13,k=b
    ```c
    int k=11;
    printf("k=%d,k=%o,k=%x\n",k,k,k);
    ```
6. 阅读以下程序段，如果从键盘上输入abc<回车>，则程序的运行结果是（ a ）。
    ```c
    char ch;
    scanf("%3c",&ch);
    printf("%c",ch);
    ```
7. 输出20
   a*4这个语句纯纯执行，但对a没有赋值
    ```c
    int a;
    printf("%d\n",(a=3*5,a*4,a+5));
    ```
8. 设字符型变量x的值是064，表达式 ~ x ^ x << 2 & x 的值是
    八进制064->52->0011 0100
    从右到左，<<更优先，正确执行顺序：~ x ^ ((x << 2) & x)
    x<<2 : 1101 0000
    ((x << 2) & x) : 0001 0000
    x ^ ((x << 2) & x) :0010 0100
    \- 0010 0100 : 1101 1011 -> 219 -> 0333
9. 正确赋值语句
    - t += 1;
    - n1 = (n2 =(n3 = 0));&nbsp;&nbsp;全为0
    - k = i = j
10. x&&1 <=> x!=0
