---
icon: book-atlas
---

# 知识科普

### 一、微调数据集的常见分类

很多同学弄不清楚，给模型喂的数据究竟需要什么样的格式，实际上就是还没分清楚几种常见的微调任务类型。为了在不同的业务场景下解决不同的问题，我们可能采取的微调任务类型是不一样的，那所用的数据集格式肯定也会有所差别。所以，为了弄清楚我们要整理什么样的数据集格式，先要搞清楚我们要做的微调属于哪种任务场景，下面是我梳理的对常见微调任务的一个分类图：

<figure><img src="https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=YmQzNjNhMWFmOWRhODg5M2UzZmQzODFjZDE4NGQ2MmZfWFFsTFM0VG9IMW93cFZMZ3ljZmVmVzhWSU5MbmYwZW5fVG9rZW46UVM3eWJoZERjb25hUFZ4WXg3NWNTWnZRbmZoXzE3NDcyMjM0MTA6MTc0NzIyNzAxMF9WNA" alt=""><figcaption></figcaption></figure>

***

#### 1.1 预训练

从零开始训练一个模型，一般这个流程叫做预训练，这个过程的目的就是让模型掌握语言的通用规律，以及基本的语言理解能力。目前我们市面上主流的大模型，比如 `ChatGPT、DeepDeek` 等等，都属于 “自回归模型”，而 “自回归模型” 的本质就是：

* **用过去的自己来预测未来的自己**。

<figure><img src="https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=YWI4OGY3ODBlODFiYzhlZjM1YmU0N2VmOGZkNzVhZTBfeTRaT3dIWm1Db2Ftakp1OElpdmxUdUtwd3VROVF5SGNfVG9rZW46R0tFemJNa0p4b1FWMDR4NHJ4V2NCZkRUbktjXzE3NDcyMjM0MTA6MTc0NzIyNzAxMF9WNA" alt=""><figcaption></figcaption></figure>

我们都知道，大模型输出文本的时候是按照 `Token` 来输出的。`Token` 简单理解就是把句子拆成最小语义单元（如中文拆字 / 词，英文拆词或子词）。回答被拆分出了 4 个 `Token`，每个 `Token` 都是根据前面的问题 + 已经输出的 `Token` 预测出来的。在预训练的数据集中，这些关键字出现在一起的次数越多，那模型输出的概率越大。所以我们的数据集越丰富，模型预测 `Token` 输出的准确率就越高，最终的输出效果也就更好。所以在预训练的过程中，我们一般用海量非结构化文本（比如书籍、网页、对话），通过「预测下一个词」来训练模型，这也就意味着预训练的数据集格式是没有明确要求的，例如下面这些数据我们可以直接用于训练：但是在特定领域的微调上，就不能用非结构化文本了，我们可以这样理解：

<figure><img src="https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=MTkzNzY3MmY0OWM4OWIxYzc4OWI4MGEyODhkNmQ5ZjFfampweXpadWVFUWxKSW80ZFhoOXpHSFZacUFyc3NjaG9fVG9rZW46QXg1TmJvblJjb0pTdHN4UW02b2N2VEx3bkpjXzE3NDcyMjM0MTA6MTc0NzIyNzAxMF9WNA" alt=""><figcaption></figcaption></figure>

* **预训练阶段**：就像婴儿学说话，听到的是各种声音（非结构化），不管是什么，直接让他多听，慢慢多就能学会语言规律；
* **指令微调阶段**：就像教小孩做事「听到问题要回答」，需要明确告诉他这是什么问题，正确答案是什么。如果继续用没规律（非结构化）对话，他对你要让他学的事情就不会印象太深刻。

而预训练的过程，我们可以理解成一个无需人工监督，自己学习和锻炼能力的过程，对应的，想要让模型具备特定的能力，就要用到监督微调了。

***

#### 1.2 监督微调

监督微调（`Supervised Fine-Tuning，SFT`），顾名思义就是需要人去监督微调的过程。比如：我们想训练一个中英翻译模型，把英文翻译为中文就是一个非常明确的需求场景，所以在数据集里只需要有输入、输出就可以了：

```json
{"input": "Hello", "output": "你好"}
```

**1.2.1 指令微调**

那假如我们想让模型具备多种语言理解的能力呢，这时候只靠两个字段就不够了，因为在 `Input` 是同样一个词语的时候，根据我们想让模型完成的不同任务，`output` 可能是不一样的，这时候我们就要多引入一个指令的概念，比如这个数据集：

```json
[
  {
    "instruction": "将这句英文翻译成法语",
    "input": "Hello, how are you?",
    "output": "Bonjour, comment ça va ?"
  },
  ...
]
```

我们告诉模型明确的指令：将英文翻译为法语，再将 `Input`（英文）、`Output`（法语）告诉模型， 模型就能准确理解要做什么了，这就是指令微调。指令微调常见的业务场景：

* **智能教育**：实现作业辅导、规划个性化学习路径、辅助语言学习。
* **智能办公**：可处理文档、邮件，进行日程管理。
* **智能翻译**：应用于专业领域翻译、特定场景翻译及多语言交互。
* **数据分析**：让模型根据分析需求指令，对数据进行准确解读和洞察。

指令微调典型开源数据集（包含指令、输入、输出字段）：

<figure><img src="https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=Y2Q0MjVjZDQzODg5NjkxMzRiMDIwODAxMDg4MDIxYmNfWlVhZHRWRnlVTmhHeVpzYXhYNVk2UnFNbFB2dzRPNFFfVG9rZW46R2RITmI2a0dab2RQajB4VVBDN2NYMVJwblFlXzE3NDcyMjM0MTA6MTc0NzIyNzAxMF9WNA" alt=""><figcaption></figcaption></figure>

> `Alpaca` 数据集：由斯坦福大学创建，通过微调模型生成，包含约 5.2 万个指令跟随数据样本。涵盖多种任务，如常识问答、文本生成等，助力模型在指令理解和生成方面优化。

***

**1.2.2 对话微调**

对话微调（`Dialogue Tuning`） 是通过多轮对话数据训练模型生成连贯、符合语境的回复，强调对话历史的上下文理解和回复的自然流畅性。其核心在于教会模型处理对话中的逻辑关系、情感表达和角色身份，对话微调的数据集通常包含对话的上下文以及对应的回复。

```javascript
[
  {
    "dialogue": [
      {"role": "user", "content": "今天天气怎么样？"},
      {"role": "assistant", "content": "北京今日多云转晴，气温22℃，适合户外活动。"},
      {"role": "user", "content": "那适合去长城吗？"},
      {"role": "assistant", "content": "长城景区海拔较高，建议携带外套，注意防晒。"}
    ]
  },
  ...
]
```

对话微调数据集的核心特点：包含多轮对话上下文、标注角色身份，注重回复连贯性与逻辑性。通过这样的数据，模型可以学习到在不同对话场景下如何生成合适的回复，从而提高对话的连贯性和相关性。对话微调常见的业务场景：

* **智能客服系统**：提升客服机器人在处理用户咨询时的对话能力，能够更准确地理解用户意图并提供解决方案。
* **聊天机器人**：让聊天机器人更自然地与用户进行多轮对话，提高用户体验。
* **语音助手**：优化语音助手在语音交互中的对话表现，使其更符合用户的期望。

对话微调典型开源数据集：

<figure><img src="https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=ZmIxOTIyZDQ1MTg3ZTg5ZDFlODFmNTUzZDdhMTIxYzRfSVFZbHhqT2JKRjhkU3pidktrV1VkQlJqMmljM0JCazRfVG9rZW46TGFnV2JYdEV4b3ByRTZ4dVRXNmNYRGtSbjlmXzE3NDcyMjM0MTA6MTc0NzIyNzAxMF9WNA" alt=""><figcaption></figcaption></figure>

> 一个用于训练对话模型的多语言问答数据集，其内容结构和风格符合 ShareGPT 对话格式，数据集中的每个样本为一个对话轮次，包含人类提问和模型回答，数据覆盖多语言（英语、西班牙语、中文、俄语等）和多样化领域。

***

**1.2.3 领域适配**

领域适配（`Domain Adaptation`）是指将模型在特定领域的数据上进行微调，使其更好地适应特定领域的任务和需求。

```json
[
  {
    "instruction": "分析患者的症状描述",
    "input": "55岁男性，持续性胸骨后疼痛3小时，含服硝酸甘油无效",
    "output": "可能诊断：急性心肌梗死（STEMI），建议立即行心电图检查及心肌酶谱检测",
    "domain": "医疗"
  },
  {
    "instruction": "解释法律条款",
    "input": "《民法典》第1032条",
    "output": "该条款规定自然人享有隐私权，任何组织或个人不得以刺探、侵扰、泄露、公开等方式侵害他人隐私权",
    "domain": "法律"
  },
  ...
]
```

领域适配数据集的核心特点：领域术语标注（如医学本体库、法律术语库）、复杂规则建模（如药物相互作用、合同条款逻辑）、场景化数据增强（如模拟问诊对话、合同审查流程）；领域适配典型的业务场景：

* **医疗领域适配**：用于病历分析、疾病诊断辅助、医疗文献检索等。
* **法律领域适配**：辅助法律文件分析、案例检索、合同审查等。
* **金融领域适配**：用于风险评估、市场分析报告生成、金融产品推荐等。

领域适配典型开源数据集：

<figure><img src="https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=ODQxNjI5NzIzYmU2ZWIyYjEzM2NmZWRhZmFmODQxMmNfOHdNQUJZaDcxZkhXOWpUNmJRNVVHOGFuWmdvZ0FwNUlfVG9rZW46SlV2aWJDWGNmb1JBakl4UVpZS2N0RmNhbk5GXzE3NDcyMjM0MTA6MTc0NzIyNzAxMF9WNA" alt=""><figcaption></figcaption></figure>

> 基于 `PubMed` 文献的医学问答数据集，包含医学研究相关问题，适合医疗信息抽取与领域适配任务。

***

**1.2.4 文本分类**

文本分类（`Text Classification`），是自然语言处理中的一个经典任务，目的就是通过标注数据训练模型对文本进行类别预测或标签分配。这类任务需要模型理解文本语义与类别特征的关系，适用于需要结构化输出的场景。

```json
[
  {"text": "这款手机续航长达48小时，拍照效果惊艳", "label": "positive"},
  {"text": "系统频繁卡顿，客服响应速度慢", "label": "negative"},
  {"text": "量子计算机突破新型纠错码技术", "label": "science_news"},
  {"text": "央行宣布下调存款准备金率0.5个百分点", "label": "finance_news"}
]
```

文本分类微调的典型业务场景：

* **情感分析**：商品评论情感极性识别（正面/负面/中性）
* **内容审核**：检测违规内容（涉政/暴力/广告）
* **新闻分类**：自动归类至财经/科技/体育等栏目
* **意图识别**：用户query分类（咨询/投诉/比价）

文本分类典型开源数据集：

<figure><img src="https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=NjAyNTM3MGVhYTg4NjAwMDlkMDMzOTNiNGM2N2FkZWRfYjU3WnNJN0NicUxZQkY1WDBrVlNOZmZsWlRzdG1WTTlfVG9rZW46V0NiZGI2Y21hb0VaY1Z4aFpDZ2MxVUJWbnJMXzE3NDcyMjM0MTA6MTc0NzIyNzAxMF9WNA" alt=""><figcaption></figcaption></figure>

> `imdb` 大型电影评论数据集，包含用户评论到电影评分的映射关系，适用于对评论进行积极、负面分类的微调任务。

***

**1.2.5 模型推理微调**

对于推理模型的微调其实是监督微调的一种特殊形式，通过在数据集中显式标注思维链（`Chain of Thought, COT`），训练模型不仅给出最终答案，还能生成逻辑推导过程。其核心在于让模型学会「分步思考」，适用于需要复杂逻辑推理的场景（如数学证明、代码调试）。在用于推理模型微调的数据集中，通常需要额外包含模型思考过程的部分：

<figure><img src="https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=NjdhMzc0ZWJmOGVjN2YyNTA4NDJmZGRjNzllYmU0NzNfVFRKMVhJSFE5alE0NkJ1eEVFRktDTld5anhCTzdJN01fVG9rZW46UDJJNGJITDZSb1VRTmh4RndwdWNFMkVvbnFiXzE3NDcyMjM0MTA6MTc0NzIyNzAxMF9WNA" alt=""><figcaption></figcaption></figure>

```json
[
  {
    "instruction": "解决数学应用题",
    "input": "小明买了3支铅笔，每支2元；又买了5本笔记本，每本比铅笔贵4元。总花费多少？",
    "chain_of_thought": [
      "铅笔单价：2元/支 → 3支总价：3×2=6元",
      "笔记本单价：2+4=6元/本 → 5本总价：5×6=30元",
      "合计花费：6+30=36元"
    ],
    "output": "总花费为36元"
  },
  ...
]
```

注意：其实并不是所有任务都适合用推理模型，因为推理模型的幻觉比较大，有些情况选择推理模型反而会起到相反的效果，在处理简单明确的任务时，推理模型可能会把问题复杂化，导致思考过度、响应较慢，甚至增加幻觉的风险。比如如果你让推理模型去完成检索、解释类的任务时，当它找不到可以参考的信息就会按照自己的思考过程进行输出，结果并不一定准确。下面则是一些适合用于推理模型微调的场景：

* **代码生成与调试**：推理模型能够理解复杂的编程问题，生成高效的代码解决方案，并辅助开发人员进行代码调试。
* **数学问题求解**：在数学建模、复杂计算和逻辑推理任务中，推理模型表现出色，能够提供详细的解题步骤和准确的答案。
* **复杂数据分析**：推理模型擅长处理需要多步骤推理和策略规划的复杂数据分析任务，帮助科学家和研究人员进行更深入的数据挖掘。
* **法律与金融分析**：在处理法律合同、金融协议等复杂文档时，推理模型能够提取关键条款，理解模糊信息，辅助决策。
* 数据集中的思维链，在某些特定场景下可能比较容易获取，比如在数学推理任务的微调上，一般数据集本身带的解题过程就可以作为思维链，比如下面的数学解题数据集：

<figure><img src="https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=M2VmYTM4MzI3YjU1ZDFmYWRiMWE3YmYwMWJmMjA5NzlfQmViakxzcHNCYW9xWjBmSlB2T1o0NUFYcWRiMU01cllfVG9rZW46UmFZemJENjBjb0VWQzF4eW9EM2N2TDBObkJkXzE3NDcyMjM0MTA6MTc0NzIyNzAxMF9WNA" alt=""><figcaption></figcaption></figure>

> 约 86 万道中国高中数学练习题、以及美国和国际数学奥林匹克竞赛的题目，每个问题的解答都采用了思维链（CoT）的格式。

还有就是靠带推理能力的大模型蒸馏获取，通过 `DeepSeek-R1` 等推理模型蒸馏而来。

***

#### 1.3 知识蒸馏

知识蒸馏（`Knowledge Distillation`）是将复杂模型（教师模型）的知识迁移到轻量级模型（学生模型）的技术，通过优化学生模型使其输出接近教师模型的“软标签”，从而在保持性能的同时降低推理成本。模型蒸馏的数据集构造应该是最简单的，在你完全信任大模型输出的条件下，你可以直接将大模型产出的问答对作为数据集，最后在进行人工的质量评估和验证即可。模型蒸馏典型开源数据集：

<figure><img src="https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=ZDIyODM2MjQ0YWMwZDY5OWQyNDAwZjljYWUyZGE1ZjVfSFltaFliazNkSmFQWWFPZWZPTktKRzUwMWNQS3hobEZfVG9rZW46Slo1cWJwdWhWb2tTV3J4bjZUdWNQZDZmbm9lXzE3NDcyMjM0MTA6MTc0NzIyNzAxMF9WNA" alt=""><figcaption></figcaption></figure>

> 中文基于满血 DeepSeek-R1 蒸馏数据集，数据集中不仅包含 math 数据，还包括大量的通用类型数据，总数量为 110K。

***

#### 1.4 其他微调技术

**1.4.1 强化学习微调**

强化学习微调是在监督微调的基础上，通过人类来主动反馈优化模型生成质量的方法。其核心在于引入奖励模型（`Reward Model`）评估生成结果的合理性，并通过强化学习策略（如 `PPO` 算法）调整模型参数，使生成内容更符合人类偏好。

```json
[
  {
    "input": "请推荐一部科幻电影",
    "output": "《星际穿越》是一部经典科幻片，探讨了时间与亲情。",
    "reward_score": 4.5  // 人类标注的质量评分（0-5分）
  },
  {
    "input": "解释黑洞理论",
    "output": "黑洞是由暗物质构成的神秘天体，会吞噬一切物质。",
    "reward_score": 2.0  // 包含错误信息，得分低
  }
]
```

强化学习微调的典型业务场景：

* **对话系统优化**：在监督微调完回复相关性后，继续对齐人类价值观（安全、无害、有用性）。
* **内容生成**：在监督微调完写作能力后，继续优化输出风格（如幽默、正式）或避免敏感信息。
* **代码生成**：在监督微调完代码生成能力后，继续优化代码的可读性和正确性。

强化学习典型开源数据集：

<figure><img src="https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=MDI4MDEwNDMxNTA5ZmNhN2NlYWI5OTNjMTY0NWFlMGVfUkk1b05uOWVYUEY4UzdLUHF4RVdWRTBZczN6Zzdnb2hfVG9rZW46SDJEM2I3RFc3b2g2WVp4WUFEc2MwNVVxbjllXzE3NDcyMjM0MTA6MTc0NzIyNzAxMF9WNA" alt=""><figcaption></figcaption></figure>

> 人类偏好排序数据集，用于强化学习微调、训练奖励模型。

***

**1.4.2 多模态微调**

多模态微调（`Multimodal Fine-Tuning`）指通过文本、图像、语音等多模态数据训练模型，使其具备跨模态理解与生成能力。它和文本类模型的微调可以说是并列的两个范畴，其中也包括监督/非监督微调、强化学习微调等范畴。

```json
[
  {
    "text": "一只猫在追蝴蝶",
    "image_url": "https://example.com/cat.jpg",
    "caption": "一只橘色的猫正在追逐花园里的白色蝴蝶"
  },
  {
    "audio": "audio.wav",
    "text": "会议录音转写：今天的议题是...",
    "summary": "会议讨论了Q3销售目标与市场策略"
  }
]
```

注意这里的图片、视频、音频等多模态数据可以是 CND 地址、base64 编码，或者直接放在 HuggingFace 上，这里写相对路径，总之在训练时能够读取的到就可以。多模态微调的典型业务场景：

* **图文问答**：输入图片和问题，生成答案。
* **视频内容理解**：分析视频帧和字幕，生成摘要。
* **跨模态检索**：根据文本描述搜索相关图像/视频。
* 多模态微调典型开源数据集：

<figure><img src="https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=MDdlYzkzZjU2MGQ0MTQyZmYyYWJjNmY5OWY2ZmY2NWJfUk8wRVhXRWt2elFTNGthMFNsZUhKUmpuNHM2V2E3S29fVG9rZW46Qmh1R2JUZThZb2U5bXN4UThTbWNPV1BzbllsXzE3NDcyMjM0MTA6MTc0NzIyNzAxMF9WNA" alt=""><figcaption></figcaption></figure>

> 包含 50 个大规模视觉语言训练数据集（仅训练集），用于多任务视觉语言模型的微调。数据集结构包含 `images`（图片列表）和`texts`（对话文本），其中对话以用户提问、模型回答的形式呈现，覆盖问答、选择等任务（如TQA数据集示例）。

***

### 二、微调数据集的常用格式

对于模型微调的数据集，是没有明确的格式要求的，我们一般在代码中抹除各种微调数据集格式的差异，我们还拿之前微调实战教程中的代码来举例，回顾一下之前我们是怎么处理数据集的。我们先来看第一段代码：

<figure><img src="https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=NzRlNGQ2NDE1YzkzMDI1NzVkNTJmOTdmNGFlYWM3MDVfTERTazI0VlNuRlplb1lZanowSmNqSkNVMWxHdmpWTXNfVG9rZW46Wm0yZGJoTXR1b3BpR1J4bENWemNPTzlkbnF3XzE3NDcyMjM0MTA6MTc0NzIyNzAxMF9WNA" alt=""><figcaption></figcaption></figure>

这段代码其实就是在定义一个用于格式化微调数据集的模版，其中的三个 "{}" 其实就是对应的我们要传入的三个变量，分别对应原始问题、思考过程、最终答案三个部分。然后我们再来看下面这段代码，也很好理解，就是提取出我们原始数据集里面的三个变量：

<figure><img src="https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=OWZiY2EzOWNiMGE4M2E5OTRjMjU0NjFjMTNmYTIwNmZfTW1sVWV0aHd1U3J1VFE0VDNRYWRWRHh2bGI3VDNWdUpfVG9rZW46RHNpUGJYTGZHb2JFYW14TXNhRGNnRnQybmVkXzE3NDcyMjM0MTA6MTc0NzIyNzAxMF9WNA" alt=""><figcaption></figcaption></figure>

然后循环原始数据集，将这三个变量传入上面的模版，最终导入到一个 `text` 变量里。回顾一下我们之前的一个数据集格式：

<figure><img src="https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=Mzk0YzY1NTQ3YzQ3NzYyYzczZTMyYzMyOTExYjk1MDNfYm1HaFdrbFZ2VW9YWmFkS0dGcHFiQU5VT1ZjR3BlR3VfVG9rZW46QmJQMWI5V1JZb200aGd4NHdUcmNRa0V5bjFzXzE3NDcyMjM0MTA6MTc0NzIyNzAxMF9WNA" alt=""><figcaption></figcaption></figure>

调用上面的模版，每条数据集其实就转换成了下面这种格式：

<figure><img src="https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=YTlhNDI1MmVjNTIyYmVhYzQ0ODM5ZjQzZTFkYTZhZWVfN1p2c1RTVWxreG9NUnBXMW56MmJtTVNqd0FPVExPcDVfVG9rZW46R21xMWJqZ2xmb2plOXV4NjQ2VmM2dEl3bm1kXzE3NDcyMjM0MTA6MTc0NzIyNzAxMF9WNA" alt=""><figcaption></figcaption></figure>

最终所有数据集合并完，其实最终就是一个字符串数组：

<figure><img src="https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=YzhkNzEwNTVmN2UyNzQ4MDhkZGE5MjcwZWE0OGE5NTlfT1o3TTJEejdiVDZvNXo4Tk51eU1scU9RUXN6MllYZnpfVG9rZW46VlEyVmJxOHhYb2RHeXh4elJBeGNtellDblBlXzE3NDcyMjM0MTA6MTc0NzIyNzAxMF9WNA" alt=""><figcaption></figcaption></figure>

我们最后在回顾下微调模型的参数，其中有两个重要的参数：

<figure><img src="https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=ZDU4MWYwNGYxZmM4NmNlZmE5Njc4OWZmYjkxYWRkYWRfWDRjU0JSSWd1bXVBRENrWU95TThpQ21vZmlIektpRHNfVG9rZW46UUNzYmJicXBCb292aVl4a2tnTGNjWHl2bnRjXzE3NDcyMjM0MTA6MTc0NzIyNzAxMF9WNA" alt=""><figcaption></figcaption></figure>

所以其实最后喂给模型的还是一段格式化好的字符串，并非结构化的数据。

***

#### 2.1 Alpaca

`Alpaca` 最初是斯坦福大学于 2023 年发布的 **52k 条指令微调数据集**，由 `OpenAI` 的 `text-davinci-003` 模型生成，旨在通过指令跟随（`Instruction Following`）任务优化大语言模型（如 `LLaMA`）的性能。后续随着社区的发展，Alpaca 的 JSON 结构逐渐被抽象为一种 **通用数据格式**，并且扩展了一些字段如 `system`（系统提示）和 `history`（历史对话），支持多轮交互任务。适用于多种微调场景，很多主流框架（如 LLaMA-Factory、DeepSpeed）都可以直接加载 `Alpaca` 格式的数据集。这里我们参考 `LLaMA-Factory` 给出的两种在不同微调场景中 `Alpaca` 格式的数据案例：**Alpaca 格式的指令微调数据集**：

<figure><img src="https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=MjgzNzVmM2NiNGQ3MDkyOGQ3OGFlMDk2M2NlYzcwNmFfUmIxQ25XdGozTkxsQjRDVTBla01wTWtvTTV3ZDVITEZfVG9rZW46VGxJTWJycGtQb041WXZ4dEUzQWNuYm5QbnlmXzE3NDcyMjM0MTA6MTc0NzIyNzAxMF9WNA" alt=""><figcaption></figcaption></figure>

***

**Alpaca 格式的领域适配微调数据集**：

<figure><img src="https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=M2ZmNzM3N2UwOGUyNGY5OWQ2MmVkZjM5YTI0ODAxNDZfN0NUdHB5RnViZXBoa1RyOWtyak12UG5SZ1d3V0xpRDdfVG9rZW46TWZDS2JWUTg5bzNiZ0d4NmVNWmN0MzFJbjFxXzE3NDcyMjM0MTA6MTc0NzIyNzAxMF9WNA" alt=""><figcaption></figcaption></figure>

***

**Alpaca 格式的偏好数据集**：

<figure><img src="https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=NDJiMjNiMzkwOTg2NTYyY2U1ZmJjNmYwNmUyOTEyYTlfWXNaZ3AzMXZVdnFwR0k4MkZmUVljSUd6Yk45MmpmRXZfVG9rZW46QTdWM2JtNnlMb1lmRTd4QXdRb2NzUVRhbm5iXzE3NDcyMjM0MTA6MTc0NzIyNzAxMF9WNA" alt=""><figcaption></figcaption></figure>

***

#### 2.2 ShareGPT

**ShareGPT** 最早是一种数据格式标准，由社区设计用于规范多轮对话和工具调用场景的模型训练数据存储方式。其核心目标是通过结构化字段（如 `conversations` 列表、`tools` 工具描述）支持复杂交互（如用户提问 → 工具调用 → 结果整合）。随着格式的普及，社区基于 `ShareGPT` 格式构建了多个具体的数据集，这类数据集被称为 "ShareGPT 格式数据集"。**ShareGPT 格式的指令微调数据集**：

<figure><img src="https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=NDZmNGJiZTA0MWY2NzcyOTgyZjQ4YWQ0MzQ4NDEzYmNfaTZEVm5lS0N5aTVpNXNRS2g0U3lyRmdpY2hvQ3B4bUtfVG9rZW46SDkzSmJzQXcwb3VEakF4T3RjSGNtTVdYbmFmXzE3NDcyMjM0MTA6MTc0NzIyNzAxMF9WNA" alt=""><figcaption></figcaption></figure>

***

**ShareGPT 格式的偏好数据集**：

<figure><img src="https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=ZDNkNDcwNTI1ODBhMzkyNGI4MDI1OWMxM2JhYTQ2ZDVfeDdlMVZmSVJzMUZYVVdGenluODhwT1Y2aEQzMkdidTlfVG9rZW46TWppN2JXQ21mb0JUYVN4YnNPMWN5bENPbjhjXzE3NDcyMjM0MTA6MTc0NzIyNzAxMF9WNA" alt=""><figcaption></figcaption></figure>

***

**ShareGPT 格式的多模态数据集**：

<figure><img src="https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=ZjFkMGRjZjVkYzRkOWEyOWQ2YzA1NTI2NjNkMzlmNDhfaThPZUpoMEZxNEFETGtjb055MERpRmlkR0RqRktpWktfVG9rZW46U3ozOGJXTFdZb05sQWd4bmVWWWNjU09MbmFiXzE3NDcyMjM0MTA6MTc0NzIyNzAxMF9WNA" alt=""><figcaption></figcaption></figure>

***

**特殊的 ShareGPT 格式数据集：OpenAI 格式**

<figure><img src="https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=ZjZiMmQ2NGE3Y2QxNDUzNTg5OWVhYTU4ZDFhOTgxY2Nfb1ZvY0sxVjdldzVacTY2T1h0Rjl0VjFSYmQwTjM5VjJfVG9rZW46VFFnVmJLMEFyb1ljZ1V4VGdUVmNmQTFvbmZlXzE3NDcyMjM0MTA6MTc0NzIyNzAxMF9WNA" alt=""><figcaption></figcaption></figure>

***

#### 2.3 格式对比

下面是两种数据集格式的详细对比，大家可以根据自己的实际需求场景选择合适的格式：

<table data-header-hidden><thead><tr><th width="146.36328125"></th><th></th><th></th></tr></thead><tbody><tr><td>对比维度</td><td>Alpaca 格式</td><td>ShareGPT 格式</td></tr><tr><td>核心设计目标</td><td>单轮指令驱动任务（如问答、翻译、摘要）</td><td>多轮对话与工具调用（如聊天机器人、API 交互）</td></tr><tr><td>数据结构</td><td>以 <code>instruction</code>、<code>input</code>、<code>output</code> 为主体的 JSON 对象</td><td>以 <code>conversations</code> 列表为核心的多角色对话链（human/gpt/function_call/observation）</td></tr><tr><td>对话历史处理</td><td>通过 <code>history</code> 字段记录历史对话（格式：<code>[["指令", "回答"], ...]</code>）</td><td>通过 <code>conversations</code> 列表顺序自然体现多轮对话（角色交替出现）</td></tr><tr><td>角色与交互逻辑</td><td>仅区分用户指令和模型输出，无显式角色标签</td><td>支持多种角色标签（如 <code>human</code>、<code>gpt</code>、<code>function_call</code>），强制奇偶位置规则</td></tr><tr><td>工具调用支持</td><td>不原生支持工具调用，需通过 <code>input</code> 或指令隐式描述</td><td>通过 <code>function_call</code> 和 <code>observation</code> 显式实现工具调用，支持外部 API 集成</td></tr><tr><td>典型应用场景</td><td>- 指令响应（如 Alpaca-7B） - 领域知识问答 - 文本结构化生成</td><td>- 多轮对话（如 Vicuna） - 客服系统 - 需实时数据查询的交互（如天气、计算）</td></tr><tr><td>优势</td><td>- 结构简洁，任务导向清晰 - 适合快速构建单轮任务数据集</td><td>- 支持复杂对话流与外部工具扩展 - 更贴近真实人机交互场景</td></tr><tr><td>局限</td><td>- 多轮对话需手动拼接 <code>history</code> - 缺乏动态工具交互能力</td><td>- 数据格式更复杂 - 需严格遵循角色位置规则</td></tr></tbody></table>

### 三、微调数据集的不同用途

训练集教会模型「基础知识」，验证集优化「学习方法」，测试集检验「实战能力」，三者如同「预习-复习-考试」的学习闭环，缺一不可：

* **训练集** = **日常练习题**（通过大量练习掌握知识点）
* **验证集** = **模拟考试卷**（检测阶段学习成果，调整学习方法）
* **测试集** = **最终期末考试**（检验真实学习能力）
* **完整集** = **所有可用的习题库**（包含前三者的原始数据全集）

***

#### 3.1 训练集 — 老师教知识

* **作用**：模型学习规律的核心资料
* **示例**：教AI识别猫时，给它看**10,000张标注好的猫图**（包含不同品种、姿势）
* **关键点**：
  * 需覆盖各种可能性（白天/夜晚、近景/远景）
  * 相当于学生的课本+习题册

***

#### 3.2 验证集 — 学习效果检查

* **作用**：防止死记硬背，测试举一反三能力
* **典型场景**：训练中途用**2,000张新猫图**验证，发现模型错把「无毛猫」认成狗，于是调整训练策略
* **核心价值**：
  * 选择最佳模型版本（如不同神经网络结构）
  * 调整超参数（相当于改变学习计划表）

***

#### 3.3 测试集 — 最终能力考核

* **作用**：评估模型真实水平
* **必须遵守**：
  * 绝对隔离原则：测试集的 **5,000张猫图** 在训练中从未出现过
  * 相当于高考的「绝密押题卷」
* **常见误区**： 若用测试集反复调参，相当于提前偷看考题，成绩会虚高

***

#### 3.4 完整集 — 数据资源池

* **包含关系**：完整集 = 训练集 + 验证集 + 测试集
* **划分比例**（示例）：
  * 常规情况：70%训练 + 15%验证 + 15%测试
  * 小数据场景：80%训练 + 10%验证 + 10%测试

***

下面是一些关于这三种数据集的常见问题：

* **为什么不能混用？** ：如果测试集数据泄露到训练中，就像考前背答案，实际应用时遇到新题就会失败。
* **数据不够怎么办？**：交叉验证法：将完整集分成5份，轮流用4份训练、1份验证（类似「轮换座位考试」），合成数据：用图像翻转、文字替换等方式扩充数据量。
* **特殊场景处理**：时间序列数据：需按时间顺序划分（不能用随机拆分）。例如预测股价，必须用2023年前的数据训练，2024年数据测试；
