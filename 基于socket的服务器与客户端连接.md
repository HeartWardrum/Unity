## TCP

~~~Csharp
//服务器端
using System;
using System.Net;
using System.Net.Sockets;

namespace Tcp服务器端
{
    class Program
    {
        static void Main(string[] args)
        {
            //创建一个插口，给定它的标准
            Socket tcpServer = new Socket(AddressFamily.InterNetwork, SocketType.Stream, ProtocolType.Tcp);//第一个参数：使用IPV4地址  第二个参数：使用流类型进行传输 第三个参数：通信协议使用TCP

            //10.0.248.2
            IPAddress ipAddress = new IPAddress(new byte[] { 10, 0, 248, 2 });//获取IP地址
            IPEndPoint ipEndPoint = new IPEndPoint(ipAddress, 7788);//声明一个终端 传入IP地址和端口号

            tcpServer.Bind(ipEndPoint);//绑定IP地址和端口号
            tcpServer.Listen(100);//指定最大连接数  此处最多100人连接此服务器

            Console.WriteLine("开始接客了....");
            Socket client = tcpServer.Accept();//获取客户端的Socket
            Console.WriteLine("一个客户端连接过来了");

        }
    }
}
~~~

~~~Csharp
//客户端
using System;
using System.Net;
using System.Net.Sockets;

namespace Tcp客户端
{
    class Program
    {
        static void Main(string[] args)
        {
            Socket tcpClient = new Socket(AddressFamily.InterNetwork, SocketType.Stream, ProtocolType.Tcp);
            IPAddress ipAddress = new IPAddress(new byte[] { 10, 0, 248, 2 });
            IPEndPoint ipEndPoint = new IPEndPoint(ipAddress, 7788);
            tcpClient.Connect(ipEndPoint);//发送连接请求
            Console.WriteLine("已连接上服务器端");
        }
    }
}
~~~

## 序列化和反序列化

### 1. 什么是序列化、反序列化

序列化：将对象转化为容易传输的格式

反序列化：重新解析构造被序列化的对象

### 2. 为什么要序列化、反序列化

1. 数据是以二进制序列的方式在网络上传送的。

~~~Csharp
//服务器端
using System;
using System.Net;
using System.Net.Sockets;
using System.Text;

namespace Tcp服务器端
{
    class Program
    {
        static void Main(string[] args)
        {
            //创建一个插口，给定它的标准
            Socket tcpServer = new Socket(AddressFamily.InterNetwork, SocketType.Stream, ProtocolType.Tcp);//第一个参数：使用IPV4地址  第二个参数：使用流类型进行传输 第三个参数：通信协议使用TCP

            //10.0.248.2
            IPAddress ipAddress = new IPAddress(new byte[] { 10, 0, 248, 2 });//获取IP地址
            IPEndPoint ipEndPoint = new IPEndPoint(ipAddress, 7788);//声明一个终端 传入IP地址和端口号

            tcpServer.Bind(ipEndPoint);//绑定IP地址和端口号
            tcpServer.Listen(100);//指定最大连接数  此处最多100人连接此服务器

            Console.WriteLine("开始接客了....");
            Socket client = tcpServer.Accept();//获取客户端的Socket
            Console.WriteLine("一个客户端连接过来了");

            //接收客户端发来的消息
            byte[] data = new byte[1024];//声明一个字节数组 作为接收缓冲区
            int length = client.Receive(data);//Receive方法将接收到的数据存入（接收缓冲区）一个字节数组
            string message = Encoding.UTF8.GetString(data, 0, length);//从接收缓冲区中解码出字符串
            Console.WriteLine("接收到客户端发来的数据：\n" + message);

            //向客户端发送消息
            client.Send(Encoding.UTF8.GetBytes("welcome client! This is server"));

            //关闭连接  先打开的后关闭
            client.Close();
            tcpServer.Close();
        }
    }
}
~~~

~~~Csharp
//客户端
using System;
using System.Net;
using System.Net.Sockets;
using System.Text;

namespace Tcp客户端
{
    class Program
    {
        static void Main(string[] args)
        {
            Socket tcpClient = new Socket(AddressFamily.InterNetwork, SocketType.Stream, ProtocolType.Tcp);
            IPAddress ipAddress = new IPAddress(new byte[] { 10, 0, 248, 2 });
            IPEndPoint ipEndPoint = new IPEndPoint(ipAddress, 7788);
            tcpClient.Connect(ipEndPoint);//发送连接请求
            Console.WriteLine("已连接上服务器端");

            //向服务器端发送数据
            string message = "hello server! This is client";
            tcpClient.Send(Encoding.UTF8.GetBytes(message));//转换成一个字节数组传入Send方法————序列化

            //接收服务器端的数据
            byte[] data = new byte[1024];
            int length = tcpClient.Receive(data);
            Console.WriteLine("客户端收到的消息：\n" + Encoding.UTF8.GetString(data, 0, length));

            //关闭连接
            tcpClient.Close();
        }
    }
}
~~~

## UDP

### ref

传入参数的前面加上ref后，如果方法对参数进行了修改，会直接影响方法外该参数的值

~~~Csharp
		//比如
        static void Main(string[] args)
        {
            int a = 0;
            Test(ref a);
            Console.WriteLine("a = " + a);//输出 a = 1
        }

        static void Test(ref int a)
        {
            a += 1;
        }
~~~

