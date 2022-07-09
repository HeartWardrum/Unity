## 为什么刚体组件在FixedUpdate()中运行地更加流畅？

### FixedUpdate()与Update()区别？

~~~C#
	Update是在每次渲染新的一帧的时候才会调用，也就是说，这个函数的更新频率和设备的性能有关以及被渲染的物体（可以认为是三角形的数量）。在性能好的机器上可能fps 30，差的可能小些。这会导致同一个游戏在不同的机器上效果不一致，有的快有的慢。因为Update的执行间隔不一样了。

    而FixedUpdate，是在固定的时间间隔执行，不受游戏帧率的影响。有点想Tick。所以处理Rigidbody的时候最好用FixedUpdate。
~~~

## 添加刚体的物体在程序运行时发生侧翻原地乱滚

- Rigidbody组件 ---- Constraints ---- Freeze Rotation 全部勾上

## 本地坐标和世界坐标

### 世界坐标系

原点：世界的中心
 轴向：世界坐标系的三个轴向是固定的
 相关API:

- `transform.position;`
- `transform.rotation; 四元数`
- `transform.eulerAngles; 欧拉角`
- `transform.lossyScale;`

移动根据世界坐标系移动 

### 本地坐标系

原点：物体的中心点（建模时决定,一般都是物体的中心点）
轴向：

- 物体右方为X轴正方向

- 物体上方为Y轴正方向

- 物体前方为Z轴正方向

  相关API:

  - `transform.localPosition;`
  - `transform.localRotation; 本地四元数`
  - `transform.localEulerAngles; 本地欧拉角`
  - `transform.localScale;`

物体移动根据自己的父物体决定 
