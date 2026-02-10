# 创建新的插件
为了简儿原生功能的丰富性，提升开发者二次开发的便捷性，简儿于 2025.02 推出了全新的 **NEXT PREVIEW 分支**。此分支的原生功能实际是 2.0 版本的迭代，但是本分支新增了插件兼容性，为广大开发者们提供了更友好的插件开发入口。本文将引导你如何快速、顺利地开发 **简儿（NEXT PREVIEW 分支）** 的插件并投入使用。

> [!IMPORTANT]
> NEXT PREVIEW 分支是**预览分支**，插件兼容性有待评估，投入实际使用可能不会具有预期中的稳定性。请谨慎使用本分支产品，如有遇到Bug，请立即反馈于 Issue ，感谢您的谅解与支持。

## **0. 原理讲解（必看）**
你可以在简儿的根目录一下找到 ```plugins``` 文件夹，这是插件的存放目录。

插件可以以以下形式在 ```plugins``` 文件夹中存在：
- ```.py``` 文件
- ```.pyw``` 文件
- 文件夹

其中 ```.py``` 文件和 ```.pyw``` 文件是以单个文件形式存在的单个插件，可以直接放在 ```plugins``` 文件夹根目录下。文件夹形式存在的插件是由多个文件组合形成的**单个插件**，文件夹中必须包含**入口文件** ```setup.py``` ，文件夹直接放在 ```plugins``` 文件夹根目录下。**文件夹形式存在的插件，其内部的子文件夹不会被识别为插件**。 

```setup.py``` 和其他以单个文件形式存在的单个插件具有与相同的内容规范，将会在后文 _**1. 开始制作**_ 中详细讲解。

无论任何形式的插件，当其文件名以 **d_** 开头时，如 ```d_something.py``` ，将会被忽略加载，即为 **已禁用插件** 。你可以很方便地在群里发送 “<u>启用插件</u>” 或 “<u>禁用插件</u>” 来使简儿加载或忽略加载某些插件。你可以发送 “<u>重载插件</u>” 来使简儿重新从磁盘中加载全部插件，而无需重启简儿。你还可以发送 “<u>插件视角</u>” 来查看插件的运行报告，哪些插件是否已被启用，或因为何种原因加载失败。

## **1. 开始制作**

### 创建单个文件形式存在的插件

在  ```plugins``` 文件夹 下，新建 ```.py``` 文件，文件名会作为插件名称。如 ```Hello World.py```

### 创建文件夹形式存在的插件

在  ```plugins``` 文件夹 下，新建文件夹，文件夹名称会作为插件名称。如 ```Hello World```

在该文件夹下，新建 ```setup.py``` 文件，该文件会作为插件的入口文件，响应插件的一系列事件。如果缺少该文件，则插件将会无法被正常加载。

接下来， ```setup.py``` 文件和单个文件形式存在的插件操作方法**完全相同**，开发者只需要按照接下来的步骤即可完成插件注册和插件编写。

### 注册插件

这是一个示例：一个  ```Hello World.py``` 插件具有以下代码

```python
TRIGGHT_KEYWORD = "你好，世界"
HELP_MESSAGE = "-你好，世界 —> 仅仅就是一句 Hello world 🤔？"
async def on_message(event, actions, Manager, Segments):
        await actions.send(group_id=event.group_id, message=Manager.Message(Segments.Text("Hello, world! 🌍")))
        return True
```

仅需5行代码即可完成开发一个可以发送消息的插件，可见简儿插件开发的高效性。接下来，本文将对代码进行讲解。
* ```TRIGGHT_KEYWORD``` ：```str``` 类型，插件的触发关键词，即当用户在群里发送的消息包含此关键词时，触发此插件。
在示例  ```Hello World.py``` 插件中，当用户发送 “<u>你好，世界</u>” 时，此插件将会被触发。（如图所示）

![image](https://github.com/user-attachments/assets/900f890a-b33b-4f65-ac1a-e5bfbe67aec1)

* ```HELP_MESSAGE``` ：```str``` 类型，插件的帮助消息。当用户在群里@简儿 或者发送 “<u>帮助</u>” 时，展示的帮助文件中会包括此帮助消息文本。（如图所示）

![QQ_1739525797968](https://github.com/user-attachments/assets/5dea55e5-dd57-4da1-ab1a-cb47c909318f)

* ```async def on_message()``` ：插件的入口函数，当插件被触发时，执行 ```on_message()``` 函数内部的代码。**注意，此方法必须异步**。

* ```return True``` ：阻断执行后续功能，此行可选。当插件返回 ```True``` 时，简儿将停止执行后续的功能，<u>防止多个具有相同触发关键词的功能一起被执行</u>。

恭喜你，已经成功地**新建并注册好了一个插件**，现在这个插件可以被正常地加载和调用啦！下一步，本文将深入讲解如何实现更多丰富功能。

### 参数传入

 ```async def on_message()``` 函数可以接受很多参数，各种各样的参数说明详见 [*Variables.md*](https://github.com/SRInternet-Studio/Jianer_QQ_bot/blob/NEXT-PREVIEW/Variables.md) 

直接将想要被传入的参数填写在函数的括号内即可，例如 ```async def on_message(event, actions, Manager, Segments)```

### 实现功能
```'actions'```：行动，用于操作机器人执行一系列操作。

```'event'```：当前已被触发的消息事件类型及事件内容。

举例：发送消息
```python
await actions.send(group_id=event.group_id, message=Manager.Message(Segments.Text("Hello, world! 🌍")))
```

* ```actions.send()``` ：发送一条内容

* ```event.group_id``` ：获取发送消息的用户所在的群号码

* ```Manager.Message``` ：一个消息内容

* ```Segments.Text``` ：一段纯文本消息

```'actions'``` 和 ```'event'``` 还可以实现许许多多的功能，它继承于 **OneBot v11** 框架，你可以在[这里](https://github.com/botuniverse/onebot-11/blob/master/api/public.md)找到 ```'actions'``` 的更多有趣用法，可以在[这里](https://github.com/botuniverse/onebot-11/blob/master/event/README.md)找到 ```'event'``` 的更多详细信息。

恭喜你，你已经实现了自己的第一个插件！快去试试吧～

## 2. 制作进阶
### 读取配置文件

正常情况下，你能够在简儿的根目录下找到一个配置文件 ```config.json``` ，这样的配置文件你可能通过设置向导 ```SetupWizard.pyw``` 去完成的，包含了机器人的名称、触发关键词等信息。

如果要在插件中加载配置文件，我们需要用到来自 **HypeR 框架** 中的一个功能：

```python
from Hyper import Configurator
Configurator.cm = Configurator.ConfigManager(Configurator.Config(file="config.json").load_from_file())
```

接下来，我们仅需要通过1行代码获取配置文件中的值：

```python
bot_name = Configurator.cm.get_cfg().others["bot_name"] #获取你给机器人配置的名称
```

你可以在任意位置插入配置文件中的值。

 ```config.json``` 使用标准的JSON字典格式，你可以直接查看配置文件以了解更多详细信息。

### 永久触发插件

**永久触发插件** 是指这个插件将会接收这个QQ账号的所有事件，比如群聊事件（GroupMessageEvent）、私聊事件（PrivateMessageEvent）、加群事件（GroupMemberIncreaseEvent）、退群事件（GroupMemberDecreaseEvent）等等，只要QQ账号的状态发生改变，插件就会被立刻触发。

要查看所有事件类型，详见 [*Variables.md 模块的第3点*](https://github.com/SRInternet-Studio/Jianer_QQ_bot/blob/NEXT-PREVIEW/Variables.md#%E6%A8%A1%E5%9D%97)

如果你想要做一个 **永久触发插件** ，仅需将改动一个值:

```python
TRIGGHT_KEYWORD = "Any"
```

可以看到，将 **TRIGGHT_KEYWORD** 设置为了 ```Any``` ，无论发生什么事件插件都会被立刻执行。**这就要求插件自己去判断事件的类型以及用户的输入，并作出判定**。

这是一个示例：一个  ```Hello World.py``` ，**但是他通过私聊消息被触发**。插件具有以下代码

```python
from Hyper import Configurator
Configurator.cm = Configurator.ConfigManager(Configurator.Config(file="config.json").load_from_file()) #加载配置文件

TRIGGHT_KEYWORD = "Any"
EXPECTED_VALUE = f"{Configurator.cm.get_cfg().others["reminder"]}你好，世界" # reminder 是机器人的触发关键词
HELP_MESSAGE = f"{EXPECTED_VALUE} —> 仅仅就是一句 Hello world 🤔？"
async def on_message(event, actions, Events, Manager, Segments):
    if isinstance(event, Events.PrivateMessageEvent): #假设 PrivateMessageEvent 私聊事件 是你想要被触发的事件
        if str(event.message) = EXPECTED_VALUE: #如果用户发送的是 触发关键词 + “你好，世界”
           await actions.send(group_id=event.group_id, message=Manager.Message(Segments.Text("Hello, world! 🌍")))
           return True #此行可选
```

**请注意， ```return True``` 将会阻断执行其他所有功能**。