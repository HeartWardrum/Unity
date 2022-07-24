## Struct

结构体

是值类型数据结构。它使得一个单一变量可以存储各种数据类型的相关数据

~~~Csharp
       public struct Books
        {
            public string title;
            public int book_id;
        };

        static void Main(string[] args)
        {
            Books book1 = new Books();//在堆空间开辟一块区域为struct的字段赋初值null和0
            book1.title = "你好世界";
            book1.book_id = 1;
            Console.WriteLine("第一本书的标题：" + book1.title);
            Console.WriteLine("第一本书的编号：" + book1.book_id);
        }
~~~

