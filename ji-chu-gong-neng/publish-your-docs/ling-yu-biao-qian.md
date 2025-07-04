---
icon: hashtag
---

# 领域标签

{% hint style="info" %}
文本分块完成后，平台会调用大模型自动基于文献数据建立领域标签树。
{% endhint %}

<figure><img src="../../.gitbook/assets/image (13) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### 查看原始目录

切换至领域树 Tab，我们可以看到基于 AI 智能分析出的文献的领域树，以及从文献提取的原始目录：

<figure><img src="../../.gitbook/assets/image (14) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

在后续生成问题以及数据集的任务中，平台会基于这个领域树去构建，并且把生成的问题和数据集映射到每个领域标签上。领域树可以让每条数据集具备全局理解的能力，并且减少生成重复数据集的可能性。

<figure><img src="../../.gitbook/assets/image (15) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### 编辑领域树

如果你觉得 AI 生成的领域树，有哪些不准确或者不完善的地方，也可以直接手动添加或者更改和删除标签，建议把领域树的划分确认的更准确后，再去生成问题。

<figure><img src="../../.gitbook/assets/image (16) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### 修订标签树

当删除、新增一个新的文献时，会提供三种模式：

* 修改领域树：根据新增或删除的文档修改当前领域树，仅影响发生变更的部分
* 重建领域树：基于所有文档内容生成全新的领域树
* 保持不变：保持当前领域树结构不变，不进行任何修改保持当前领域树不变

<figure><img src="../../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>





