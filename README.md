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
import winreg


class User:
    # 打开或创建注册表键
    key_path = r"SOFTWARE\ChmlFrp"
    key = winreg.CreateKey(winreg.HKEY_CURRENT_USER, key_path)

    username = None
    password = None
    usertoken = None

    @staticmethod
    def load():
        try:
            with winreg.OpenKey(winreg.HKEY_CURRENT_USER, User.key_path) as key:
                User.username = winreg.QueryValueEx(key, "username")[0]
                User.password = winreg.QueryValueEx(key, "password")[0]
                User.usertoken = winreg.QueryValueEx(key, "usertoken")[0]
        except FileNotFoundError:
            User.username = None
            User.password = None
            User.usertoken = None

    @staticmethod
    def save(username, password, usertoken):
        with winreg.OpenKey(winreg.HKEY_CURRENT_USER, User.key_path, 0, winreg.KEY_WRITE) as key:
            winreg.SetValueEx(key, "username", 0, winreg.REG_SZ, username)
            winreg.SetValueEx(key, "password", 0, winreg.REG_SZ, password)
            winreg.SetValueEx(key, "usertoken", 0, winreg.REG_SZ, usertoken)
        User.load()
```
