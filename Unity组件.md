## 1. Rigidbody组件



| Mass                | 质量         | 物体的质量（任意单位）。建议一个物体的质量不要与其他物体 相差100倍 |
| ------------------- | ------------ | ------------------------------------------------------------ |
| Drag                | 阻力         | 当受力移动时物体受到的空气阻力。0表示没有空气阻力，极 大时使物体立即停止运动 |
| Angular Drag        | 角阻力       | 当受扭力旋转时物体受到的空气阻力。0表示没有空气阻力， 极大时使物体立即停止旋转 |
| Use Gravity         | 使用重力     | 该物体是否受重力影响，若激活，则物体受重力影响               |
| Is Kinematic        | 是否是运动学 | 游戏对象是否遵循运动学物理定律，若激活，该物体不再受物理 引擎驱动，而只能通过变换来操作。适用于模拟运动的平台或 者模拟由铰链关节连接的刚体 |
| Interpolate         | 插值         | 物体运动插值模式。当发现刚体运动时抖动，可以尝试下面的 选项：None(无），不应用插值；Interpolate(内插值），基于上一巾贞 变换来平滑本帧变换；Extrapolate(外插值），基于下一帧变换来 平滑本帧变换 |
| Collision Detection | 碰撞检测     | 碰撞检测模式。用于避免高速物体穿过其他物体却未触发碰 撞。碰撞模式包括Discrete (不连续）、Continuous  (连续）、 Continuous Dynamic (动态连续〉3种。其中，Discrete模式用来  检测与场景中其他碰撞器或其他物体的碰撞；Continuous模式 用来检测与动态碰撞器（刚体）的碰撞；Continuous Dynamic模  式用来检测与连续模式和连续动态模式的物体的碰撞，适用于 高速物体 |
| Constraints         | 约束         | 对刚体运动的约束。其中，Freeze Position(冻结位置）表7TC刚体 在世界中沿所选HZ轴的移动将无效，Freeze Rotation(冻结 旋转）表示刚体在世界中沿所选的X、Y、Z轴的旋转将无效 |

## 2. Blend Tree

2D Simple Directional（2D简单方向）：当你的运动代表不同的方向，如“向前走”，“向后走”，“向左走”，“向右走”，或“向上瞄准”，“向下瞄准”，“左瞄“和”右瞄“。当然了，可以在(0,0)处包含一个默认动作类似“空闲站立”或“直线瞄准”。与1D混合树不同的是，2D Simple Directional不是在同一个方向上的多个动作，比如“走”和“跑”。

2D Freeform Directional（2D自由方向）：动画运用有不同的方向时，也可以使用这种混合类型：可以在同一个方向上有多个运动，例如“走”和“跑”。在Freeform Directional类型中，(0，0)位置必须包含一个默认动作，如“空闲站立”。

2D Freeform Cartesian（2D自由笛卡儿）：当混合的2个参数不代表不同的方向时使用。使用Freeform Cartesian，参数X和Y可以表示不同的概念类型，例如角速度和线速度。举个例子：“向前走不转向”，“向前跑不转向”，“向前走并右转”，“向前跑并右转”等动作
Direct : 一种动作的多个表现 比如不同的idle动作权重