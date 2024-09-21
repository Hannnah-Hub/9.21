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
在rigidbody中禁用rotation
```C#
using UnityEngine;

public class movement : MonoBehaviour
{
    public float moveSpeed = 5f; // 控制移动速度
    private Vector3 moveDirection;
    private Rigidbody rb; // 添加Rigidbody变量

    void Start()
    {
        rb = GetComponent<Rigidbody>(); // 获取Rigidbody组件
        rb.freezeRotation = true; // 冻结物体的旋转，确保不受物理影响而旋转
    }

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
吃掉金币
```C#
using UnityEngine;

public class CoinCollector : MonoBehaviour
{
    private int score = 0; // 玩家得分

    // 当玩家碰撞到金币时调用
    void OnTriggerEnter(Collider other)
    {
        // 判断碰撞物体是否是金币
        if (other.gameObject.CompareTag("Coin"))
        {
            // 增加玩家的分数
            score += 1;
            Debug.Log("得分: " + score);

            // 销毁金币
            Destroy(other.gameObject);
        }
    }
}
```
将得分作为ui
```C#
using UnityEngine;

public class CoinCollector : MonoBehaviour
{
    public ScoreManager scoreManager; // 引用ScoreManager

    // 假设已有的OnTriggerEnter方法
    void OnTriggerEnter(Collider other)
    {
        // 判断碰撞物体是否是金币
        if (other.gameObject.CompareTag("Coin"))
        {
            // 增加分数并更新UI
            scoreManager.AddScore(1);  // 调用ScoreManager增加分数的方法

            // 销毁金币
            Destroy(other.gameObject);
        }

        // 如果有其他OnTriggerEnter逻辑，继续保留
        // 例如：处理其他物体的碰撞...
    }
}
```
```C#
using UnityEngine;
using TMPro; // 引入TextMeshPro的命名空间

public class ScoreManager : MonoBehaviour
{
    public TextMeshProUGUI scoreText; // 使用TextMeshProUGUI代替Text
    private int score = 0; // 初始化得分

    // 用于初始化
    void Start()
    {
        // 初始化得分文本
        scoreText.text = "Score: " + score.ToString();
    }

    // 调用此方法增加分数
    public void AddScore(int value)
    {
        score += value; // 增加分数
        scoreText.text = "Score: " + score.ToString(); // 更新UI文本
    }
}
```

