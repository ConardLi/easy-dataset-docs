---
icon: table
---

# 数据集管理

{% hint style="info" %}
对已生成的数据集进行确认、过滤、修订、优化，保障最终导出符合需求的高质量数据集。
{% endhint %}

### 数据集列表

查看所有已经生成的数据集，包括原始问题、创建时间、使用的模型、领域标签、是否含有思维链（COT）、答案摘要：

<figure><img src="../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

### 数据集详情

点击单条数据集，可查看数据集详情，包含问题、答案、思维链、使用模型、领域标签、创建时间、文本块：

<figure><img src="../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

点击文本块名称，可查看原始文本块详情，方便对比原始内容和答案的差距：

<figure><img src="../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

### 数据集修订

若对于生成的答案、思维链不满意，可点击编辑按钮手动修改：

<figure><img src="../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>

点击魔法棒图标，可向 AI 提供优化建议，基于 AI 进行优化：

<figure><img src="../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

### 数据集确认

确认数据集无问题，可点击确认保留：

<figure><img src="../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

已确认的数据集将会被打上标签：

<figure><img src="../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
注意：确认数据集不是必备操作，仅用于平台记录已确认的情况，不影响后续导出（**未确认的数据集也能导出**）。
{% endhint %}

### 数据集标注

为了满足更灵活的数据集标注需求，在数据集详情中，你可以对数据集添加自定义标签、备注以及评分：

![](https://files.mdnice.com/user/6267/d5aaeb76-c9e6-403b-9ac5-ecad9c129e45.jpg)

并且在筛选中可以根据这些条件进行筛选：

![](https://files.mdnice.com/user/6267/495cc75a-c5fe-47a9-96f0-899d70645ef4.png)

### 数据集评估

你可以使用 AI 对已有数据集进行质量评估，可对单条数据集发起评估，以及后台批量评估：

![](https://files.mdnice.com/user/6267/4e4d58b5-fc89-4798-a94c-ffb9c1d43fda.png)

AI 质量评估完成后，将自动对数据集进行打分，以及添加 AI 评估备注：

![](https://files.mdnice.com/user/6267/b2872875-2f4b-4e9b-b945-1e0cadaa1a0c.jpg)

同样的，你可以到 **项目配置 - 提示词配置 - 质量评估** 自由更改自动质量评估的提示词，以满足定制化的评估需求：

![](https://files.mdnice.com/user/6267/65bb9f66-4ab4-4a1d-84c0-311bf2f64be6.png)

