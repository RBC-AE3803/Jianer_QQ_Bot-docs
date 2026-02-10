# NapCatQQ使用教程

NapCatQQ是一个基于LiteLoaderQQNT的QQ机器人框架，本教程将指导你如何安装、配置并与简儿QQ机器人一起使用。

## 第一步：下载NapCatQQ

### Windows/Windows Server用户
前往[NapCatQQ Releases](https://github.com/NapNeko/NapCatQQ/releases)下载最新版Windows一键包：
- 下载链接：[NapCat.Framework.Windows.OneKey.zip](https://github.com/NapNeko/NapCatQQ/releases/download/v4.7.78/NapCat.Framework.Windows.OneKey.zip)
- 下载完成后解压到任意目录

### 桌面Linux用户
在桌面环境的终端中执行以下命令（不要使用SSH连接）：
```bash
curl -o napcat.sh https://nclatest.znin.net/NapNeko/NapCat-Installer/main/script/install.framework.sh && sudo bash napcat.sh
```

### 无桌面Linux用户（Linux Server）
在终端中执行以下命令：
```bash
curl -o napcat.sh https://github.moeyy.xyz/https://raw.githubusercontent.com/NapNeko/napcat-linux-installer/refs/heads/main/install.sh && sudo bash napcat.sh
```

## 第二步：启动NapCatQQ

### Windows/Windows Server用户
1. 双击运行 `NapCatInstaller.exe` 等待自动化配置完成
2. 进入生成的 `NapCat.XXXX.Framework` 目录（XXXX为版本号）
3. 启动 `NapCatWinBootMain.exe`

> **注意**：如果频繁提示QQ出现损坏，请安装插件 [LiteLoaderQQNT-Kill-Update](https://github.com/xh321/LiteLoaderQQNT-Kill-Update)

### 桌面Linux用户
安装脚本可能会自动启动NapCatQQ，如果没有自动启动，请执行：
```bash
sudo ./launcher.sh
```

### 无桌面Linux用户（Linux Server）
在终端中执行：
```bash
sudo ./launcher.sh
```

> **提示**：请根据安装脚本的具体提示进行操作，以上命令仅供参考

## 第三步：配置NapCatQQ

1. 打开NapCatQQ的WebUI界面：
   - 本地部署：http://localhost:6099
   - 服务器部署：将localhost替换为服务器的IP地址

2. 使用默认账号密码登录：
   - 用户名：napcat
   - 密码：napcat

   ![NapCatQQ登录界面](https://github.com/user-attachments/assets/ca6824ef-8d40-4908-b932-639bd68594dd)

3. 配置WebSocket服务器：
   - 在左侧菜单中找到**网络配置**
   - 点击**添加**按钮，选择**Websocket服务器**类型
   - 配置参数（名称可自行更改）：
     - 地址：根据部署环境填写（本地部署填127.0.0.1，服务器部署填服务器IP）
     - 端口：默认使用6099（可根据需要修改）

   ![网络配置界面](https://github.com/user-attachments/assets/7b207237-c159-45cf-81f1-c0c1c4490c57)
   ![添加WebSocket服务器](https://github.com/user-attachments/assets/2c285fb3-a414-4ffd-be8c-c3e9fa62c979)

## 第四步：连接简儿QQ机器人

完成NapCatQQ的配置后，启动你的简儿QQ机器人。如果机器人提示连接成功，恭喜你！你已经成功配置了NapCatQQ与简儿的连接。

## 故障排除

如果遇到问题，可以尝试以下解决方法：

1. 检查NapCatQQ是否正常运行
2. 确认WebSocket服务器配置是否正确
3. 查看NapCatQQ的日志文件获取详细错误信息
4. 参考[NapCatQQ官方文档](https://napneko.github.io/)获取更多帮助

## 常见问题

- **无法访问WebUI**：请检查NapCatQQ是否正在运行，以及防火墙设置是否允许访问
- **QQ出现损坏提示**：安装[LiteLoaderQQNT-Kill-Update](https://github.com/xh321/LiteLoaderQQNT-Kill-Update)插件
- **连接简儿失败**：检查WebSocket服务器地址和端口是否与简儿配置一致