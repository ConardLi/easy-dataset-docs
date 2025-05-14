---
icon: question
---

# 常见问题

### Q：如何生成英文的数据集？

<img src="https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=ODUzZmFmYThhODVkZjM4NjUyNWYzZWMyYzM1NzlmNDFfRkRoQmROWFA2STFIZUI5dWlJaklSbmhGOHJRNUROZXVfVG9rZW46VEJzbGJvcWEwb1lNa2h4MDQzQWMwWlcybktiXzE3NDcyMjMyMDY6MTc0NzIyNjgwNl9WNA" alt="" data-size="original">

系统会根据当前用户选择的语言决定最终生成数据集的语言，目前支持中、英两种语言。当前默认语言环境为中文，如果需要生成英文数据集，需要手动切换至英文。

***

### Q：模型配置里未找到想要的模型提供商和模型？

![](https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=N2U0NTNjZGZhYjY4YTBhZmM1ZjVjMzZmYzIwODc1YmZfTEl0ZXYyZk5aeUlMc1E0NjlxZjMzQjEwRTFGVThzNnZfVG9rZW46WGMwZ2J1ZHZSb0NjQlZ4TUhIcGMySFdZbndkXzE3NDcyMjMyMDY6MTc0NzIyNjgwNl9WNA)

目前支持 **OpenAI 标准协议** 的模型接入，兼容 Ollama，系统只是内置了一些常见的模型配置，如果未找到可以自定义**模型提供商、** **模型名称、API地址、密钥** 。

***

### Q：模型测试没问题，但是生成问题、数据集时报错

系统在很多情况下会要求模型按照规定 JSON 格式输出，如果模型本身的理解能力、上下文长度不足，则输出可能不稳定，建议更换参数量较大、上下文长度较大的模型。

***

### Q：批量任务处理速度太慢

任务的处理速度大部分情况下取决于选择的模型本身的处理速度，如果是本地模型，请检查资源利用率；如果是远程模型，建议更换更快更稳定的平台。

***

### Q：批量任务突然中断，在某个节点开始快速完成

![](https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=Nzg1NzA2YzE2NGNmYzZiZjRkNjIxZjE0Y2ZkYzhiY2Vfa3N5QzBqTnR6bXJsZ0VnSkhaTTcxakl2S1oxT1JnSm5fVG9rZW46WWpibmI4eVBhbzc3WnR4MU41T2NJSEVGbmxnXzE3NDcyMjMyMDY6MTc0NzIyNjgwNl9WNA)

很有可能触发了模型的限流策略、常见于未充值的硅基流动、免费的 OpenRouter 模型，可以手动将任务配置里的并发处理数量调小，目前默认是 5 。

***

### Q：问题、数据集未按照期望风格输出

![](https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=MjllODY4ZTQwNDRjN2M5NzdjODNkOTc1N2YyNDc0NmJfbTlyUDhvaHM4eEZWSTZHa0tnWHA1Zm1hbUcxRWNGZmpfVG9rZW46QlBIVmJEZ01Zb2hVNGp4YVZBRGNTUE1QbkJlXzE3NDcyMjMyMDY6MTc0NzIyNjgwNl9WNA)

可以在项目配置 - 提示词配置增加自定义提示词进行主动干预。
