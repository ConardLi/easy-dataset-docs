---
icon: flask-round-potion
---

# 自动评估任务

题出好了，接下来就是让业务模型来做题，系统来判卷。系统支持两种阅卷模式：

**模式一：直接计算得分（针对客观题）**

对于**判断题、单选题、多选题**，答案是唯一的。系统不需要调用大模型，直接用规则代码比对。我们来到【评估-自动评估任务】模块，点击创建任务，您可以同时勾选多个模型，系统会并发执行多个任务：就像要真实要对模型进行一场考试一样，我们可以配置本次 “考卷” 的具体题目范围：

<figure><img src="https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=NDgyYzc5NThkOGIwOGU3ZGUwYTkzMTMxYmM4ZTZiYjFfd2l1VTltcHRqWnh5ZXZ4djJNUXN5ZEY0dW93eTBVRExfVG9rZW46SjBwVGJCYUwxb3lmS1J4Y2dxQ2NuT0dCbmxpXzE3NjgyMzEzNDA6MTc2ODIzNDk0MF9WNA" alt=""><figcaption></figcaption></figure>

* **题型筛选**：比如本次之考察选择题和判断题。
* **标签筛选**：比如只考查标签为 `医疗知识` 的题目。
* **动态采样**：如果您想快速获得结果，可以从 1000 道题中随机抽样 50 道。

<figure><img src="https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=YzcyMzlmN2Q0ODU0YTViZDlhNTI2MDE3ZWQyMTI0MGRfM1NjR3hwOG13cnNnTW1GNVlaZnRRWVBZZWtGQlFwdGxfVG9rZW46VEZxcWJLZ1Q5b2M0blZ4Ull3cWN2bkVybkNiXzE3NjgyMzEzNDA6MTc2ODIzNDk0MF9WNA" alt=""><figcaption></figcaption></figure>

<figure><img src="https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=NjFkMThiYTY3YTZhYTcyMzlhN2RmZDRiZDI5OGViZmNfZVViWHpIb0dYRXBoeFlwU0lmTzVxQm1LaVJYOFVFelhfVG9rZW46Q3lKOWJrMThqb1FNbDF4VjRuSGNpZEh0bnpkXzE3NjgyMzEzNDA6MTc2ODIzNDk0MF9WNA" alt=""><figcaption></figcaption></figure>

***

进入评估任务详情，你可以看到模型在不同题目上的具体得分情况，我们可以根据题目回答结果（正确/错误）以及题目类型（判断、单选、多选）进行筛选：

<figure><img src="https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=NWM0MjJlNjI5YTRmMGU4OTAxMmZlZmQ1N2U2NGI5YWJfV2lxM2ZLR0h0TUVJcGd2bVJPOEZmelRrSnpKYWE1ZzdfVG9rZW46TUpDS2JpZHdOb0tmQmZ4T0VlT2M0STM1bkpiXzE3NjgyMzEzNDA6MTc2ODIzNDk0MF9WNA" alt=""><figcaption></figcaption></figure>

***

**模式二：教师模型评估（针对主观题）**

对于客观题（选择、判断），系统可以自动对齐答案。但对于 **简答题** 和 **开放题**，答案往往是多样化的。我们可以选择一个更智慧的 “教师模型”（就像判断老师一样） 对测试模型的回答进行深度评测，给出量化的分数和定性的评语。

<figure><img src="https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=YTkxOTI1NjI5ODdhZjBiMmUwZGYyM2FlNjhiMDFhOThfeUo4VDFPaU80ckVWMjYwT3NXaTVFS3Zmc0w0cmtrM0xfVG9rZW46U0NQNWJaSjhCb0s3Tmd4eDQ0eWNHNHVQbjFnXzE3NjgyMzEzNDA6MTc2ODIzNDk0MF9WNA" alt=""><figcaption></figcaption></figure>

系统内置了一份评分标准，不过通用的标准比较宽泛，不一定适用于所有场景，如果你想得到更准确的评估结果，建议根据实际业务场景和数据集的特点定制具体的评分规则：

<figure><img src="https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=ZDVhOWE5NDY5NjIxMGFmZmYxNTA1Yjg0MTMyNDQwZTFfdng2eTMzNjdQQzlYWkVDMkJFbVo2RXNqM0Y1amdFU2ZfVG9rZW46V3Nud2JRcThEb0ZNTVV4VGNYNmNaMDl0bnVmXzE3NjgyMzEzNDA6MTc2ODIzNDk0MF9WNA" alt=""><figcaption></figcaption></figure>

在评估报告详情中，你可以看到每个题目的具体得分，教师模型的打分以及具体的打分理由：

<figure><img src="https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=OGRiYTViYTdhMGQwODc3ZjJkM2ZkMjczMjQwNDFjYzJfakxjeGlaWmIza1NlR0ppZlJxMVJOZHNKcnNDMmhlQ0lfVG9rZW46QmI3MmJiMkRwb1ZhWUp4M1FwNGNyd1lubjdnXzE3NjgyMzEzNDA6MTc2ODIzNDk0MF9WNA" alt=""><figcaption></figcaption></figure>

建议：

* 同一套评估长期对比时，尽量固定教师模型与评分配置，否则分数不可直接横向对比
* 先在小样本（如 20 题）跑通，确认裁判标准符合预期，再扩大规模
