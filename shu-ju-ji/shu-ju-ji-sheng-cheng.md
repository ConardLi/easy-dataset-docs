---
icon: wand-magic-sparkles
---

# 数据集生成

### 生成单个数据集

点击单个问题上的魔法棒🪄图标，为单个问题生成答案（构造数据集）：

<figure><img src="../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

问题生成答案后，将在右侧展示已经生成答案的数量（单个问题可以生成多个答案）：

<figure><img src="../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Easy DataSet 会根据问题 + 问题对应的文本块 + 领域标签来一起生成答案，来保障答案和文献本身的相关性。
{% endhint %}

当右上角选择的是推理模型时，将保留模型推理过程中的思维链（COT）：

<figure><img src="../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

可以筛选已生成答案、未生成答案的问题：

<figure><img src="../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

### 批量生成数据集

可以多选、全选问题，批量生产答案：

<figure><img src="../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

可以查看批量任务的进度：

<figure><img src="../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
当批量任务进行中，关闭、刷新当前页面都会中断任务，可以开一个新页面到数据集管理查看已经生成的答案。
{% endhint %}

### 数据集生成配置

在任务设置 - 问题生成设置中的并发任务数量，依然可以控制批量生成数据集的最大并发数量：

<figure><img src="../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
最大并发数量越大，数据集生成任务越快，反之越慢，注意模型提供商最大并发限制。
{% endhint %}





