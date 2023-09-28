# 基本操作

- 鼠标滚轮滚动以缩放
- 按住鼠标滚轮并拖动, 可拖动视角
- 按住鼠标右键并拖动, 可进行旋转
- 鼠标左键可选中对象
- `Ctrl + C` 可复制对象, `Ctrl + V` 可粘贴对象, `Ctrl + D` 可复制并粘贴对象
- `Del` 或 `Delete` 可删除对象
- `Ctrl + Z` 可回退操作
- 在 `Hierarchy` 一栏里鼠标单击可选中相应对象, 按住 `Ctrl` 可多选对象, 先选中一个对象后按住 `Shift` 再次选中对象可快速选中列表中两对象之间的所有对象
- `QWERTY` 分别对应 `Tools` 里的查看(`View Tool`)、移动(`Move Tool`)、旋转(`Rotate Tool`)、缩放(`Scale Tool`)、矩形(`Rect Tool`)、综合(`Transform Tool`), 其中 `WER` 三个快捷键最为常用

# 打印语句

```cs
Debug.Log("Debug.Log");
Debug.LogWarning("Debug.LogWarning");
Debug.LogError("Debug.LogError");

Debug.DrawLine(Vector3.zero,Vector3.one, Color.blue);
Debug.DrawRay(Vector3.zero,Vector3.one, Color.red);
```

# 坐标系

`Unity` 采用**左手坐标系**, `X` 轴为红色, `Y` 轴为蓝色, `Z` 轴为绿色。

## 世界坐标系(`UCS`, `Universal Coordinate System`)

世界原点 `(0,0,0)`

## 本地坐标系

`Unity` 每个对象的位置坐标都是相对于父对象的局部位置。如果对象无父对象, 则其位置坐标即世界坐标系中的坐标, 否则即为本地坐标系坐标。

# `C#` 脚本的生命周期

调用顺序依次为:

1. `Awake`
2. `OnEnable`
3. `Start`
4. `FixedUpdate`
5. `Update`
6. `LateUpdate`
7. `OnDisable`
8. `OnDestroy`

先执行完所有 `C#` 脚本的 `Awake` 方法, 然后往下执行完所有 `C#` 脚本的 `OnEnable` 方法, 依此类推。

在脚本中可通过 `` 获取游戏物体引用:

```cs
// this 可省略
GameObject go = this.gameObject;
// GameObject go = gameObject;

// 游戏物体名称
Debug.Log(go.name);

// 游戏物体标签
Debug.Log(go.tag); // Untagged 等值

// 游戏物体图层, 默认图层 0:Default
Debug.Log(go.layer); // 0

// 当前真实的激活状态
Debug.Log(go.activeInHierarchy);
// 当前自身激活状态
Debug.Log(go.activeSelf);

// 设置激活状态
go.SetActive(false); // go.setActive(true);

// 获取 Transform Component, this 可省略
Debug.Log(this.transform); // Debug.Log(transform);

// 获取除 Transform 以外的其他组件
// 使用 GetComponent, 并声明组件泛型
// T t = GetComponent<T>();
BoxCollider boxCollider = go.GetComponent<BoxCollider>();

// 获取当前物体的子物体上的组件
GetComponentInChildren<CapsuleCollider>(boxCollider);

// 获取当前物体的父物体的组件
GetComponentInParent<BoxCollider>();

// 添加组件
gameObject.AddComponent<AudioSource>();

// 通过游戏物体名称获取游戏物体
// NullReferenceException: Object reference not set to an instance of an object
GameObject test = GameObject.Find("Test");

// 通过游戏标签获取游戏物体
GameObject testTag = GameObject.FindWithTag("TestTag");

// 手动销毁组件
Destory(go);
```

## `Awake`

`Awake` 最早调用, 只会被调用一次, 可在此做初始化操作 (更多情况下是在 `Start` 中初始化) 或实现单例模式。

```cs
private void Awake()
{

}
```

## `OnEnable`

组件(每次)激活后调用, 在 `Awake` 之后调用, 可能会被调用多次, 因此不要在此做初始化操作。

```cs
private void OnEnable()
{

}
```

## `Start`

可在 `Start` 做初始化操作, 只会被调用一次。

```cs
// Start is called before the first frame update
void Start()
{

}
```

## `FixedUpdate`

固定频率调用该方法, 默认值 `0.02s`, 调用间隔相同。

> [!tip]
> 修改固定间隔: `Edit` -> `Project Settings` -> `Time` -> `Fixed Timestep`

```cs
private void FixedUpdate()
{

}
```

## `Update`

每帧调用一次, 但调用间隔不同。

```cs
// Update is called once per frame
void Update()
{

}
```

## `LateUpdate`

紧随 `Update` 之后调用。

```cs
private void LateUpdate()
{

}
```

## `OnDisable`

组件未激活时调用。

```cs
private void OnDisable()
{

}
```

## `OnDestroy`

组件销毁时调用。

```cs
private void OnDestroy()
{

}
```

# 预设体 `Precab`

`*.precab` 文件

```cs
public GameObject Prefab;

// 通过预设体实例化一个游戏物体
// Instantiate 有十个重载方法
// 实例化后会返回当前 GameObject
Instantiate(Prefab);
```

# 变体 `Precab Variant`

# Vector3

以下三种写法等价:

```cs
Vector3 v1 = new Vector3(0, 0, 0);

// IDE0090
// https://learn.microsoft.com/en-us/dotnet/fundamentals/code-analysis/style-rules/ide0090
Vector3 v2 = new(0, 0, 0);

// 简写
Vector3 v3 =  Vector3.zero;
```

```cs
// 坐标
Vector3 v1 = new(1, 2, 3);

// 旋转
Vector3 v2 = new(45, 90, 45);

// 缩放
Vector3 v1 = new(0.1f, 0.2f, 0.3f);
```

一些简写:

```cs
Vector3 v1 = Vector3.zero; // Vector3(0, 0, 0)
Vector3 v2 = Vector3.one; // Vector3(1, 1, 1)

Vector3 v3 = Vector3.forward; // Vector3(0, 0, 1)
Vector3 v4 = Vector3.back; // Vector3(0, 0, -1)

Vector3 v5 = Vector3.up; // Vector3(0, 1, 0)
Vector3 v6 = Vector3.down; // Vector3(0, -1, 0)

Vector3 v7 = Vector3.left; // Vector3(-1, 0, 0)
Vector3 v8 = Vector3.right; // Vector3(1, 0, 0)
```

修改属性值:

```cs
Vector3 v1 = Vector3.zero; // Vector3(0, 0, 0)

v1.x = 1;
v1.y = 1;
v1.z = 1;
```

计算:

```cs
Vector3 v1 = Vector3.forward; // Vector3(0, 0, 1)
Vector3 v2 = Vector3.back; // Vector3(0, 0, -1)

// 计算两个向量的夹角
Debug.Log(Vector3.Angle(v1, v2)); // 180

// 计算距离
Debug.Log(Vector3.Distance(v1, v2)); // 2

// 向量长度
Debug.Log(v1.magnitude); // 1

// 归一化
Debug.Log(new Vector3(3, 4, 0).normalized); // (0.60, 0.80, 0.00)

// 计算点乘
Debug.Log(Vector3.Dot(v1, v2)); // -1

// 计算叉乘
Debug.Log(Vector3.Cross(v1, v2)); // (0.00, 0.00, 0.00)

// 插值
Debug.Log(Vector3.Lerp(Vector3.zero, Vector3.one, 0.2f)); // (0.20, 0.20, 0.20)
```

## 欧拉角与四元数

```cs
Vector3 rotate = new(0, 30, 0);

Quaternion quaternion1 = Quaternion.identity;

// 由欧拉角得到相应的四元数
Quaternion quaternion2 = Quaternion.Euler(rotate);
// 由四元数得到相应的欧拉角
Vector3 rotate2 = quaternion1.eulerAngles;

// 看向 rotate
Quaternion quaternion3 = Quaternion.LookRotation(rotate);
```

## Time

```cs
Debug.Log(Time.time);

// 时间缩放值, 默认值 1.0, 可用于游戏加速、减速和暂停等
Debug.Log(Time.timeScale);

// 固定时间间隔, 默认值 0.02
Debug.Log(Time.fixedDeltaTime);

// 上一帧到下一帧所用的游戏时间, 可在 Update 生命周期内调用, 当做计时器
Debug.Log(Time.deltaTime);
```

```cs
private float timer;

    void Update()
    {
        timer += Time.deltaTime;
    }
```

## Application

```cs
// 游戏数据文件夹路径 (只读, 不可写, 打包后会被加密压缩)
// Example: D:/work/learn-unity/3d/Assets
Debug.Log(Application.dataPath);

// 持久化文件夹路径, 可用于文件的读写, 支持跨平台和持久化
// Example: C:/Users/Administrator/AppData/LocalLow/DefaultCompany/3d
Debug.Log(Application.persistentDataPath);

// StreamingAssets 文件夹路径 (只读, 打包后不会被加密压缩, 类似 public 文件夹)
// 可用于存放配置文件、二进制文件等
// Example: D:/work/learn-unity/3d/Assets/StreamingAssets
Debug.Log(Application.streamingAssetsPath);

// 临时文件夹路径
// Example: C:/Users/Administrator/AppData/Local/Temp/DefaultCompany/3d
Debug.Log(Application.temporaryCachePath);

// 是否在后台运行, 默认值 True
// File -> Build Settings -> Player Settings -> Resolution and Presentation -> Resolution -> Run In Background
Debug.Log(Application.runInBackground);

// 打开网页
Application.OpenURL("https://www.baidu.com/");

// 退出游戏

```

# SceneManager

```cs
// 同步方式场景跳转
// 可传入场景索引, 场景名称
SceneManager.LoadScene(1);
SceneManager.LoadScene("SceneName");
// 替换当前场景并跳转, 只存在新场景
SceneManager.LoadScene(1, LoadSceneMode.Single);
// 加载新场景到当前场景, 二者并存
SceneManager.LoadScene(1, LoadSceneMode.Additive);

// 异步方式场景跳转
SceneManager.LoadSceneAsync(1);

// 获取当前场景
Scene currentScene = SceneManager.GetActiveScene();
// 获取场景名称
Debug.Log(currentScene.name);
// 场景是否已加载
Debug.Log(currentScene.isLoaded);
// 场景路径
Debug.Log(currentScene.path);
// 场景索引
Debug.Log(currentScene.buildIndex);

// 当前加载的场景数量
Debug.Log(SceneManager.sceneCount);

// 创建新场景, 返回新场景
Scene newScene = SceneManager.CreateScene("NewScene");

// 卸载场景
// UnloadScene 已弃用
SceneManager.UnloadScene(newScene);
// 应使用 UnloadSceneAsync
SceneManager.UnloadSceneAsync(newScene);
```

# 协程

```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.SceneManagement;

public class SceneTest : MonoBehaviour
{
    AsyncOperation asyncOperation;
    // Start is called before the first frame update
    void Start()
    {
        StartCoroutine(LoadScene());
    }

    IEnumerator LoadScene()
    {
        asyncOperation = SceneManager.LoadSceneAsync(1);
        // 加载完场景后不自动跳转, 默认值为 true
        asyncOperation.allowSceneActivation = false;
        yield return asyncOperation;
    }

    // Update is called once per frame
    void Update()
    {
        // 输出场景加载进度, 0 - 0.9
        Debug.Log(asyncOperation.progress);
    }
}
```

# Transform

```cs
// 世界坐标系位置坐标
Debug.Log(transform.position);
// 相对于父物体的位置坐标
Debug.Log(transform.localPosition);

// 旋转 (四元数)
Debug.Log(transform.rotation);
Debug.Log(transform.localRotation);
// 旋转 (欧拉角)
Debug.Log(transform.eulerAngles);
Debug.Log(transform.localEulerAngles);

// 缩放 (只有 localScale 获取相对于父物体的缩放)
Debug.Log(transform.localScale);

// 获取当前物体的前方
Debug.Log(transform.forward);
// 获取当前物体的右侧
Debug.Log(transform.right);
// 获取当前物体的上方
Debug.Log(transform.up);

// 时刻看向原点
transform.LookAt(Vector3.zero);

// 自转
transform.Rotate(Vector3.up, 1);
// 类似公转, 绕着转
transform.RotateAround(Vector3.zero, Vector3.up, 5);

// 移动
transform.Translate(Vector3.forward * 0.1f);

// 获取子物体数量
Debug.Log(transform.childCount);

// 获取父物体
Debug.Log(transform.parent.gameObject);

// 解除所有父子关系
transform.DetachChildren();

// 获取子物体
Transform child1 = transform.Find("Child");
Transform child2 = transform.GetChild(0);

// 判断一个物体是否是另一个物体的子物体, 即判断物体间的父子关系
Debug.Log(child1.IsChildOf(transform)); // True

// 设置父物体
child1.SetParent(transform);
```

# 键盘和鼠标操作

> [!tip]
> 须在游戏画面内操作键盘和鼠标才会响应, 其它地方无效。

`Update` 生命周期中监听**鼠标**操作:

```cs
    void Update()
    {
        // 0 鼠标左键, 1 鼠标右键, 2 鼠标滚轮
        if (Input.GetMouseButtonDown(0))
        {
            Debug.Log("按下鼠标左键");
        }
        
        if (Input.GetMouseButton(0))
        {
            Debug.Log("长按鼠标左键");
        }
        
        if (Input.GetMouseButtonUp(0))
        {
            Debug.Log("松开鼠标左键");
        }
    }
```

`Update` 生命周期中监听**键盘**操作:

```cs
        if (Input.GetKeyDown(KeyCode.A))
        {
            Debug.Log("按下键盘 A");
        }
        
        if (Input.GetKey(KeyCode.A))
        {
            Debug.Log("长按键盘 A");
        }
        
        if (Input.GetKeyUp(KeyCode.A))
        {
            Debug.Log("松开键盘 A");
        }
```

> [!tip]
> `KeyCode.A` 等价于小写字母 `"a"`, 但是不能是大写字母 `"A"`。

# 虚拟按钮和虚拟轴

`Edit` -> `Project Settings` -> `Input Manager` -> `Axes`, 有内置的 `Horizontal`、`Vertical`、`Fire1`、`Jump` 等虚拟按钮和虚拟轴。

## 虚拟按钮

`Jump` 虚拟按钮对应键盘上的 `Space` 按键。

```cs
    void Update()
    {
        if (Input.GetButtonDown("Jump"))
        {
            Debug.Log("按下跳跃键 (Space)");
        }

        if (Input.GetButton("Jump"))
        {
            Debug.Log("长按跳跃键 (Space)");
        }

        if (Input.GetButtonUp("Jump"))
        {
            Debug.Log("松开跳跃键 (Space)");
        }
    }
```

## 虚拟轴

`A` 和 `D` 控制 `Horizontal`, `W` 和 `S` 控制 `Vertical`, 范围均为 `-1 ~ 1`。

```cs
    void Update()
    {
        float horizontal = Input.GetAxis("Horizontal");
        float vertical = Input.GetAxis("Vertical");
        Debug.Log(horizontal + " " + vertical);
    }
```

# 触摸操作

```cs
    void Start()
    {
        Input.multiTouchEnabled = true;
    }

    void Update()
    {
        // 单点触摸
        if (Input.touchCount == 1)
        {
            Debug.Log("单点触摸");
            // 触摸对象
            Touch touch = Input.touches[0];
            // 触摸位置
            Debug.Log(touch.position);

            // 触摸阶段
            switch (touch.phase)
            {
                case TouchPhase.Began:
                    break;
                case TouchPhase.Moved:
                    break;
                case TouchPhase.Stationary:
                    break;
                case TouchPhase.Ended:
                    break;
                case TouchPhase.Canceled:
                    break;
            }
        }

        // 两点触摸
        if (Input.touchCount == 2)
        {
            Debug.Log("两点触摸");
            Touch touch1 = Input.touches[0];
            Touch touch2 = Input.touches[1];
        }

        // 三点以上触摸
        if (Input.touchCount > 2)
        {

        }
    }
```

# Audio 和 Video

`Audio`:

```cs
using UnityEngine;

public class AudioTest : MonoBehaviour
{
    // AudioClip
    public AudioClip music;

    public AudioClip soundEffects;

    public AudioSource player;
    void Start()
    {
        player = GetComponent<AudioSource>();
        // 设定播放的音频片段
        player.clip = music;
        // 循环播放
        player.loop = true;
        // 调节音量
        player.volume = 0.5f;
        // 播放
        player.Play();
    }



    void Update()
    {
        if (Input.GetKeyDown(KeyCode.Space))
        {
            // (只读属性) 是否正在播放
            if (player.isPlaying)
            {
                // 暂停播放
                //player.Pause();

                // 从 0 开始暂停
                player.Stop();
            }
            else
            {
                // 继续播放
                //player.UnPause();

                // 从 0 开始播放
                player.Play();
            }
        }
        
        // 单击鼠标左键播放音效
        if (Input.GetMouseButtonDown(0))
        {
            player.PlayOneShot(soundEffects);

        }
    }
}
```

`Video` 须引入命名空间 `using UnityEngine.Video`。

# 碰撞

碰撞发生条件:

1. 二者均含有碰撞组件 `Colider`, 如 `Box Colider`
2. 二者至少有一个含有刚体组件 `Rigid`, 如 `RigidBody`

```cs
using UnityEngine;

public class ColiderTest : MonoBehaviour
{
    // 爆炸预设体
    public GameObject Prefab;
    
    void Start()
    {

    }

    void Update()
    {

    }

    // 发生碰撞
    private void OnCollisionEnter(Collision collision)
    {
        // 创建爆炸物体
        Instantiate(Prefab, transform.position, Quaternion.identity);
        // 销毁自身
        Destroy(gameObject);
        // 碰撞到的游戏物体名称
        Debug.Log(collision.gameObject.name);
    }
    
    // 持续发生碰撞
    private void OnCollisionStay(Collision collision)
    {

    }

    // 结束碰撞
    private void OnCollisionExit(Collision collision)
    {

    }
}
```

# 触发

```cs
using UnityEngine;

public class CubeControl : MonoBehaviour
{
    void Start()
    {

    }

    void Update()
    {

    }

    // 触发
    private void OnTriggerEnter(Collider other)
    {
        GameObject wall = GameObject.Find("Wall1");
        Debug.Log(wall);
        if (wall != null)
        {
            wall.SetActive(false);
        }
    }

    private void OnTriggerStay(Collider other)
    {

    }

    private void OnTriggerExit(Collider other)
    {
        
    }
}

```

# 碰撞检测

```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class CubeControl : MonoBehaviour
{
    void Start()
    {

    }

    void Update()
    {
        if (Input.GetMouseButtonDown(0))
        {
            //Ray ray1 = new Ray(Vector3.zero, Vector3.up);
            Ray ray2 = Camera.main.ScreenPointToRay(Input.mousePosition);
            // 声明一个碰撞信息类
            RaycastHit hit;
            // 碰撞检测
            bool res = Physics.Raycast(ray2, out hit);
            if (res == true)
            {
                Debug.Log(hit.point);
                transform.position = hit.point;
            }
            // 多碰撞检测
            RaycastHit[] hits = Physics.RaycastAll(ray2);
        }
    }
}
```

# Hinge Joint


- `Add COmponent` 搜索 `Joint`, 选择 `Hinge Joint` 即可创建**铰链** (轴承)
- 设置 `Anchor` 和 `Axis` 属性, 以改变其轴的位置和旋转方向
- 勾选 `Use Motor` 并设置 `Target Velocity` 和 `Force` 即可实现自动旋转, 如门的自动旋转

# Spring Joint

- `Add Component` 搜索 `Joint`, 选择 `Spring Joint` 即可创建**弹簧**
- 选择 `Connected Body`, 或拖动游戏物体至该处

# Fixed Joint

- `Add Component` 搜索 `Joint`, 选择 `Fixed Joint` 即可创建**固定连接**
- 选择 `Connected Body`, 或拖动游戏物体至该处
- 可设置 `Break Force` 断开力和 `Break Torque` 断开力矩

# Line Renderer

```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class LineTest : MonoBehaviour
{
    void Start()
    {
        // 获取线段渲染器
        LineRenderer lineRenderer = GetComponent<LineRenderer>();
        lineRenderer.positionCount = 3;
        lineRenderer.SetPosition(0, Vector3.zero);
        lineRenderer.SetPosition(0, Vector3.one);
        lineRenderer.SetPosition(0, Vector3.down);
    }

    void Update()
    {

    }
}

```

# Trail Renderer

# Animation

# Animator

# 注意事项

- `C#` 脚本文件中 `class` 类名须与脚本文件名一致
- 游戏物体无材质时会显示紫色