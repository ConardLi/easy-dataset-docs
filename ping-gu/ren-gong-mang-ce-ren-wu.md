---
icon: user-group-simple
---

# 人工盲测任务

虽然自动化评估很方便，但在模型上线的最后阶段，或者两个模型分数咬得很死的时候，还是需要人来看一眼。**盲测任务是什么？**

* 盲测任务 = 把多个模型的回答“匿名化”，让评审者只看回答质量做选择/打分
* 适合：
  * 你希望排除“模型名偏见”
  * 你更在意主观体验（可读性、风格、说服力、完整性等）
  * 开放题/对话型内容的最终质量评估

***

就像在之前的章节中我们讲到到 `LMArena`，人工盲测对于垂直领域的模型评估同等重要，在实际测试中，系统会隐藏两个模型的回答结果，评判者仅根据回答的质量、逻辑、语气进行主观判断，彻底消除对特定品牌的固有偏见。我们来到【评估-人工盲测任务】模块，然后点击创建任务，然后配置：

<figure><img src="https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=NzZmZmE2YzY5NWZkZTkxZDhjNTQxYTU5MDcwMWI4MThfTUk0N0VVcVVmUHhWZ0JsZkNPcDBBbm9QemR5em5mM0lfVG9rZW46V2xka2JaS1d4b1dUbGF4cUcxc2NWaUJTblliXzE3NjgyMzE0NTM6MTc2ODIzNTA1M19WNA" alt=""><figcaption></figcaption></figure>

* **两两对比**：从模型库中选择两个你最想对比的模型。
* **题目范围**：选择简答题或开放题并设置抽样数量。

任务开启后，您将进入一个类似 **Chatbot Arena** 的沉浸式的对比界面：

<figure><img src="https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=MmRiNDg5Y2JlYTAxZDkyMzA3MzYzMTBlMjM4NTljZTNfTkNpejZFN2NPRk9tNjRxTTEwRGhGN2I5eno5eURNVFFfVG9rZW46VmtpWGJ6OFpVb0llbUZ4U1ZDYmNFY1drbndoXzE3NjgyMzE0NTM6MTc2ODIzNTA1M19WNA" alt=""><figcaption></figcaption></figure>

* **左右对照**：左边展示候选 A 的回答，右边展示候选 B 的回答，但不告诉标注人员具体是哪个模型。
* **流式加载**：系统支持流式输出，您可以实时看到模型的生成过程。
* **四选一投票**：标注人员只需要根据直观感受，选择“左边好”、“右边好”或者“平局”。
  * **👈 左边更好**：左侧回答在准确性、流畅度或安全性上更优。
  * **👉 右边更好**：右侧回答更符合你的预期。
  * **🤝 平局**：两者难分伯仲，或都存在明显的严重错误。

<figure><img src="https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=OWVjZTQxYjJjM2RmMmJjYjkyOTY3OWJjYmM1OGY3NTdfSGhKZFpmZmdkWTNtajJBZHFybTBMY2FvWGRZaFVTTE5fVG9rZW46SjNySGI3VnBvbzhkb2x4UzkxT2NKakNHblFmXzE3NjgyMzE0NTM6MTc2ODIzNTA1M19WNA" alt=""><figcaption></figcaption></figure>

这种 Side-by-Side 的比较数据，是目前公认最符合人类真实体感的评估方式。当所有题目投票完成后，系统会 “揭晓谜底” 并生成胜率统计，系统将展示每个模型在对比中获胜的百分比。如果平局较多，说明这两个模型在当前题库下的表现非常接近。你还可以回顾具体某个题目的回答结果：

<figure><img src="https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=YmNkNzFmNWY0ZWY5MzM1YmQ3OTAzMTFiN2RkODg1MWZfRWREVmlPZHo5OW4zTm1EZENrQ09Yam9QNXY2UlZsdHFfVG9rZW46TDEySGJBWmVYbzkyaFF4RHZEdGNGMFpobjhmXzE3NjgyMzE0NTM6MTc2ODIzNTA1M19WNA" alt=""><figcaption></figcaption></figure>

回到任务列表，我们能清晰的看到每次盲测任务的结果：

<figure><img src="https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=MmQyMWY2ZTQ2NmU3MjRkMGZjZTIwZWNmYjAyNzNkYzhfVzJlRHFBS3ZUcmxKb1diZXNzRndkSFhWU2RnODdsTFBfVG9rZW46VDVRbWJEVGhOb0x3OVZ4ZXgyV2NBQm10bjllXzE3NjgyMzE0NTM6MTc2ODIzNTA1M19WNA" alt=""><figcaption></figcaption></figure>

***
