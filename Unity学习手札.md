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

## Time.deltaTime

deltaTime 增量时间

Update函数是每帧执行一次，那么经过一帧耗费的时间就是**增量时间**

1秒内Update执行的次数，就是一秒内执行的总帧数

Update1秒内执行了1次，`transform.Translate(0, 0, 1/60 \* 10)`执行一次，物体移动了1/6米

Update1秒内执行了60次，就是`transform.Translate(0, 0, Time.deltaTime * 10)`乘以60次

相当于 =（每帧时间 \* 速度 \* 每秒几帧）=10米

## OnCollisionEnter

经过测试： OnCollisionEnter方法被触发要符合以下条件：

> 1 碰撞双方必须是碰撞体
> 2 碰撞的主动方必须是刚体，注意我的用词是主动方，而不是被动方
> 3 刚体不能勾选IsKinematic
> 4 碰撞体不能够勾选IsTigger

注意OnCollisionEnter方法的形参对象指的是碰撞双方中没有携带OnCollisionEnter方法的一方

## Collision.gameObject

您正在碰撞其碰撞体的GameObject（只读）

这是正在与您 GameObject 碰撞的 GameObject。访问它，以检查正在碰撞的 GameObject 的属性，例如 GameObject 的名称和标记
