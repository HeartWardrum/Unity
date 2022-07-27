## UDPClient类

提供用户数据报系欸（UDP）网络服务

### ReceiveAsync()

异步返回由远程主机发送的UDP数据报

返回值类型为`Task<UdpReceiveResult>` 表示异步操作的任务对象

### UdpReceiveResult结构

呈现UDP对ReceiveAsync()方法的调用的结果信息

## `ConcurrentQueue<T>`类

保证线程安全的先进先出集合

### ManualResetEvent

 多个线程可以通过调用ManualResetEvent对象的WaitOne方法进入等待或阻塞状态。当控制线程调用Set()方法，所有等待线程将恢复并继续执行。

  在内存中保持着一个bool值，如果bool值为False，则使所有线程阻塞，反之，如果bool值为True,则使所有线程退出阻塞。当我们创建ManualResetEvent对象的实例时，我们在函数构造中传递默认的bool值，以下是实例化ManualResetEvent的例子。

```
ManualResetEvent manualResetEvent = new ManualResetEvent(false);
```

在上面代码中，我们初始化了一个值为False的ManualResetEvent对象，这意味着所有调用WaitOne放的线程将被阻塞，直到有线程调用了 Set() 方法。而如果我们用值True来对ManualResetEvent对象进行初始化，所有调用WaitOne方法的线程并不会被阻塞，可以进行后续的执行。