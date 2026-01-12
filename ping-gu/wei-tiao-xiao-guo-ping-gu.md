---
icon: ballot-check
---

# 评估数据集生成

**评估数据集是什么？**

* 评估数据集（测试集）是一组“题目 + 标准答案/参考答案 + 评分规则/选项”的集合。你可以用它来：做不同模型的对比评估，长期追踪效果变化。

***

**测试集题目类型**

一个好的模型评估数据集（测试集）是衡量模型真实能力的基石。在 `Easy Dataset` 中，评估集不仅仅是问题的集合，更是包含标准答案、考点标签和业务逻辑的综合知识库。为了全面考察模型能力，我们设计了五种题型：

* **判断题：**&#x8FD9;是最直接的。考察模型对核心事实是否搞混。比如文档里说“温度不能超过 100 度”，题目问“温度是否可以达到 105 度？”，能有效检测幻觉。
* **单选题：**&#x34;个选项（A-D），单选答案 | 考察模型在干扰项下的知识提取和辨析能力。
* **多选题：**&#x591A;个选项，答案为字母数组（如 `["A", "C"]`） | 极具挑战性，漏掉一个信息点就选不对。
* **简答题（短答案）：**&#x63D0;供标准短答案（20字以内），可测试模型获取核心知识点并精简表达的能力。如：2025 年美团的营收是多少亿？
* **开放题（长答案）：**&#x8003;察推理和总结能力。比如“根据文档描述，分析一下为什么会出现设备异响？”。这种题没有标准死答案，最考验模型的逻辑。

***

在任务配置中 **支持配置各题目类型生成的比例**（比如：我要 30% 的判断题用于测幻觉，70% 的简答题测理解）：在 `Easy Dataset` 中，你可以通过多种方式生成和配置评估数据集（测试集）：

<figure><img src="https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=NjRlNGFlYjBhM2UyN2ZlNTE4ODA5ZjVjMThkZTg2YjZfQTVFYVlydjlsYmllcXY0ZTRXZm12Ykd5YUZWNkpHRXdfVG9rZW46UnprZGJJSnlUb3UwcXZ4MlI1M2NQSGM2bjJpXzE3NjgyMzA4OTg6MTc2ODIzNDQ5OF9WNA" alt=""><figcaption></figcaption></figure>

* 从领域文献中提取测试集
* 从训练集添加或生成测试集变体
* 导入自定义/平台内置测试集

***

**从领域文献生成测试集**

不管是 PDF 还是 Docx 格式的领域文献，系统支持直接导入。后台会把这些长文本切分成小块（Chunk），然后通过提示词工程，让大模型基于这些文本块自动生成题目。我们首先来到【数据源-文献处理】模块，导入一份小米 2025 Q3 季度的财报文档：

<figure><img src="https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=MWVmY2VjZjdjMGNjNmVmOGNlOTIxYjZhMzQ3MGFiYmRfTjh2dWtXVnRjVHpYR1RLendUQVFZTnJvNWpxa1l3QkhfVG9rZW46Q2M1UGJlaG1jb1h3U2V4cDBEMmNHbDAxbnRmXzE3NjgyMzA5OTg6MTc2ODIzNDU5OF9WNA" alt=""><figcaption></figcaption></figure>

系统解析完成后，会对文档进行自动切块，为了保证后续在文本块上生成的测试集更符合主题，我们批量编辑文本块：在每个文本块的开头增加全局摘要信息：

<figure><img src="https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=MDM3MWQxN2FhZTk5NmMxNTBjZjgzNDY5NDBhYTcwZjFfUDRscHhFenV1d0huM2VzQnhjVzVrakgzQ2wzS21ETXFfVG9rZW46RWFPM2JZRkxzb0RISk94Z1dvV2NVbGczbnZnXzE3NjgyMzA4OTg6MTc2ODIzNDQ5OF9WNA" alt=""><figcaption></figcaption></figure>

然后，我们可以选择基于单个文本块生成测试集，或自动生成测试集（后台自动读取并处理未生成测试集的文本块），系统将根据我们前面在项目设置中设置的几种题目类型的比例自动生成测试题目（默认的题目类型判断题、单选题、多选题、简答题、开放题为 `1:1:1:1:1`）。

<figure><img src="https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=NmIxZDZlYTVlN2U4MGEzMWQyZGY3ZGNiNTAyYzEzZDVfQlFualRNbG14bThZNk10THgyRTFtV1psSFppTDlWOGhfVG9rZW46QWNCYmJjdzcwb1NUOVR4U0Y2SmN2QkRhbkQwXzE3NjgyMzEwNjU6MTc2ODIzNDY2NV9WNA" alt=""><figcaption></figcaption></figure>

建议：

* 先用 “单个生成” 跑通流程，确认题型质量与期望一致，在执行自动生成任务。
* 比例配置先从保守开始：开放题比例不要太高（后续教师模型评估成本更高）

***

**测试集管理**

点击每个文本块上的 **已生成测试题** 标签，我们将跳转至【评估-评估数据集】模块，在这里你可以看到已经生成的所有数据集，你可以根据题目类型、题目内容和标签进行筛选：

<figure><img src="https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=OGIzODAyMzkyZTIzZDM3ODRkZWY3NmE4MWI3NWE4MjBfWjhTdVp6dExSQjc0bkJ6U1hVMUJobWcxMFBYME00cWNfVG9rZW46TldsSGJQR2ROb3FkOHN4WUE4Q2Nsd0pybk1oXzE3NjgyMzA4OTg6MTc2ODIzNDQ5OF9WNA" alt=""><figcaption></figcaption></figure>

点击单个题目，可以查看题目详情：

<figure><img src="https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=OWUwNjRkNDc1ZGRhYmU2MTRhMTRjYTYzYTE5MGQ3YTVfMHBvMnlFNW9ZOFFObzdCYWFkWkZpTG9ycGk0TnZ2TDBfVG9rZW46TUZnNmJ5ekw5b1JsSUR4d1pHUGNvckk1bk4zXzE3NjgyMzA4OTg6MTc2ODIzNDQ5OF9WNA" alt=""><figcaption></figcaption></figure>

问题、选项、答案都可以自由编辑，你也可以对题目进行打标签、备注、删除等等：

<figure><img src="https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=ODQ2NGUxYzRhMjc2Y2QwNGNiZTYxM2M4N2JlNTMzZGZfTng2OGlKT0thWWExSFdEU0RwVVc2ZUpSZ0hiQnpnOFlfVG9rZW46TVhoWWJkek1ub3NlTjl4RnpVQ2NqVktobmtnXzE3NjgyMzA4OTg6MTc2ODIzNDQ5OF9WNA" alt=""><figcaption></figcaption></figure>

***

**从已有数据集添加和生成**

在以前的项目中，你可能已经使用 `Easy Dataset` 生成过数据集（训练集），我们也支持直接从已有数据集上标注和生成测试集。下面我们来到【数据集-单论问答数据集】模块，可以看到之前生成过的数据集：

<figure><img src="https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=OThmMTA1OTUwYThkZDZmNzc3MmI2OTk1NzVlYjI0YzVfY25RcVhyejU0NVRGZUhFUVRybHU3dWdMNExCYUk1S1VfVG9rZW46UXFzR2JaakYwb0pKdWl4Y1RpNmNGbzVPbmpoXzE3NjgyMzA4OTg6MTc2ODIzNDQ5OF9WNA" alt=""><figcaption></figcaption></figure>

进入数据集详情页，我们可以直接将当前数据集添加到评估数据集（测试集），同时，系统给原数据集打上 Eval 标签（用于后续筛选/识别）：

<figure><img src="https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=MWE1MWIzMTJiM2NmZTY5ZjA1OTA2MWI3NDZkMzI0MDBfdTZvcEtVTlJScnlyUkE1ZjF2ZEd6dUZJSDRRMFV4bGZfVG9rZW46TnF0S2J4S0NWb3JJVUZ4Y0N4S2N6V2Fjbm1kXzE3NjgyMzA4OTg6MTc2ODIzNDQ5OF9WNA" alt=""><figcaption></figcaption></figure>

如果训练集太少或多样性不足，模型有时候会 “死记硬背”。我们也可以把一道现有的数据集题目自动改写生成评估集变体（比如换个问法，或者把选择题改成判断题），看看模型是不是真的理解了。

<figure><img src="https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=NmJiYjI4M2ZmMDNjNDM4MGM2NmFjYmNmYTlkNjZhNDVfR3k5UHZLMk5BRmNnelNyWmYyRWdyYU9lTkNORDdQUWpfVG9rZW46RGVYNWJ0Q0x0b0drelV4R3R6RmNWWDU3bnhWXzE3NjgyMzA4OTg6MTc2ODIzNDQ5OF9WNA" alt=""><figcaption></figcaption></figure>

点击：【生成评估集变体】可以选择要生成的题目类型和数量：

<figure><img src="https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=NjkxOWRkOWE1OGY1ZjQ2ODZlMjZjM2JlMGRkYjZhYWZfVHptWk41TDNVNU5scVFXSTczU0ZzYVlMWXNncEJDNTRfVG9rZW46WFlTcWJzbzFJb0FjRGR4UTZPRmMzUEpybkdoXzE3NjgyMzA4OTg6MTc2ODIzNDQ5OF9WNA" alt=""><figcaption></figcaption></figure>

在常规的思路中，一般我们要从所有数据集中划分出一定比例（如 15%）作为测试集。但是，在小规模的数据集上，如果直接划分出一定比例的测试集可能会导致原有的训练集数量和多样性不足，导致模型训练效果差。如果使用 `Easy Dataset` 生成的数据集，我们可以全部用于训练集，另外一部分测试集我们可以直接在现有的数据集上生成变体，或重新从文本块提取。这样既能保证训练集的多样性不会受到损失，还能保证有足够丰富的测试集来支撑最终模型效果的评估。

***

**导入导出测试集**

如果你已经有准备好的测试集，只是想使用 `Easy Dataset` 来做评估任务，可以到【评估-评估数据集】模块直接进行导入：

<figure><img src="https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=N2RlZDY0MGVmMGMyYjA4NDUxNzYwZWM4MWJiYThjNmVfS1pQcWNaakVUREJlS0ZCT2JMOHZCQnJKcHdhMU9TZW5fVG9rZW46WDVjd2JleWtpb0FUQXl4WXN2RGNUd1pabkxiXzE3NjgyMzA4OTg6MTc2ODIzNDQ5OF9WNA" alt=""><figcaption></figcaption></figure>

目前支持从 `JSON、XLS、XLSX` 几种类型的文件进行导入，需要将文件处理成规定格式：

<figure><img src="https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=YmVlZmQ5YmJkNGUxYjJmZDBiYmVmYTYzNzk3ZTA2YzZfalZEWktFdGZrN1J2MEYySGFYV2dvMnFtZUVUV092d3RfVG9rZW46VkdTVmJpdld1b0QwTFF4VTh5Z2NUc0ZFbnVjXzE3NjgyMzA4OTg6MTc2ODIzNDQ5OF9WNA" alt=""><figcaption></figcaption></figure>

你可以直接下载对应题型和文件类型的模版，然后按照模版进行补充：

<figure><img src="https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=YzE0OTdjZjNjODYzMWY3MzZjY2ExYmNiMTVjMGY2NDRfN3k1UzRmSHF6MEs0bnJwNE13TzZUd2dqUU9aNnI3YTRfVG9rZW46TkcxVGJJTHAxb0pxSW54MVh5MWNYMVVMbkJkXzE3NjgyMzA4OTg6MTc2ODIzNDQ5OF9WNA" alt=""><figcaption></figcaption></figure>

另外，平台还内置了丰富的领域知识数据集，如果你想测试模型在特定领域下的表现，可以直接选择【导入内置数据集】并选择对应学科进行导入：

<figure><img src="https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=MDUyMzczYjY0MTFkOGRhMTAwMTMyZTM4ZmEzYjM4ZjBfSmtTb29FTVQxdUVQUTR3Znh3eEluN3JUQXM0emF0Z0ZfVG9rZW46SG1ZNWIwQm5Ob1NmM2l4eGxHRWNmZ1o0blVvXzE3NjgyMzA4OTg6MTc2ODIzNDQ5OF9WNA" alt=""><figcaption></figcaption></figure>

每个学科下都内置了几百道不同难度的题目（大部分为单选或多选题）：

<figure><img src="https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=YzJlYTQzYTZkMDhhNzA2MmYwNWMzZWRlOTVhYTJiMDJfYlNtaEVZWmFyWWRkVlQ4bWV0WUhOZ1lFYUlkVU5SYmdfVG9rZW46SVlLemJSMjZrb1pPVnJ4YzFYbGNUajJKblFlXzE3NjgyMzA4OTg6MTc2ODIzNDQ5OF9WNA" alt=""><figcaption></figcaption></figure>

测试集处理完成后，我们也可以直接进行导出（支持自定义导出范围和格式），你可用于其他评估系统：

<figure><img src="https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=YjVhMDRlZWQ1NDVmNWY0MDA1NWQ3NTgyNjg0OTY3NWZfM1hUSVpHbWZES2tkNjE4b1BWTkZZRGJSZUQ1MkZkYzlfVG9rZW46TjBJMmI3VXVNb1V6REl4Zjh2cGNoNFphbmZnXzE3NjgyMzA4OTg6MTc2ODIzNDQ5OF9WNA" alt=""><figcaption></figcaption></figure>

***
