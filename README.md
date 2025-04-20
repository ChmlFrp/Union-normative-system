# 联合规范制度

## 1.用户数据存储位置
我们要求启动器对用户数据需统一存储至注册表

数据项位置：
```
计算机\HKEY_CURRENT_USER\Software\ChmlFrp
```


| 数据项名称  | 数据项类型 | 描述 |
| ------------- | ------------- | ------------- |
| password  | 字符串值  | 用户密码  |
| username  | 字符串值  | 用户名  |
| usertoken  | 字符串值  | 用户token  |

## 2.示例代码
```csharp
using Microsoft.Win32;

public abstract class User
{
    private static readonly RegistryKey Key = Registry.CurrentUser.CreateSubKey(@"SOFTWARE\\ChmlFrp", true);
    public static string Username;
    public static string Password;
    public static string Usertoken;

    public static void Load()
    {
        Username = Key.GetValue("username")?.ToString();
        Password = Key.GetValue("password")?.ToString();
        Usertoken = Key.GetValue("usertoken")?.ToString();
    }

    public static void Save(string username, string password, string usertoken)
    {
        Key.SetValue("username", username);
        Key.SetValue("password", password);
        Key.SetValue("usertoken", usertoken);
        Load();
    }
}
```

```python
暂无Python代码
```
