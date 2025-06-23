---
author: wallezen
date: 2024-01-01
title: OpenAI 官方提示工程指南（译）
description: 本指南介绍了从与 GPT-4 等大语言模型的交互中获得更好结果的六大策略以及相关的具体措施，在实际应用过程中，组合使用这些策略通常可以取得更好的效果。因此，我们鼓励你多试验尝试，探索适合你的应用场景的使用方法。
tags:
  - prompt engineering
  - openai
thumbnail: https://futurelog-1251943639.cos.accelerate.myqcloud.com/img/202401011111839.png
draft: false
---

*原文地址：https://platform.openai.com/docs/guides/prompt-engineering*


## 一、 TL;DR：获得更好结果的六大策略
### 1.1 策略一：编写清晰的指示
 如果不能给出清晰的指示，大语言模型并不能清楚地知道你想要什么。如果模型的输出太长了，就请要求简短答复；如果输出太简单，就请要求专家级别的详细回复；如果输出的格式不是所希望的，就请您给出希望看到的格式的示例。总之，越少让模型去猜测你想要什么，你得到所希望的结果的可能性就越大。

具体措施：
 - [在您的查询中包含详细信息以获得更相关的答案]()
 - [角色扮演]()
 - [使用分隔符清楚地指示输入的不同部分]()
 - [指定完成任务所需的步骤]()
 - [提供示例]()
 - [指定输出长度]()

### 1.2 策略二：提供参考资料
大语言模型存在“幻觉”问题，所以它可能会自信地编造不存在的信息。特别是当被问及深奥的主题或引文和 URL 时。就像一张笔记可以帮助学生在考试中取得更好的成绩一样，为这些模型提供参考资料可以帮助减少“幻觉”问题。

具体措施：
- [指示模型使用参考资料回答]()
- [指示模型通过引用参考资料来回答]()

### 1.3 策略三：将复杂的任务拆分为更简单的子任务
正如在软件工程中，为了降低系统的复杂性，保障系统的可用性可靠性可维护性，通常会将复杂系统分解为模块化的组件。同理，提交给大语言模型的单次任务也最好别太复杂，因为复杂的任务往往比简单的任务具有更高的出错概率。复杂的任务通常可以被重新定义为由更简单任务串接起来的工作流，前面任务的输出作为后续任务的输入。

具体措施：
- [使用意图分类来识别与用户查询最相关的指令]()
- [对于需要很长对话的对话应用，总结或过滤以前的对话]()
- [分段总结长文档并递归构建完整摘要]()

### 1.4 策略四：给大语言模型多点“思考时间”
如果要求计算 17 乘以 28，您可能不会立即知道结果，但随着多给点时间，您肯定可以算出来。同样，相比于多花点时间逐步找出答案，大语言模型在尝试立即回答问题时通常会犯更多的错误。通过“ chain of thought 思路链”等措施，可以帮助模型更可靠地推理出正确答案。

具体措施：
- [指示模型在急于得出结论之前找出自己的解决方案]()
- [使用内心独白或一系列查询来隐藏模型的推理过程]()
- [询问模型在之前的过程中是否遗漏了任何内容]()

### 1.5  策略五：使用外部工具
通过向模型提供其他工具的输出来弥补模型的弱点。例如，文本检索系统（有时称为 RAG 或检索增强生成）可以告诉模型相关文档。像 OpenAI 的代码解释器这样的代码执行引擎可以帮助模型进行数学运算并运行代码。如果一项任务可以通过工具而不是语言模型更可靠或更有效地完成，那么就可以结合工具和模型，充分利用两者的能力。

具体措施：
- [使用基于嵌入的搜索实现高效的知识检索]()
- [使用代码执行来执行更准确的计算或调用外部API]()
- [授予模型访问特定功能的权限]()

### 1.6 策略六：系统地进行变更测试
如果您可以衡量性能，那么提高性能就会更容易。在某些情况下，对提示的修改将在一些孤立的示例上实现更好的性能，但会导致在一组更具代表性的示例上整体性能变差。因此，为了确保更改对性能产生净积极影响，可能有必要定义一个全面的测试套件（也可以称为“评估”）。

具体措施：
- [参考“黄金标准答案”评估模型输出]()


## 二、具体措施
### 2.1 策略一：编写清晰的指示
#### 2.1.1 在您的查询提问中包含详细信息以获得更相关的答案
为了获得高度相关的回答，需要确保提问中提供了重要的详细信息或上下文信息。不然模型只能猜测你具体想要什么。

| Worse                                           | Better                                                                                                                                                                                                      |
| ----------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| How do I add numbers in Excel?                  | How do I add up a row of dollar amounts in Excel? I want to do this automatically for a whole sheet of rows with all the totals ending up on the right in a column called "Total".                          |
| Who’s president?                                | Who was the president of Mexico in 2021, and how frequently are elections held?                                                                                                                             |
| Write code to calculate the Fibonacci sequence. | Write a TypeScript function to efficiently calculate the Fibonacci sequence. Comment the code liberally to explain what each piece does and why it's written that way.                                      |
| Summarize the meeting notes.                    | Summarize the meeting notes in a single paragraph. Then write a markdown list of the speakers and each of their key points. Finally, list the next steps or action items suggested by the speakers, if any. |
#### 2.1.2 角色扮演
OpenAI 的 “System Message”选项可以用于指定模型作为一个什么样的角色来回答问题。

| Role   | Text                                                                                                                                                                |
| ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| SYSTEM | When I ask for help to write something, you will reply with a document that contains at least one joke or playful comment in every paragraph.                       |
| USER   | Write a thank you note to my steel bolt vendor for getting the delivery in on time and in short notice. This made it possible for us to deliver an important order. |
#### 2.1.3 使用分隔符清楚地指示输入的不同部分
分割符（如 """, XML 标记，标题 等）可以帮助区分 Prompt 中起不同作用的部分。
- 示例 1

| Role | Text                                                                                       |
| ---- | ------------------------------------------------------------------------------------------ |
| USER | Summarize the text delimited by triple quotes with a haiku. <br><br>"""insert text here""" |
- 示例 2

| Role   | Text                                                                                                                                                                                                             |
| ------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| SYSTEM | You will be provided with a pair of articles (delimited with XML tags) about the same topic. First summarize the arguments of each article. Then indicate which of them makes a better argument and explain why. |
| USER   | \<article> insert first article here \</article><br> <br>\<article> insert second article here \</article>                                                                                                       |
- 示例 3

| Role   | Text                                                                                                                                                                                                                                                         |
| ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| SYSTEM | You will be provided with a thesis abstract and a suggested title for it. The thesis title should give the reader a good idea of the topic of the thesis but should also be eye-catching. If the title does not meet these criteria, suggest 5 alternatives. |
| USER   | Abstract: insert abstract here <br><br>Title: insert title here                                                                                                                                                                                              |
对于上述较为直观的任务，使用分隔符可能提现不出明显的结果质量差异。但是，对于约复杂的任务，使用分隔符区分 Prompt 中的不同部分就越重要。这里的关键就在于不要让模型费力去理解你需要它完成的任务。

#### 2.1.4 指定完成任务所需的步骤
