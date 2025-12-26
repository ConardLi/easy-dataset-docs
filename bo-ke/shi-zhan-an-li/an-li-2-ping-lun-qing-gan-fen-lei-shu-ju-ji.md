# 案例2：评论情感分类数据集

在刚刚的场景中，我们已经使用过问题模版了，这一个非常灵活的功能，它也可以用在文本数据集上，我们来具一个构造文本分类数据集的例子。

> 目标场景：现有一份微博评论数据，希望基于大模型分析评论是正面还是负面的，用于训练情感分类模型。

数据示例：使用固定的 `--------` 分隔符进行分割：

<figure><img src="https://files.mdnice.com/user/6267/d6795b67-ef41-44af-a957-5cd0cc15541a.png" alt=""><figcaption></figcaption></figure>

<figure><img src="https://files.mdnice.com/user/6267/d6795b67-ef41-44af-a957-5cd0cc15541a.png" alt=""><figcaption></figcaption></figure>

在 EDS 中，我们首先要在任务设置中将分块策略改为 “自定义符号分块” （在自定义分隔符处输入：`---------`），这种策略会严格按照给定的分割符进行分块，并且会忽略分隔符，不受文本块的大小限制：

<figure><img src="https://files.mdnice.com/user/6267/6dc316de-6af9-4a9b-98b7-3788d8445518.png" alt=""><figcaption></figcaption></figure>

然后我们来到文献处理模块，导入这份配置：

<figure><img src="https://files.mdnice.com/user/6267/f667369a-f0d5-403f-b97c-48f8fd02cc9d.png" alt=""><figcaption></figcaption></figure>

然后我们将得到按照评论内容分割的文本块：

<figure><img src="https://files.mdnice.com/user/6267/26420f67-d75f-4199-b80a-d3fc6ad4d3de.png" alt=""><figcaption></figcaption></figure>

这时，我们来到问题管理，创建一个问题模版：

* 在问题中输入：“对评论进行情感分析”
* 提示词填写：“对评论进行情感分析，并将评论分为三类：正面、负面、中性”
* 定义三个标签：正面、负面、中性

<figure><img src="https://files.mdnice.com/user/6267/d6e9da70-0a31-41d6-9aec-b9b7f5ac18cf.png" alt=""><figcaption></figcaption></figure>

然后我们看到 EDS 为每个文本块都创建了这个问题，我们点击自动提取数据集 - 单轮对话数据集：

<figure><img src="https://files.mdnice.com/user/6267/942b47ec-2162-4799-aea1-3d7f4f74ee4f.png" alt=""><figcaption></figcaption></figure>

然后我们在数据集详情可以看到对文本块（评论）的分析结果，答案只分布在了正面、负面、中性这三个标签内：

<figure><img src="https://files.mdnice.com/user/6267/9c219cf1-fa66-4507-8fee-e17a06f6c1b5.png" alt=""><figcaption></figcaption></figure>

在导出数据集时，我们选择自定义格式，并勾选包含文本块：

<figure><img src="https://files.mdnice.com/user/6267/a674ac87-7645-42ad-a113-022bcb3a8ed2.png" alt=""><figcaption></figcaption></figure>

然后我们就得到了一份评论情感分类数据集：

<figure><img src="https://files.mdnice.com/user/6267/8383e439-795a-448f-a02f-7f7d3f450fb1.png" alt=""><figcaption></figcaption></figure>

### <br>
