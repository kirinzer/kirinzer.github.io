---
layout: post
title: '用 ChatDev 帮你写一个乒乓球游戏'
date: 2024-02-18
cover: '/assets/img/chat dev arch.jpg'
tags: '2024 ai chat gpt'
---

# 用 ChatDev 帮你写一个乒乓球游戏

### 1. 环境搭建

#### 1.1 配置环境变量
https://github.com/OpenBMB/ChatDev

参考这里  Quickstart with terminal 的部分

需要注意的，它的核心依赖还是需要调用 open ai 的 api，

因此会有如下的环境变量配置这里只列出关键部分；

**Set OpenAI API Key:** Export your OpenAI API key as an environment variable. Replace `"your_OpenAI_API_key"` with your actual API key.

Remember that this environment variable is session-specific, so you need to set it again if you open a new terminal session. On Unix/Linux:

如下所示：

export OPENAI_API_KEY="your_OpenAI_API_key"

通常来说，如果你直接使用 OpenAI API 接口这里直接填写对应的 key 就可以了。

如果使用第三方供应商提供的接口，那需要注意。还需要配置额外的字段。

例如，原生接口 [https://api.openai.com/v1/chat/completions](https://api.openai.com/v1/chat/completions)，更换为第三方

export BASE_URL="https://aaa.bbb.ccc/v1/"

后面的部分在发起请求的时候会被拼接进去。

---
#### 1.2 安装 Anaconda
本地依赖环境有需要 Anaconda 终端安装方式如下  **brew install anaconda**

顺序安装 python 的 module 的时候，其中的一个出现了问题，distutils 这个在安装 numpy 的环节出问题了。stack overflow 上看了一下，要回退一下 python 的版本，太新的不行：）

#### 1.3 回退 python 使用 3.9 版本
具体的回退方法如下
1. 确定已安装的 Python 版本：
    - 打开终端应用程序。
    - 运行以下命令来列出当前系统上已安装的 Python 版本：
      
        ```
        ls /usr/local/bin/python*
        
        ```
    
2. 选择要卸载的 Python 版本：
    - 根据上一步的输出，确定要卸载的 Python 版本。通常，Python 3.x 的可执行文件名称为 `python3` 或 `python3.x`，其中 `x` 是具体的版本号。
3. 执行卸载命令：
    - 在终端中运行以下命令来卸载指定的 Python 版本（将 `<version>` 替换为您要卸载的版本号）：
      
        ```
        sudo rm -rf /Library/Frameworks/Python.framework/Versions/<version>
        
        ```
        
    
    请注意，卸载 Python 可能需要管理员权限，因此可能需要输入管理员密码。
    
4. 清理相关符号链接：
    - 运行以下命令来清理相关的符号链接（将 `<version>` 替换为您要卸载的版本号）：
      
        ```
        brew unlink python@<version>
        
        ```
        
    
    如果之前使用 Homebrew 安装了 Python，则需要清理相关的符号链接。
    
5. 确认卸载：
    - 运行以下命令来确保已成功卸载指定的 Python 版本：
      
        ```
        python3 --version
        
        ```
        
    
    如果看到类似 "Python x.x.x is not installed" 的消息，则表示成功卸载。


### 2. 注意事项
2.1 关于拼接 BASE_URL 这里需要带上版本号v1，命名规则引入了版本控制，后面是操作的动作。
2.2 本地 python 环境，使用 3.9 不要使用最新版本，否则会有 module 无法安装。

### 3. 确认合适的提示词以及调试代码
下面是每次开启一个新的终端窗口都需要反复执行的命令，包含切换工程路径，设置环境变量，执行脚本

```python
Projects/ChatDev/

export OPENAI_API_KEY="<your api key>"

export BASE_URL="<your base url>"

python3 [run.py](http://run.py) —task "design a pingpong game" —name "SecondGame"
```
![本地图片](/assets/img/api timeout.jpg)

如果这里没有问题的情况下会顺利生成可执行的软件。这一步是构建环节，会在当前目录的 WareHouse 下指定文件夹生成软件。在控制台中输出的调试信息不够详细可以，去看一下 log 文件，在 console 没有输出的地方有写到具体的报错问题。

比如上面这个问题，最后排查出来就是设置环境变量 BASE URL 出问题了，一开始是字段 key 用错，程序使用了默认的 open  ai 的官方 api 接口，但是用了第三方 api key；后面的问题是，字段配置对了，但是 value 上，没有配置完整，也就是注意事项 2.1 中，需要配置成 aaa.bbb.ccc/v1/ 这样的形式。

### 4. 生成并调试程序
如果上述的坑都踩过之后，应该可以顺利的运行代码（对了，运行代码前请确保你的 task 不是特别的复杂，以及你的账户里有足够的 money，不至于在执行到一半的时候中断）

这里省去的是目标 task 最开始执行的讨论环节，其实代码执行起来挺快的。各个不同的 agent 会进行对话来完善程序。最后是输出程序以及对应的报告包括花费。

![game result](/assets/img/game result.jpg)


#### 4.1 调试遇到的问题
ping pong game 的环境问题，因为是一个 GUI 游戏，本身还需要安装一些 python 的依赖，这里也会出现卡主的情况，如果有某些 module 没有安装，也会导致报错，但是这个在生成代码的过程中其实 ChatDev 并不会完全的检查到，也就是说它没办法完全保证宿主环境的稳定可靠。需要宿主主动处理潜在问题。

另外就是，代码的逻辑问题，在 ChatDev 中也有 agent 作为测试人员，会自圆其说的通过测试。但是，实际的执行下来。代码还是会有问题。比如，按照第 3 部分代码块中的提示词，生成的代码，初看并不能响应键盘操作。
添加代码调试后发现，是后续移动的操作并没有刷新 UI 导致的。

工程文件如下，出现问题的部分已经修复并添加了注释。

![ping pong](/assets/img/ping pong.jpg)

<https://github.com/kirinzer/ChatDev-WareHouse-Projects/blob/main/ForthGame_DefaultOrganization_20240206175955/game.py>

### 5. 总结
简单总结一下，目前看来，如果做复杂任务可能还是有一定的难度的。但是可以拆解开，这其实也是我们现有的处理复杂问题的标准流程。将复杂问题拆解，大问题化解成多个小问题，甚至在没有上下文强依赖的情况下可以并行执行，缩短整体项目执行时间。

给一个 prompt 的情况下，多个 Agents 自己讨论决策，最终开动写出来的代码，稍微 debug 一下也可以执行，也许在可以预见的未来，programer 都会变成给 agent 下达指令，教他们怎么做事的人。

