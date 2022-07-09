————————————————
版权声明：本文为CSDN博主「swt369」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/swt369/article/details/78238130

————————————————

C#与Java的语法差异

    C与Java的语法差异
        前言
        程序结构
        基本语法
        数据类型
        字符串
        变量与常量
        运算符
        判断语句
        循环语句
        访问权限
        方法
        数组
        结构
        枚举
        类
        继承
        多态
        运算符重载
        接口
        命名空间
        预处理器指令
        正则表达式
        异常
        IO
        泛型
        集合
        属性
        索引器
        委托
        事件
        匿名方法

前言

本文主要供有Java基础的读者快速掌握C#基本语法使用，重点落在C#的语法上。
程序结构

C#中使用using关键字引用命名空间（namespace），作用和Java中使用import导入包中的类基本相同，都是为了避免命名冲突。

C#中文件名和类名可以不相同，但Java中文件名必须和主类名相同。

C#中方法名一般是让所有单词的首字母大写（ToString()），Java中一般是驼峰式，即除第一个单词外首字母大写(toString())。
基本语法

C#中标识符可以以字母、下划线以及@开头；Java中可以以字母、下划线以及$开头。
数据类型

C#中byte是8位无符号整型，sbyte是8位有符号整型；Java中byte是8位有符号整型。

C#中还有uint、ulong、ushort数据类型，是int、long、short的无符号版。

C#中使用sizeof()查看数据类型所占字节数（如sizeof(int)）；Java中通过包装类实现（如Integer.SIZE）。

C#中的动态（dynamic）类型的变量可以存储任何类型的值，例：

    dynamic d = 100;
    
    1

一般类型变量的类型检查在编译时发生，动态类型变量的类型检查在运行时才发生。比如下面的例子，编译器不会报错：

    dynamic d = 100.0;
    int x = d;
    
    1
    2

C#中可以使用指针，和C与C++中的指针功能相同。

C#中提供了一种特殊的类型：nullable类型。这种类型除了可以表示正常范围内的值外，还可以表示null值。使用方法是在数据类型后面加上一个？。例：

    int? x = null;
    double? y = null;
    
    1
    2

注意两点：
- 即便想使用null值，nullable类型仍需显示初始化为null。
- nullable类型和原类型不是同一种类型，如方法需要int，传递一个int?类型的变量会报错。
字符串

C#中可以使用一种逐字字符串，它会将所有转义字符当做普通字符处理，使用方法是在字符串前加上@：

    String str = @"c:\windows\";
    
    1

会输出c:\windows\，而不会将\视为转义字符。

C#中基本类型（int,float等）也可以调用ToString()转换成字符串。

Java中String类提供的各类字符串操作方法基本都能在C#中找到功能类似的实现。
变量与常量

C#中用const声明常量，Java中使用final声明常量。
运算符

C#中包含以下运算符：
- typeof()：返回class的类型。
- &,*：含义与使用方法同C,C++的指针。
- is：判断对象是否为某一类型，同Java的instanceof。
- as：强制将某个对象转成某个类型，转换失败也不会抛出异常。

要注意的是，在C#中，类内部声明的常量都是静态的，但不能加上static。示例：

    public class Persons
    {
        public const int SIZE = 10;
        private String[] names;
    }
    class Program
    {
        static void Main(string[] args)
        {
            int x = Persons.SIZE;
            Console.ReadLine();
        }
    }
    
    1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    11
    12
    13

可以看到，虽然SIZE没有用static修饰，它仍然是静态的。这和Java不同，Java中静态常量必须声明为static的。
判断语句

和Java基本相同。
循环语句

C#支持用foreach迭代数组或集合对象。语法示例如下：

    int[] array = new int[]{1,2,3,4,5};
    foreach (int element in array)
    {
    ...
    }
    
    1
    2
    3
    4
    5

Java中的foreach如下：

    int[] array = new int[]{1,2,3,4,5};
    for(int element : array){
    ...
    }
    
    1
    2
    3
    4

访问权限

C#中public,private,protected的含义与Java相同。不同之处如下：
- C#中没有包的概念，自然也没有包级私有访问权限。
- C#特有：internal——同一个程序集的对象可以访问；protected internal——同一个程序集内的派生类可以访问，是internal与protected的交集。
- C#成员变量和成员方法默认private，类默认internal，接口方法默认public；Java除接口默认public外默认为包级私有。
方法

C#的参数传递分为三种：
（1）值参数：默认的方式，复制实参给形参，形参的改变不会改变实参。

（2）引用参数：复制实参的内存位置的引用给形参，形参的改变会影响实参。引用参数用ref声明：

    public static void Swap(ref int x, ref int y)
    {
        int temp;
    
        temp = x;
        x = y;
        y = temp;
    }
    
    1
    2
    3
    4
    5
    6
    7
    8

使用时也要给参数加上ref：

    int x = 1;
    int y = 2;
    Swap(ref x, ref y);
    
    1
    2
    3

上面的方法调用会改变x和y的值。

（3）输出参数：C#的return只能从方法中返回一个值，但是使用输出参数就可以返回多个值。输出参数用out声明：

    public static void GetValue(out int x)
    {
        x = 5;
    }
    
    1
    2
    3
    4

提供给输出参数的变量不需要赋值，不过传递给方法时要加上out：

    int a;
    GetValue(out a);
    Console.WriteLine(a);
    
    1
    2
    3

会发现a已经被成功赋值。
注意：如果方法中未给输出参数赋值，编译器会报错。

C#中的变长参数列表是通过在方法的参数列表中用params声明一个数组实现的：

    public int AddElements(params int[] arr)
    {
       int sum = 0;
       foreach (int i in arr)
       {
          sum += i;
       }
       return sum;
    }
    
    1
    2
    3
    4
    5
    6
    7
    8
    9

数组

C#中只能使用类似int[] array的方式来声明数组，不能使用int array[]的方式。Java中二者均可。

C#多维数组：用[,]声明二维数组，[ , , ]声明三维数组，以此类推。示例：

    int[,] array = new int[3, 4]
    {
        {1, 2, 3, 4 },
        {5, 6, 7, 8 },
        {9, 10, 11, 12}
    };
    
    1
    2
    3
    4
    5
    6

使用array[x,y]引用上面的数组的元素。

C#交错数组：即数组的数组，用[][]这样的方式声明。示例：

    int[][] arr = new int[3][];
    
    1

声明该数组时不会为其分配内存，需要单独创建它的每个元素（也是一个数组）。每个数组元素的长度可以不同。
结构

C#中能够定义和使用结构struct。和C,C++的结构体的区别在于：
- 结构可带有方法、字段、索引、属性、运算符方法和事件。
- 结构可以定义构造函数，但不能定义析构函数。不能覆盖结构的默认构造函数，它会自动被定义，且不能改变。
- 结构不能继承其他的结构或类，也不能作为其他结构和类的基础结构。
- 结构可实现一个或多个接口。
- 结构成员不能声明为abstract、virtual、protected。
- 结构即使不使用New操作符也能完成实例化，但也可使用New以调用合适的构造函数。
- 结构的字段必须先赋值后才能使用。

和类的区别在于：
- 类是引用类型，结构是值类型。
- 结构不支持继承。
- 结构不能声明默认构造函数。
枚举

C#中的枚举和C,C++类似，是一组命名整型常量，不能像Java那样在枚举中声明方法。示例：

    enum Days { Sun, Mon, tue, Wed, thu, Fri, Sat };
    
    1

默认情况下，第一个枚举符号的值为0，后面依次递增1。不过也可以以赋值的方式自定义各个枚举符号的值。
类

C#的类支持析构函数，析构函数的名称是在类名前加上一个~。它没有返回值，也不带任何参数。

C#支持静态成员和静态方法。

C#的静态初始化块的写法和Java的static{}不同，是使用一种静态构造器的方式：

    // Static variable that must be initialized at run time.
    static readonly long baseline;
    
    // Static constructor is called at most one time, before any
    // instance constructor is invoked or member is accessed.
    static SimpleClass()
    {
        baseline = DateTime.Now.Ticks;
    }
    
    1
    2
    3
    4
    5
    6
    7
    8
    9

继承

C#的继承写法：class Rectangle : Shape；Java的继承写法：class Rectangle extends Shape。

关于在构造器中调用父类的构造器，C#中写法为：public Rectangle(String name) : base(name)；Java中写法为在构造器第一行加上super(参数列表)。

关于串联构造器，C#中写法为：public Rectangle(String name) : this(参数列表)，Java中写法为在第一行加上this(参数列表)。

C#的base与this和Java的super与this在其他用法上基本相同。

C#不支持多重继承，但可以实现多个接口，这点和Java一样。但C#实现接口不用implements，而是直接和继承类一样写在冒号后面，如：class Rectangle : Shape, SomeInterface
多态

C#的重载规则和Java类似，个数和类型不同能够触发重载，返回值类型不同不能触发重载。

C#中可被子类覆盖的成员方法需要在访问控制权限后面加上virtual关键字，Java中默认所有成员方法都可被子类覆盖，加上final可让方法无法被覆盖。

C#中，当子类覆盖父类的方法时，需要加上override关键字，Java中不需要。

C#中，可以将方法声明为abstract的，表示该方法应交由子类实现。包含abstract方法的类本身必须也是abstract的，即无法实例化的抽象类。

C#中，在类定义前加上sealed可以让类无法被继承，Java中使用final关键字实现该效果。
运算符重载

C#支持运算符重载。定义运算符重载的方法必须为静态方法，拥有返回值和参数列表，方法名为operator后跟对应的运算符。例：

    public class Point
    {
        public int x;
        public int y;
        public Point(int x, int y)
        {
            this.x = x;
            this.y = y;
        }
    
        //重载+运算符
        public static Point operator+ (Point a, Point b)
        {
            return new Point(a.x + b.x, a.y + b.y);
        }
    }
    
    static void Main(string[] args)
    {
        Point a = new Point(1, 2);
        Point b = new Point(2, 1);
        //运算符重载
        Point c = a + b;
        Console.WriteLine("x={0}, y={1}", c.x,c.y);
        Console.ReadLine();
    }
    
    1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    11
    12
    13
    14
    15
    16
    17
    18
    19
    20
    21
    22
    23
    24
    25
    26

下面是对各个运算符能否重载的总结：
- +, -, !, ~, ++, – 这些一元运算符只有一个操作数，且可以被重载。
- +, -, *, /, % 这些二元运算符带有两个操作数，且可以被重载。
- ==, !=, <, >, <=, >= 这些比较运算符可以被重载。
- &&, || 这些条件逻辑运算符不能被直接重载。
- +=, -=, *=, /=, %= 这些赋值运算符不能被重载。
- =, ., ?:, ->, new, is, sizeof, typeof 这些运算符不能被重载。

Java中不能自定义运算符重载。
接口

C#中接口内方法默认public。接口支持继承。这些和Java基本一致。

C#中接口名称通常以I开头。

C#中，实现接口中的方法时不需要加上override（实际上是不能，会报错）。
命名空间

命名空间namespace是C#独有。命名空间的定义方法如下：

    namespace namespace_name
    {
        class A{
    
        }
    }
    
    1
    2
    3
    4
    5
    6

使用命名空间中的类时需要加上命名空间名和’.’：

    namespace_name.A a = new namespace_name.A();
    
    1

可以在开头加上using 命名空间名，这样就不用每次引用命名空间中的类时加上前缀。

命名空间可以嵌套，即可以在一个命名空间中声明另一个命名空间。

其他命名空间用法：
（1）using static 指令：指定无需指定类型名称即可访问其静态成员的类型

    using static System.Math;var = PI; // 直接使用System.Math.PI
    
    1

（2）起别名

    using Project = PC.MyCompany.Project;
    
    1

（3）using语句：将实例与代码绑定

    using (Font font3 = new Font("Arial", 10.0f),
                font4 = new Font("Arial", 10.0f))
    {
        // Use font3 and font4.
    }
    
    1
    2
    3
    4
    5

代码段结束时，自动调用font3和font4的Dispose方法，释放实例。
预处理器指令

C#的预处理器指令源于C,C++。可用的预处理器指令如下：

#define 它用于定义一系列成为符号的字符。
#undef  它用于取消定义符号。
#if 它用于测试符号是否为真。
#else   它用于创建复合条件指令，与 #if 一起使用。
#elif   它用于创建复合条件指令。
#endif  指定一个条件指令的结束。
#line   它可以让您修改编译器的行数以及（可选地）输出错误和警告的文件名。
#error  它允许从代码的指定位置生成一个错误。
#warning    它允许从代码的指定位置生成一级警告。
#region 它可以让您在使用 Visual Studio Code Editor 的大纲特性时，指定一个可展开或折叠的代码块。
#endregion  它标识着 #region 块的结束。

    1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    11

使用示例：

    #define DEBUG
    #define VC_V10
    using System;
    public class TestClass
    {
       public static void Main()
       {
          #if (DEBUG && !VC_V10)
             Console.WriteLine("DEBUG is defined");
          #elif (!DEBUG && VC_V10)
             Console.WriteLine("VC_V10 is defined");
          #elif (DEBUG && VC_V10)
             Console.WriteLine("DEBUG and VC_V10 are defined");
          #else
             Console.WriteLine("DEBUG and VC_V10 are not defined");
          #endif
          Console.ReadKey();
       }
    }
    
    输出：DEBUG and VC_V10 are defined
    
    1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    11
    12
    13
    14
    15
    16
    17
    18
    19
    20
    21

正则表达式

C#同样支持正则表达式。C#中的正则表达式的优势在于，可以使用逐字字符串（双引号前加@）来简化输入（不需要考虑字符串本身的转义，但正则表达式的转义仍需考虑）。具体的正则表达式语法规则和Java基本一致。
异常

C#中不能在方法后面用throws指明可能抛出的异常类型，其余和Java一致。
I/O

C#的I/O与文件系统体系和Java很像，但具体使用上会产生差异。
具体见http://www.runoob.com/csharp/csharp-file-io.html
泛型

C#中，声明泛型类的方法和Java相同，都是在声明类时在类名后面加<泛型参数列表>，但声明泛型方法的语法不太一样，体现在不需要声明泛型参数列表上。下面是C#中一个泛型方法的声明与使用：

    public static void Swap<T>(ref T a, ref T b)
    {
        T temp;
    
        temp = a;
        a = b;
        b = temp;
    }
    
    static void Main(string[] args)
    {
        int x = 10;
        int y = 20;
        Swap(ref x, ref y);
        Console.WriteLine(x);
        Console.WriteLine(y);
        Console.ReadLine();
    }
    
    1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    11
    12
    13
    14
    15
    16
    17
    18

Java中的话，Swap方法的返回值前还得加上<T>。
集合

Java中的集合几乎都能在C#中找到对应的实现，名称也基本相同,除了Map。C#对应Map的集合类是Dictionary类。
属性

属性是C#独有的语法，它形式上类似于在字段的基础上添加了get和set两个访问器形成的。下面是一个例子：

    class Person
    {
        private int age;
        public int Age
        {
            get
            {
                return age;
            }
            set
            {
                if (value <= 200)
                {
                    age = value;
                }
                else
                {
                    throw new Exception("");
                }
            }
        }
    }
    
    1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    11
    12
    13
    14
    15
    16
    17
    18
    19
    20
    21
    22

Age就是一个属性。当外部需要获取Age的值时会自动调用get，当外部需要设置Age的值时会自动调用set。注意set中的value，它指代的是外部想要为其设置的值。
对于声明了属性的类，还可以用下面的方式来初始化：

    Person person = new Person
    {
        Age = 15
    };
    
    1
    2
    3
    4

访问属性时时使用属性名，而不是字段名：

    int x = person.Age;
    person.Age++;
    
    1
    2

注意Age = 15后面没有分号。

属性可以只有get，也可以只有set，但不能两个都没有。

还能够像这样声明自动完成的属性，并设置初始值：

    public String Name { get; set; } = "father";
    
    1

可以为属性的某个访问器声明访问控制权限。

类还可以使用virtual或者abstract声明一个属性，它们可以在子类中覆盖或实现。
索引器

C#的索引器允许一个对象像一个数组一样被索引。当为一个类声明了索引器，就可以用对象名[]的方式访问对象的一些字段。
索引器用下面的语法声明：

    element-type this[int index]
    {
       // get 访问器
       get
       {
          // 返回 index 指定的值
       }
    
       // set 访问器
       set
       {
          // 设置 index 指定的值
       }
    }
    
    1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    11
    12
    13
    14

示例：

    public class Persons
    {
        public const int SIZE = 10;
        private String[] names = new String[SIZE];
    
        public Persons()
        {
            for(int i = 0; i < SIZE; i++)
            {
                names[i] = i.ToString();
            }
        }
    
        public String this[int index]
        {
            get
            {
                String temp = "";
                if(index >= 0 && index < SIZE)
                {
                    temp = names[index];
                }
                return temp;
            }
            set
            {
                if (index >= 0 && index < SIZE)
                {
                    names[index] = value;
                }
            }
        }
    }
    class Program
    {
        static void Main(string[] args)
        {
            Persons persons = new Persons();
            for(int i = 0; i < Persons.SIZE; i++)
            {
                Console.WriteLine(persons[i]);
            }
            Console.ReadLine();
        }
    }
    
    1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    11
    12
    13
    14
    15
    16
    17
    18
    19
    20
    21
    22
    23
    24
    25
    26
    27
    28
    29
    30
    31
    32
    33
    34
    35
    36
    37
    38
    39
    40
    41
    42
    43
    44
    45

索引器还可以被重载，重载规则和方法的相同。
委托

C#中有一种叫委托的引用类型，它和C,C++的函数指针很像，用来持有某个方法的引用。引用可在运行时改变。
委托在C#中常被用于实现事件和回调方法。

委托使用delegate关键字声明，形式上和接口中的一个方法很像。委托可指向一个与其签名相同的方法。下面是一个示例：

    public delegate int DoSomething(int x);
    
    1

这个委托的实例可指向一个参数为一个int且返回值也为int的方法，下面是使用示例：

    class Program
    {
        public delegate int DoSomething(int x);
    
        public static int AddOne(int a)
        {
            return a + 1;
        }
    
        public int MinusOne(int a)
        {
            return a - 1;
        }
    
        static void Main(string[] args)
        {
            int x = 10;
            DoSomething doSomeThing = new DoSomething(Program.AddOne);
            Console.WriteLine(doSomeThing(x));
    
            Program program = new Program();
            DoSomething doSomething2 = new DoSomething(program.MinusOne);
            Console.WriteLine(doSomething2(x));
    
            Console.ReadLine();
        }
    }
    
    1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    11
    12
    13
    14
    15
    16
    17
    18
    19
    20
    21
    22
    23
    24
    25
    26
    27

委托实例还可以利用+、-、+=、-=、=等进行各种方法拼接、移除操作，这叫做委托的多播。调用这样的委托的实际效果相当于按照顺序依次调用一系列的方法。
事件

事件是C#的一种实现进程间通信的机制，使用发布-订阅模型。
事件由委托和event关键字声明。下面是完整地实现一个事件的过程：
（1）声明事件的委托类型：

    public delegate void NumManipulationHandler(int value);
    
    1

（2）使用event关键字声明事件：

    public event NumManipulationHandler NumChanged;
    
    1

（3）利用委托的多播，在事件上使用+、-等实现订阅/取消订阅。
下面是一个完整的例子:

    public class Publisher
    {
        private int value = 0;
    
        public delegate void NumManipulationHandler(int value);
        public event NumManipulationHandler NumChanged;
    
        protected virtual void OnNumChanged()
        {
            if(NumChanged != null)
            {
                NumChanged(value);
            }
        }
    
        public void SetValue(int x)
        {
            if(value != x)
            {
                value = x;
                OnNumChanged();
            }
        }
    }
    
    class Subscriber
    {
        public void Printf(int value)
        {
            int x = value;
            Console.WriteLine("new value: {0}",x);
        }
    }
    
    class Program
    {
        static void Main(string[] args)
        {
            Publisher publisher = new Publisher();
            Subscriber subscriber = new Subscriber();
    
            publisher.NumChanged += new Publisher.NumManipulationHandler(subscriber.Printf);
    
            publisher.SetValue(100);
            publisher.SetValue(200);
    
            Console.ReadLine();
        }
    }
    
    1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    11
    12
    13
    14
    15
    16
    17
    18
    19
    20
    21
    22
    23
    24
    25
    26
    27
    28
    29
    30
    31
    32
    33
    34
    35
    36
    37
    38
    39
    40
    41
    42
    43
    44
    45
    46
    47
    48
    49

其实这和Java中先定义回调接口，之后在外部实现回调接口的思想很像。
匿名方法

有些委托实现可能只会使用一次，因此可以用匿名的方式传递给需要委托的方法，和Java的匿名内部类非常相似。示例：

    public delegate void DoSomething(int x);
    
    DoSomething doSomething = delegate (int x)
    {
        Console.WriteLine(x);
    };
