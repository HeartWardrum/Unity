## 简单连接

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

