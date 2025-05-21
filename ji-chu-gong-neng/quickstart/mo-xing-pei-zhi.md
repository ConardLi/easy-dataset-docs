---
icon: gear-complex-code
---

# 模型配置

{% hint style="info" %}
&#x20;此模块用于配置后续文献处理、构造数据集等功能需要调用的大模块，包括文本模型和视觉模型。
{% endhint %}

<figure><img src="../../.gitbook/assets/image (6) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

目前平台已默认内置了部分模型提供商，仅需要填入模型提供商对应的密钥即可：

<table><thead><tr><th width="139.87890625">ProviderId</th><th width="136.83203125">Name</th><th>API URL</th></tr></thead><tbody><tr><td>ollama</td><td>Ollama</td><td>http://127.0.0.1:11434/api</td></tr><tr><td>openai</td><td>OpenAI</td><td>https://api.openai.com/v1/</td></tr><tr><td>siliconcloud</td><td>硅基流动</td><td>https://api.ap.siliconflow.com/v1/</td></tr><tr><td>deepseek</td><td>DeepSeek</td><td>https://api.deepseek.com/v1/</td></tr><tr><td>302ai</td><td>302.AI</td><td>https://api.302.ai/v1/</td></tr><tr><td>zhipu</td><td>智谱AI</td><td>https://open.bigmodel.cn/api/paas/v4/</td></tr><tr><td>Doubao</td><td>火山引擎</td><td>https://ark.cn-beijing.volces.com/api/v3/</td></tr><tr><td>groq</td><td>Groq</td><td>https://api.groq.com/openai</td></tr><tr><td>grok</td><td>Grok</td><td>https://api.x.ai</td></tr><tr><td>openRouter</td><td>OpenRouter</td><td>https://openrouter.ai/api/v1/</td></tr><tr><td>alibailian</td><td>阿里云百炼</td><td>https://dashscope.aliyuncs.com/compatible-mode/v1</td></tr></tbody></table>

{% hint style="success" %}
注意：不在以上列表的模型提供商也是支持配置的，模型提供商、API 接口地址、API Key、模型名称这些信息都是支持自定义输入的，只要是符合 OPEN AI 格式的 API，平台均可兼容。
{% endhint %}

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

点击**刷新模型列表**，可查看该提供商提供的所有模型（这里也可以手动输入模型名称）：

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

支持配置语言模型（用于完成文本生成任务）和视觉模型（用于完成视觉分析任务）：

<figure><img src="../../.gitbook/assets/image (7) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

另外也支持配置模型的温度和最大输出 Token：

<figure><img src="../../.gitbook/assets/image (5) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* **Temperature**：控制生成文本的随机性，温度越高，结果越随机多样，反之越稳定保守。
* **Max Token**：限制模型生成文本的长度，以 Token 为单位，防止输出过长。

***

支持 Ollama ，可自动拉取本地已经部署的模型列表：

<figure><img src="../../.gitbook/assets/image (12) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

支持配置多个模型，可通过右上角模型下拉框切换模型：

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
