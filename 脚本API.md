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

