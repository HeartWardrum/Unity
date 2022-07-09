## 1. [Rigidbody](https://docs.unity.cn/cn/2020.3/ScriptReference/Rigidbody.html).MovePosition

~~~~C#
public void MovePosition (Vector3 position);
//参数 position
//为Rigid'body对象提供新位置  新位置：当前位置+移动距离
//例如：
rigidBody.MovePosition(transform.position + transform.forward * Time.fixedDeltaTime * moveSpeed * inputV);
~~~~

