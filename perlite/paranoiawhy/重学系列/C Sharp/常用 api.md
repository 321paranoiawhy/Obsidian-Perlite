# 类型转换

`float` 转 `int`:

```cs
// 1. 显式转换, 忽略小数点后所有值
int intFromFloat = (int)3.6f; // 3

// 2. Math.Ceiling() 向上取整
// Math.Ceiling() 返回值为 double
intFromFloat = (int)Math.Ceiling(3.6f); // 4

// 3. Math.Floor() 向下取整
intFromFloat = (int)Math.Floor(3.6f); // 3

// 4. Math.Round() 四舍五入
intFromFloat = (int)Math.Round(3.6f); // 4
```

# 退出应用程序

`Application.Quit` 在 `Unity` 中退出应用程序, 注意在某些平台上可能并不适用, 但适用于 `Windows exe` 应用:

```cs
Application.Quit();
```

`Application.Exit` 退出 `WinForms` 应用程序

```cs
using System.Windows.Forms;

System.Windows.Forms.Application.Exit();
```

在 `Unity Editor` 中暂停游戏:

```cs
UnityEditor.EditorApplication.isPlaying = false;
```

```cs
Environment.Exit();

// Exit the application with a success code
Environment.Exit(0);

// Exit the application with a non-zero exit code to indicate an error
Environment.Exit(1);
```

# 抛出错误

```cs
throw new ArgumentNullException(nameof(parmater));
```