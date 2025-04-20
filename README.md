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
public abstract class User
{
     public static string Username;
     public static string Password;
     public static string Usertoken;

     public static void Load()
     {
        var key = Registry.CurrentUser.OpenSubKey(@"SOFTWARE\\ChmlFrp");
        if (key == null) return;
        Username = key.GetValue("username")?.ToString();
        Password = key.GetValue("password")?.ToString();
        Usertoken = key.GetValue("usertoken")?.ToString();
     }

     public static void Save(string username, string password, string usertoken)
     {
        var key = Registry.CurrentUser.CreateSubKey(@"SOFTWARE\\ChmlFrp", true);
        if (key == null) return;
        key.SetValue("username", username);
        key.SetValue("password", password);
        key.SetValue("usertoken", usertoken);
        Load();
    }
}
```

```python
暂无Python代码
```
