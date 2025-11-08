---
icon: question
---

# 常见问题

### Q：Windows 客户端打开报错

<figure><img src="../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

安装应用时选择仅为自己安装，不要选择为所有用户安装。

***

### Q：Windows 客户端启动白屏

<figure><img src="../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

先检查是不是 1717 端口被占用，如果没有被占用，重启电脑再打开试试。

***

### Q：Docker 环境连接本地模型报错

使用 Docker 环境时，如果需要调用本地模型，将 localhost 替换为：[host.docker.internal](http://host.docker.internal:11434) ，如 Ollama 的 API 配置应该为：[http://host.docker.internal:11434](http://host.docker.internal:11434)

***

### Q：升级至 1.3.x 版本后历史数据丢失

同时打开历史数据目录（**Open Data Directory（History）**）、当前数据目录（**Open Data Directory**）

<figure><img src="../.gitbook/assets/image (49).png" alt=""><figcaption></figcaption></figure>

将历史数据目录下的所有文件夹移动至当前数据目录：

<figure><img src="../.gitbook/assets/image (50).png" alt=""><figcaption></figcaption></figure>

重启客户端，将弹出数据迁移弹框，点击开始迁移

<figure><img src="../.gitbook/assets/image (51).png" alt=""><figcaption></figcaption></figure>

迁移成功后，可在新版本使用历史数据。

***

### Q：如何生成英文的数据集？

<figure><img src="../.gitbook/assets/image (46).png" alt=""><figcaption></figcaption></figure>

系统会根据当前用户选择的语言决定最终生成数据集的语言，目前支持中、英两种语言。当前默认语言环境为中文，如果需要生成英文数据集，需要手动切换至英文。

***

### Q：模型配置里未找到想要的模型提供商和模型？

目前支持 **OpenAI 标准协议** 的模型接入，兼容 Ollama，系统只是内置了一些常见的模型配置，如果未找到可以自定义**模型提供商、** **模型名称、API地址、密钥** 。

***

### Q：模型测试没问题，但是生成问题、数据集时报错

系统在很多情况下会要求模型按照规定 JSON 格式输出，如果模型本身的理解能力、上下文长度不足，则输出可能不稳定，建议更换参数量较大、上下文长度较大的模型。

***

### Q：批量任务处理速度太慢

任务的处理速度大部分情况下取决于选择的模型本身的处理速度，如果是本地模型，请检查资源利用率；如果是远程模型，建议更换更快更稳定的平台。

***

### Q：批量任务突然中断，在某个节点开始快速完成

<figure><img src="../.gitbook/assets/image (47).png" alt=""><figcaption></figcaption></figure>

很有可能触发了模型的限流策略、常见于未充值的硅基流动、免费的 OpenRouter 模型，可以手动将任务配置里的并发处理数量调小，目前默认是 5 。

***

### Q：问题、数据集未按照期望风格输出

<figure><img src="../.gitbook/assets/image (48).png" alt=""><figcaption></figcaption></figure>

可以在项目配置 - 提示词配置增加自定义提示词进行主动干预。
