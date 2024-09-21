# 9.21 unity潜能课
## WASD键控制Player前后左右移动
```C#
using UnityEngine;

public class movement : MonoBehaviour
{
    public float moveSpeed = 5f; // 控制移动速度
    private Vector3 moveDirection;

    void Update()
    {
        // 获取水平（左右）和垂直（前后）方向的输入
        float moveX = Input.GetAxis("Horizontal"); // 左右移动 (A/D 或 左/右方向键)
        float moveZ = Input.GetAxis("Vertical");   // 前后移动 (W/S 或 上/下方向键)

        // 计算移动方向（X轴控制左右，Z轴控制前后）
        moveDirection = new Vector3(moveX, 0f, moveZ);

        // 移动Player
        transform.position += moveDirection * moveSpeed * Time.deltaTime;
    }
}
```
