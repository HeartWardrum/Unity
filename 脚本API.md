## 1. RigidBody.MovePosition

~~~~C#
public void MovePosition (Vector3 position);
//参数 position
//为Rigid'body对象提供新位置  新位置：当前位置+移动距离
//例如：
rigidBody.MovePosition(transform.position + transform.forward * Time.fixedDeltaTime * moveSpeed * inputV);
~~~~

## 2. Input.GetAxis()

`public static float GetAxis(string axisName);`      

**描述**

返回由 `axisName` 标识的虚拟轴的值。

对于键盘和游戏杆输入设备，该值将处于 -1...1 的范围内。该值的含义取决于输入控制的类型，例如，对于游戏杆的水平轴，值为 1 表示游戏杆向右推到底，值为 -1 表示游戏杆向左推到底；值为 0 表示游戏杆处于中性位置。如果将轴映射到鼠标，该值会有所不同，并且不会在 -1...1 的范围内。此时，该值为当前鼠标增量乘以轴灵敏度。通常，正值表示鼠标向右/向下移动，负值表示鼠标向左/向上移动。该值与帧率无关；使用该值时，您无需担心帧率变化问题。

~~~C#
 void Update()
    {
        inputH = Input.GetAxis("Horizontal"); //接收横向输入
        inputV = Input.GetAxis("Vertical");  //接收纵向输入
    }
~~~

## 3. Transform.eulerAngles

`public Vector3 eulerAngles`

**描述**

以欧拉角表示的旋转（以度为单位）。

Transform.eulerAngles表示世界空间中的旋转。在检视面板中查看 GameObject 的旋转时，可能会看到与此属性中存储的值不同的角度值。这是因为检视面板显示本地旋转。

欧拉角可以通过围绕各个轴执行三个单独的旋转来表示三维旋转。在 Unity 中，围绕 Z 轴、X 轴和 Y 轴（按该顺序）执行这些旋转。

可以通过设置此属性来设置四元数的旋转，并且可以通过读取此属性来读取欧拉角的值。

 使用 .eulerAngles 属性设置旋转时，务必要了解，虽然提供 X、Y 和 Z 旋转值描述旋转，但是这些值不存储在旋转中。而是将 X、Y 和 Z 值转换为四元数的内部格式。

读取 .eulerAngles 属性时，Unity 将四元数的内部旋转表示形式转换为欧拉角。因为可通过多种方式使用欧拉角表示任何给定旋转，所以读出的值可能与分配的值截然不同。如果尝试逐渐增加值以生成动画，则这种情况可能会导致混淆。

 若要避免这些类型的问题，使用旋转的建议方式是避免在读取 .eulerAngles 时依赖一致的结果，特别是在尝试逐渐增加旋转以生成动画时。

## 4. Mathf.Lerp

`public static float Lerp(float a,float b,float t);`

**参数**

| a    | 起点值。               |
| ---- | ---------------------- |
| b    | 终点值。               |
| t    | 两个浮点数之间的插值。 |

**返回**

`float 两个浮点值之间的插值浮点结果`

**描述**

- 在 `a` 与 `b` 之间按 `t` 进行线性插值
- 参数 `t` 限制在范围 [0, 1] 内
- 当 `t` = 0 时，返回 `a` 
- 当 `t` = 1 时，返回 `b` 
- 当 `t` = 0.5 时，返回 `a` 和 `b` 的中点      

## 5. Input.GetKeyDown

`public static bool GetKeyDown(string name);`     

在用户开始按下 `name` 标识的键的帧期间返回 true。

在Update方法中调用它，因为它的状态每帧都会重置；在用户释放按键并再次按下它之前，它不会返回true

## 6. Animator.CrossFade()

使用标准化时间创建从当前状态到任何其他状态的淡入淡出效果。

`Animator.CrossFade(string 状态名称,float 过渡的持续时间)`

## 7.BitConverter.GetBytes()

将字节数组转化为一个基数据格式

例如：

`byte[] _length = BitConverter.GetBytes(int型参数)`

## 8. Array.Copy(Array,Int32,Array,Int32,Int32)

复制 Array中的一系列元素（从指定的源索引开始），并将它们粘贴到另一Array中（从指定的目标索引开始）。 长度和索引指定为 32 位整数。

~~~Csharp
1. sourceArray   Array 
包含要复制的数据的 Array。
    
2. sourceIndex    Int32 
一个 32 位整数，它表示 sourceArray 中复制开始处的索引。

3. destinationArray    Array 
接收数据的 Array。
    
4. destinationIndex	Int32 
一个 32 位整数，它表示 destinationArray 中存储开始处的索引。
    
5. length	Int32 
一个 32 位整数，它表示要复制的元素数目。
~~~

















