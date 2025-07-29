# 联盟规范制度

## 1.加入ChmlFrp第三方启动器联盟
1.需要拥有一个github账号和CHMLFRP账号

2.所写启动器必须按照联盟规范制度

3.账号不在 https://all.chmlfrp.com/blacklist 当中

4.要求代码开源

## 2.用户数据存储位置
我们要求启动器对用户数据需统一存储至注册表

数据项位置：
```
计算机\HKEY_CURRENT_USER\Software\ChmlFrp
```

文件树：
```
├───ChmlFrp
│   ├───password
│   ├───username
│   └───usertoken        
│       
```

| 数据项名称  | 数据项类型 | 描述 |
| ------------- | ------------- | ------------- |
| password  | 字符串值  | 用户密码  |
| username  | 字符串值  | 用户名  |
| usertoken  | 字符串值  | 用户token  |

