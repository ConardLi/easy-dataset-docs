---
icon: up
---

# 更新日志

{% hint style="info" %}
同步：[https://github.com/ConardLi/easy-dataset/releases/](https://github.com/ConardLi/easy-dataset/releases/)
{% endhint %}

### [\[1.3.1\] 2025-05-14](https://github.com/ConardLi/easy-dataset/releases/tag/1.3.1)

**🔧 修复**

1. 修复数据集优化过程中意外生成 COT 的问题
2. 修复文本处理页上传时已移除文件仍被处理致报错的问题

**⚡ 优化**

1. 将本地文件存储重构为本地数据库存储，大幅优化大量数据下的使用体验
2. 随机取出问题中的问号（支持配置）
3. 优化多项功能使用体验

**✨ 新功能**

1. **领域树灵活管理模式**
   * 新增/删除文献时支持三种模式：
     * **修订模式**：仅修正新增/删除文献相关的领域树节点，最小化影响现有结构
     * **完全重建模式**：基于所有文献目录重新生成领域树（现有逻辑）
     * **锁定模式**：固定当前领域树，新增/删除文献不触发更新\
       [![image](https://private-user-images.githubusercontent.com/30708545/443675834-ce3b8ae9-8931-4e28-9264-9f4755bf7d47.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDcyMzY0MDIsIm5iZiI6MTc0NzIzNjEwMiwicGF0aCI6Ii8zMDcwODU0NS80NDM2NzU4MzQtY2UzYjhhZTktODkzMS00ZTI4LTkyNjQtOWY0NzU1YmY3ZDQ3LnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTA1MTQlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUwNTE0VDE1MjE0MlomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTJlZTRjNmUxMTEyMmY4ZmExOTMwNWNiOGIyMDdjNTBmMTE5NjM4NzkzMGNlNGQ1Y2IzOTI1ZTI4YzZjN2ZkZjYmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.BSwPfOoWwK6i9YNf3iwwj6H7aAXXoJQgM8EFvLs28d0)](https://private-user-images.githubusercontent.com/30708545/443675834-ce3b8ae9-8931-4e28-9264-9f4755bf7d47.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDcyMzY0MDIsIm5iZiI6MTc0NzIzNjEwMiwicGF0aCI6Ii8zMDcwODU0NS80NDM2NzU4MzQtY2UzYjhhZTktODkzMS00ZTI4LTkyNjQtOWY0NzU1YmY3ZDQ3LnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTA1MTQlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUwNTE0VDE1MjE0MlomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTJlZTRjNmUxMTEyMmY4ZmExOTMwNWNiOGIyMDdjNTBmMTE5NjM4NzkzMGNlNGQ1Y2IzOTI1ZTI4YzZjN2ZkZjYmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.BSwPfOoWwK6i9YNf3iwwj6H7aAXXoJQgM8EFvLs28d0)
2. **多种文本分块策略**
   * **Markdown分块**：根据文档标题自动分割，保持语义完整性（适用于结构化Markdown）
   * **自定义分割符递归分块**：按优先级递归尝试多级分隔符（可配置），适合复杂文档
   * **自定义分割符固定长度分块**：按指定分隔符切分后组合为固定长度（可配置）
   * **Token分块**：基于Token数量分块（非字符数），适配模型输入要求
   * **程序代码智能分块**：根据编程语言语法结构智能分割，避免语法断裂\
     [![image](https://private-user-images.githubusercontent.com/30708545/443675054-fb98d30b-e929-4cb3-9cea-8fabd80da93a.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDcyMzY0MDIsIm5iZiI6MTc0NzIzNjEwMiwicGF0aCI6Ii8zMDcwODU0NS80NDM2NzUwNTQtZmI5OGQzMGItZTkyOS00Y2IzLTljZWEtOGZhYmQ4MGRhOTNhLnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTA1MTQlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUwNTE0VDE1MjE0MlomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPWIxZDY5MWRmYjk5OWI0ZGVmZTczYmFjZjg2NDViNjJkZDRmZWFkMGZhZjcyYjI2MmU1MjA5OTM0MzY2M2ViYmQmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.i_SWtAKiFdSN_mg_HHPbT2qTFDUwBpPUBuDfZmNsqy0)](https://private-user-images.githubusercontent.com/30708545/443675054-fb98d30b-e929-4cb3-9cea-8fabd80da93a.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDcyMzY0MDIsIm5iZiI6MTc0NzIzNjEwMiwicGF0aCI6Ii8zMDcwODU0NS80NDM2NzUwNTQtZmI5OGQzMGItZTkyOS00Y2IzLTljZWEtOGZhYmQ4MGRhOTNhLnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTA1MTQlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUwNTE0VDE1MjE0MlomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPWIxZDY5MWRmYjk5OWI0ZGVmZTczYmFjZjg2NDViNjJkZDRmZWFkMGZhZjcyYjI2MmU1MjA5OTM0MzY2M2ViYmQmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.i_SWtAKiFdSN_mg_HHPbT2qTFDUwBpPUBuDfZmNsqy0)
3. **可视化自定义分块**
   * 支持通过图形界面手动调整分块边界，实时预览分块效果\
     [![image](https://private-user-images.githubusercontent.com/30708545/443675148-efe9ef9d-8db1-489e-870f-811649e69fbb.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDcyMzY0MDIsIm5iZiI6MTc0NzIzNjEwMiwicGF0aCI6Ii8zMDcwODU0NS80NDM2NzUxNDgtZWZlOWVmOWQtOGRiMS00ODllLTg3MGYtODExNjQ5ZTY5ZmJiLnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTA1MTQlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUwNTE0VDE1MjE0MlomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTE2NGVlZDlmMWJiM2U3ZjQ1Nzc1NWVhYmVmNjA3OTdlMjdhM2Y3NjkyN2UyYzJhZDNjYjBmNzhhMjI2YWRkZTkmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.h5vffql_BUnE8tO1JB3RRIAOLVNaX73av4G6sxhqT64)](https://private-user-images.githubusercontent.com/30708545/443675148-efe9ef9d-8db1-489e-870f-811649e69fbb.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDcyMzY0MDIsIm5iZiI6MTc0NzIzNjEwMiwicGF0aCI6Ii8zMDcwODU0NS80NDM2NzUxNDgtZWZlOWVmOWQtOGRiMS00ODllLTg3MGYtODExNjQ5ZTY5ZmJiLnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTA1MTQlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUwNTE0VDE1MjE0MlomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTE2NGVlZDlmMWJiM2U3ZjQ1Nzc1NWVhYmVmNjA3OTdlMjdhM2Y3NjkyN2UyYzJhZDNjYjBmNzhhMjI2YWRkZTkmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.h5vffql_BUnE8tO1JB3RRIAOLVNaX73av4G6sxhqT64)
4. **客户端工具增强**
   * 新增本地日志存储，可一键打开日志目录排查问题
   * 新增清除缓存功能，支持清理历史日志和数据库备份文件

### \[1.3.0-beta.1] 2025-05-06

**本次更新在修复系统问题的基础上，对存储方式进行了重大优化，将本地文件存储重构为本地数据库存储，为提升大量数据下的使用体验带来大幅改进。由于此次改动较大，特发布 beta 版本供大家体验。如果大家在使用本版本过程中遇到任何问题，欢迎通过 Issues 提交反馈，帮助我们进一步完善产品。**

**🔧 修复**

1. 修复数据集优化过程中意外生成 COT 的问题
2. 修复了文本处理页上传时已移除文件仍被处理致报错的问题

**⚡ 优化**

1. 将本地文件存储重构为本地数据库存储，大幅优化大量数据下的使用体验
2. 随机取出问题中的问号（支持配置）
3. 优化多项功能使用体验

**✨ 新功能**

1. 客户端新增本地日志存储，可打开日志目录排查问题
2. 客户端新增清除缓存功能，可清理历史日志文件和备份的数据库文件

***

### \[1.2.5] 2025-04-13

**🔧 修复**

1. 修复第一次配置模型报错的问题
2. 修复 Docker 打包镜像报错的问题

***

### \[1.2.4] 2025-04-12

**⚡ 优化**

1. 使用 OPEN AI SDK 对模型交互接口进行重构，提升兼容性

**✨ 新功能**

1. 支持视觉模型配置
2. 支持使用自定义视觉模型解析 PDF，准确率更高
3. 模型测试支持发送图片，对视觉模型进行测试
4. 数据集详情页支持查看所属文本块
5. 支持用户自己编辑文本块
6. 支持下载和预览查看解析好的 Markdown 文件

***

### \[1.2.3] 2025-03-30

**⚡ 优化**

1. 增强模型默认最大输出 Token 限制
2. 去除更新失败弹窗
3. 去除部分干扰错误日志输出

**✨ 新功能**

1. 支持一键打开客户端数据目录
2. 支持模型温度、最大生成 Token 数量配置
3. 支持两种 PDF 文件解析（基础解析、MinerU 解析）
4. 支持数据集导出 CSV 格式

***

### \[1.2.2] 2025-03-24

**🔧 修复**

1. 修复领域树视图下无法选中问题、删除问题失败的 Bug
2. 修复升级新版本链接可能不准确的问题

**⚡ 优化**

1. 去除答案和思维链中多余的换行符
2. 去除更新失败弹窗、更新下载最新安装包地址

**✨ 新功能**

1. 文献管理支持已生成、未生成问题的筛选

***

### \[1.2.1] 2025-03-23

**🔧 修复**

1. 修复文本块排序不准确的问题

**⚡ 优化**

1. 下调默认并发量为 3 （解决触发部分模型限流问题）
2. 优化问题生成提示词，提升问题生成质量
3. 下调最小分割字符数为 100，上调最大分割字符数为 10000
4. 当模型未按标准格式输出时，日志增加原始输出信息

**✨ 新功能**

1. 支持编辑问题、自定义问题
2. 支持数据集直接在 LLaMa Factory 中使用
3. 支持配置用户自定义提示词

***

### \[1.1.6] 2025-03-19

**🔧 修复**

1. 修复 extractThinkChain 报错的问题
2. 修复 NPM 依赖弃用问题
3. 修复问题筛选，全选联动的问题

**⚡ 优化**

1. 优化上传多个文献时删除文献后重新构建领域树的操作
2. 客户端打开后默认最大化，不再全屏
3. 优化思维链内容，去除参考文献的话术

***

### \[1.1.5] 2025-03-18

**🔧 修复**

1. 修复缓存导致的项目列表为空的问题
2. 修复问题分割字数配置不生效的问题
3. 修复部分特殊文件名导致的报错问题
4. 修复部分 Loading 状态失效的问题

**⚡ 优化**

1. 客户端内打开外部链接，默认跳转浏览器
2. 继续优化数据集结果生成的成功率
3. 大量问题下领域树展示性能优化

**✨ 新功能**

1. 新建项目时可选择复用其他项目的模型配置
2. 单个项目支持上传多个文件（共享领域树）
3. 问题管理增加已生成/未生成数据集的筛选
4. 支持 docx 类型文件上传



