# 案例1：生成汽车图片识别数据集

`VQA` 数据集（Visual Question Answering Dataset）是用于多模态模型训练 / 微调的核心数据集合，核心包含 “图像 + 对应自然语言问题 + 标准答案” 三部分，目的是让模型学会结合图像视觉信息与语言理解能力，准确回答关于图像内容的问题。

例如下面就是一个最简单的 `VQA` 数据集案例：

<figure><img src="https://files.mdnice.com/user/6267/bc8e5329-dd17-48c7-b792-9ca9427319c1.png" alt=""><figcaption></figcaption></figure>

> 目标场景：已有一批各种汽车的图片，希望创建一组针对汽车特征进行识别的数据集，用于训练车辆识别模型。

首先进入【数据源 - 图片管理】模块，点击右上角导入图片，这里我们将需要生成数据集的图片目录输入进去（本机的绝对路径）：

<figure><img src="https://files.mdnice.com/user/6267/7d845102-91e8-475c-b606-d9f9a00cf18b.png" alt=""><figcaption></figcaption></figure>

导入完成后，图片会加载到当前项目目录下，然后我们将看到所有图片：

<figure><img src="https://files.mdnice.com/user/6267/efd97462-97fd-4bcc-bdb6-6dcb3c79e6e5.jpg" alt=""><figcaption></figcaption></figure>

我们可以点击单个图片的生成问题，让 AI 智能根据图片识别问题：

<figure><img src="https://files.mdnice.com/user/6267/9437267f-4f5c-4a34-a2a9-3e2bcc9c1a9b.jpg" alt=""><figcaption></figcaption></figure>

也可以点击右上角的自动提取问题，这将创建一个后台批量任务，自动为没有生成问题的图片来生成问题：

<figure><img src="https://files.mdnice.com/user/6267/a60284dc-1702-411d-91eb-edd9f98dce60.jpg" alt=""><figcaption></figcaption></figure>

进入问题管理模块可以看到所有已经生成的问题，和普通问题的区别是数据源属性，普通问题关联的是文本块，而图片问题关联的是一张具体的图片：

<figure><img src="https://files.mdnice.com/user/6267/ab77dd76-b17d-4565-9dc6-908d7d8988de.png" alt=""><figcaption></figcaption></figure>

回到图片管理模块，我们可以直接针对某张图片进行提问，让 AI 直接生成答案：

<figure><img src="https://files.mdnice.com/user/6267/33dbc7c3-363a-4d5f-b09f-a1619d25407e.jpg" alt=""><figcaption></figcaption></figure>

也可以点开智能标注模块，手动标注或让 AI 辅助生成已经创建好的问题对应答案：

<figure><img src="https://files.mdnice.com/user/6267/8da71b5b-1338-4d3f-bc5a-a28779b670c5.png" alt=""><figcaption></figcaption></figure>

在标注模块我们可以快捷创建问题和问题模版，目前支持三种不同的问题模版：

* AI 生成的答案是普通文本

<figure><img src="https://files.mdnice.com/user/6267/7320946f-0d91-4cc2-9181-205ef47609a8.png" alt=""><figcaption></figcaption></figure>

> 例如：描述这辆车的样子；我们可以通过问题模版的提示词来控制最终答案的预期效果，例如答案必须限定在 20 字内

* AI 生成的答案限定在一些标签下

<figure><img src="https://files.mdnice.com/user/6267/14fb141d-bca9-41f8-aec4-b0bab4e840c3.png" alt=""><figcaption></figcaption></figure>

> 例如：识别汽车是几座车时，一定要限定在固定的几个座位里，避免 AI 冗余输出

* AI 生成的答案固定为某种结构：

<figure><img src="https://files.mdnice.com/user/6267/ada40564-2048-4a3f-b945-8f31106e12e2.png" alt=""><figcaption></figcaption></figure>

> 例如：提取汽车的更多特征，可能有多个固定的特征需要提取，我们可以自定义模型输出的 JSON 结构，一定要限定在 color、brand 两个字段上，这样每次识别的答案只会包含汽车品牌和颜色数据。

> 注意：创建问题模版后，会为当前所有图像均创建一个对应问题。

模版创建完成后，我们可以继续在标注界面手动标注这些问题，也可以让 AI 智能生成答案，根据问题模版的不同类型，将会有不同的标注形态：

<figure><img src="https://files.mdnice.com/user/6267/b539ca24-6465-4072-b6c0-cd4c63e4a626.png" alt=""><figcaption></figcaption></figure>

标注完成一个后，我们可以点击保存并继续，AI 将自动查找下一个还未完成标注的图片或问题：

<figure><img src="https://files.mdnice.com/user/6267/815037ea-f7c0-4a98-a705-eee997b66ef6.png" alt=""><figcaption></figcaption></figure>

如果嫌手动标注太慢，可以到问题管理模块，点击自动提取数据集 - 生成图像问答数据集，这会自动创建一个后台异步任务：

<figure><img src="https://files.mdnice.com/user/6267/66942275-9aaa-4f29-9806-67e27b611838.png" alt=""><figcaption></figcaption></figure>

随后，来到图片数据集管理模块，我们可以看到已经生成好的数据集：

<figure><img src="https://files.mdnice.com/user/6267/71328000-9ca5-4925-8209-21367fcc9158.jpg" alt=""><figcaption></figcaption></figure>

点击数据集详情，可以对答案进行更改，自定义评分、自定义标签、备注等标注操作：

<figure><img src="https://files.mdnice.com/user/6267/bab0d6fc-d78c-40d1-ae3f-0b1b4c4cc30b.jpg" alt=""><figcaption></figcaption></figure>

图像数据集导出依然支持多种格式（可选择是否同时导出图片，以及是否在数据集中携带图片路径）：

<figure><img src="https://files.mdnice.com/user/6267/0d367e46-5afe-4e19-8343-653d32c1f29c.jpg" alt=""><figcaption></figcaption></figure>

导出的数据集案例：

<figure><img src="https://files.mdnice.com/user/6267/df97a9a9-68ed-4240-b9f1-763e67795059.png" alt=""><figcaption></figcaption></figure>

### <br>
