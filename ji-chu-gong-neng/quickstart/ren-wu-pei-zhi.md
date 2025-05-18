---
icon: diagram-next
---

# 任务配置

{% hint style="info" %}
任务配置模块用于对文本处理、问题生成、任务并发等相关参数进行设置，以满足不同的任务需求。合理配置各项参数，能够有效提升任务执行效率和质量。
{% endhint %}

### 文本分割设置

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

#### 1. 分割策略（Split Strategy）

文本分割基于设置的长度范围进行操作，将输入文本按照规则分割成合适的段落，以便后续处理。

#### 2. 最小长度（Minimum Length）

* 功能：设定分割后每个文本片段的最小字符长度，当前默认值为 1500。若某段文本长度小于该值，会与相邻文本段合并，直至满足最小长度要求。
* 设置方法：在 “Minimum Length” 后的输入框中输入期望的数值（需为正整数）。

{% hint style="warning" %}
数值不宜过大，否则可能导致文本片段数量过少，影响后续处理的灵活性；也不宜过小，避免文本片段过于零碎。
{% endhint %}

#### 3. 最大分割长度（Maximum Split Length）

* 功能：限制分割后每个文本片段的最大字符长度，当前默认值为 2000。超过该长度的文本会被分割成多个片段。
* 设置方法：在 “Maximum Split Length” 后的输入框中输入合适的数值（需为正整数且大于最小长度值）。

### 问题生成设置

<figure><img src="../../.gitbook/assets/image (3) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

#### 1. 问题生成长度（Question Generation Length）

* 功能：设定生成问题的最大字符长度，当前默认值为 240。确保生成的问题在合理长度范围内，便于阅读和理解。
* 设置方法：在 “Question Generation Length” 后的输入框中输入期望的数值（需为正整数）。

#### 2. 移除问号概率（Removing Question Marks Probability）

* 功能：设置生成问题时移除问号的概率，当前默认值为 60%。可根据具体需求调整问题格式。
* 设置方法：在 “Removing Question Marks Probability” 后的输入框中输入 0 - 100 之间的整数（代表百分比概率）。

#### 3. 并发限制（Concurrency Limit）

* 功能：用于限制同时生成问题和生成数据集的任务数量，避免因任务过多占用过多系统资源，导致系统性能下降或任务失败。
* 设置方法：根据系统资源情况和任务需求，设置合适的并发任务数量上限。具体操作可能需在相关设置界面找到对应的输入框或滑块进行调整（若存在）。

{% hint style="warning" %}
设置时需考虑服务器的硬件性能、网络带宽等因素，若并发任务过多，可能导致任务排队等待时间过长，甚至出现任务超时失败的情况。另外，此处可能会受浏览器的最大并发数量限制影响，可以手动扩大本地浏览器的最大并发数量，参考：[https://github.com/ConardLi/easy-dataset/issues/306](https://github.com/ConardLi/easy-dataset/issues/306)
{% endhint %}

### PDF 转换配置

<figure><img src="../../.gitbook/assets/image (4) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

#### 1. **MinerU Token 配置**

* 功能：MinerU Token 用于基于 MinerU AIP 转换 PDF 的身份验证和授权。
* 设置方法：在对应的输入框中输入有效的 MinerU Token。需注意，MinerU Token 有效期仅为 14 天，过期后需及时更换新的 Token 以保证功能正常使用。

#### 2. 自定义大规模视觉模型并发限制

* 功能：限制自定义大规模视觉模型相关任务的并发数量，合理分配系统资源，保障模型处理任务的稳定性和效率。
* 设置方法：根据模型的计算复杂度和系统资源情况，谨慎设置并发限制，过高可能导致系统负载过大，过低则可能无法充分利用系统资源。

### 数据集上传设置

<figure><img src="../../.gitbook/assets/image (5) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

#### 1. Hugging Face Token

* 功能：Hugging Face Token 用于在与 Hugging Face 平台交互时进行身份验证，实现数据集上传等功能（目前 Hugging Face 功能尚未实现，此 Token 设置暂时仅为预留）。
* 设置方法：在 “hf\_” 后的输入框中输入 Hugging Face 平台生成的 Token。
