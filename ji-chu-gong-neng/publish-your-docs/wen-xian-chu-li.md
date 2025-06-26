---
icon: book
---

# 文献处理

{% hint style="info" %}
此模块用于将多种格式的领域文献，处理为可供模型理解的数据结构。
{% endhint %}

### 文件类型

目前平台支持 **Markdwon、PDF、DOCX、TXT** 四种格式的文献处理：

<figure><img src="../../.gitbook/assets/image (18) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
模型对于具备良好结构划分的 Markdown 文献理解效果最好，建议大家优先上传 Markdwon 文件。
{% endhint %}

### PDF 处理

由于 PDF 格式相对特殊，平台针对不同场景支持了四种不同的 PDF 处理方式，当上传的文献中含有 PDF 格式的文献时，会触发弹框：

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

#### 基础解析

专注于快速识别简单 PDF 文件的关键轮廓，处理规整纯文本报告、简单说明文档等效率高，但无法精准解析含大量公式、图表等复杂内容的文件。

#### MinerU API 解析

可通过 「设置 - 任务设置」 配置 MinerU API Key，调用 MinerU API 进行解析，可深度解析含公式、图表的复杂 PDF 文件，适用于学术论文、技术报告等场景，文件越复杂处理速度越慢。可以通过 [https://mineru.net/apiManage/token](https://mineru.net/apiManage/token) 申请 MinerU API Key（注意有效期为 14 天，过期需重新申配置）。

<figure><img src="../../.gitbook/assets/image (14) (1) (1).png" alt=""><figcaption></figcaption></figure>

#### MinerU 在线平台解析

跳转至 MinerU 平台：[https://mineru.net/OpenSourceTools/Extractor](https://mineru.net/OpenSourceTools/Extractor) ，用户可在此平台解析 PDF，并下载 Markdwon 文件，再回平台重新上传。

<figure><img src="../../.gitbook/assets/image (4) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

#### 自定义视觉模型解析

可以识别复杂的 PDF 文件，包括公式和图表。该方式要求在模型配置中添加视觉模型配置，通过自定义的视觉模型来实现对 PDF 文件的解析。可以根据具体需求定制解析规则和模型参数，以适应不同类型的复杂 PDF 文件。

<figure><img src="../../.gitbook/assets/image (3) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

当选择 MinerU API 解析、自定义视觉模型解析时，PDF 处理时间可能较长，请耐心等待：

<figure><img src="../../.gitbook/assets/image (8) (1) (1) (1) (1).png" alt=""><figcaption><p><br></p></figcaption></figure>

可通过 「设置-任务设置」 配置自定义视觉模型的最大并发数量，及最多同时处理多少页 PDF，并发数量越大，处理速度也快，注意考虑模型提供商的并发量限制。

<figure><img src="../../.gitbook/assets/image (15) (1) (1).png" alt=""><figcaption></figcaption></figure>

### 文本分块

在选择好文件和处理方式，点击上传前，注意一定要提前在右上角选择模型，否则会导致处理失败：

<figure><img src="../../.gitbook/assets/image (7) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
注意，这一步大家没必要选推理模型（比如 DeepSeek-R1），选择一个普通的问答模型比如豆包、千问都可以，在这一步推理模型并不会起到优势，而且会拖慢处理速度。
{% endhint %}

点击上传后，会将传入的文献进行了智能的文本分割，我们可以在分割列表里看到被拆分好的文本块，以及每个文本块的字数：

<figure><img src="../../.gitbook/assets/image (9) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

可以查看每个文本块的详情：

<figure><img src="../../.gitbook/assets/image (10) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

可以对每个文本块进行编辑：

<figure><img src="../../.gitbook/assets/image (11) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

关于文本分块的原理，以及想自定义分块规则以适应不同的文献结构，可查看：《[自定义分块](../../basics/editor.md)》 章节。

### 文献管理

可以筛选指定文献已经生成的文本块：

<figure><img src="../../.gitbook/assets/image (3) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

&#x20;可预览文献详情（转换为 Markdown），下载文献（Markdown），删除文献：

<figure><img src="../../.gitbook/assets/image (6) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

预览文献：

<figure><img src="../../.gitbook/assets/image (7) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
