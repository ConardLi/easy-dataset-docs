---
icon: comments-question-check
---

# 问题生成

{% hint style="info" %}
从分割好的文本块中提取问题，并为问题建立领域标签。
{% endhint %}

### 单个文本块生成问题

<figure><img src="../.gitbook/assets/image (17) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

任务完成后，可在文本块中查看已经生成好的问题。

<figure><img src="../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

可对已生成问题的文本块、未生成问题的文本块进行筛选：

<figure><img src="../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption></figcaption></figure>

### 批量生成问题

可批量、全选文本块，并批量构造问题：

<figure><img src="../.gitbook/assets/image (8) (1) (1).png" alt=""><figcaption></figcaption></figure>

可以实时查看批量任务的进度：

<figure><img src="../.gitbook/assets/image (9) (1) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
当批量任务进行中，关闭、刷新当前页面都会中断任务，可以开一个新页面到问题管理查看已经生成的问题。
{% endhint %}

### 问题生成配置

每个文本块生成多少问题，是由 「项目设置 - 任务设置」 里的生成问题的最大长度决定的，默认设置是每 240 个字符生成一个问题，大家 2000 字符左右的文本块生成了 8 个问题，大家可以根据自己文献的信息密度来灵活调整：

<figure><img src="../.gitbook/assets/image (11) (1) (1).png" alt=""><figcaption></figcaption></figure>

还可以控制生成的问题中消除 ？的比例（默认将消除 60%）。

<figure><img src="../.gitbook/assets/image (12) (1) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
在实际问答任务中，用户的问题并不总是会携带 ？消除一定比低的 ？ 有助于提升微调效果
{% endhint %}

可以控制批量任务中的最大并发数量，（默认最大并发 5 个任务）。

<figure><img src="../.gitbook/assets/image (13) (1) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="danger" %}
注意，部分模型提供商会对最大并发数量进行限制，调整过大的值可能导致批量任务失败，建议灵活测试调整。
{% endhint %}
