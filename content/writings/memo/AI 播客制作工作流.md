---
title: AI 播客制作工作流
date: 2025-04-11
draft: false
tags:
  - writing
  - AI
  - 播客
  - 工作流
  - memo
---
## ✨简化版 AI 播客工作流：

### 1. 收集资料
#### 1.1 收集主题相关的 官方网站 或 文档

#### 1.2（可选）收集主题相关的 Youtube 视频（或 播客）
#### 1.3 生成关于主题的深度研究分析文章
使用 chatGPT、Gemini、claude、Perplexity 或 Genspark 等的 search 和 deep research 功能各自生成一份关于某个主题的文档；
#### Prompt:
```
write a deep and detailed research article about {xxxx} in explanatory style.
the article should include following content.
1. Clear title - accurately reflects the content of the article and includes keywords for easy searching
2. Introduction/Overview - briefly introduce the topic, explain why it is important, and outline what the article will cover
3. Background Information - provide necessary context, explain relevant concepts and terms
4. Core Content - explain the technical content in depth in a logical order, which can be divided into multiple subsections
5. Charts/Examples - use visual materials and specific examples to enhance understanding
6. Code Examples (if applicable) - provide actual working code to show how to implement or apply the described technology
7. Common Problems/Challenges - discuss problems that may be encountered when using the technology and their solutions
8. Best Practices - provide suggestions and guidance for using the technology
9. Comparison with other technologies - compare related or competing technologies and explain the advantages and disadvantages
10. Real-World Application Scenarios - show the application of the technology in real life
11. Summary - summarize the main points and conclusions of the article
12. References/Further Reading - provide additional learning resources
```

#### Deep Research Copilot
- https://chatgpt.com/
- https://gemini.google.com
- https://claude.ai/
- https://www.genspark.ai/
- https://www.perplexity.ai/

### 2. 制作播客音频
将 上述步骤收集的资料，上传到 Google Notebook-LLM 或 elevenlanb GenFM，得到这个主题的播客内容。
- https://notebooklm.google/
- https://elevenlabs.io/app/studio?create=genfm

*注意：使用 Google NotebookLM 时可以 customize（不一定有效）：`Use a lighthearted, fun and explanatory style, audio overview should be less than 15 minutes.`*s
