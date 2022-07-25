## UDPClient类

提供用户数据报系欸（UDP）网络服务

### ReceiveAsync()

异步返回由远程主机发送的UDP数据报

返回值类型为`Task<UdpReceiveResult>` 表示异步操作的任务对象

### UdpReceiveResult结构

呈现UDP对ReceiveAsync()方法的调用的结果信息

## `ConcurrentQueue<T>`类

保证线程安全的先进先出集合