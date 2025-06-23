---
title: MCP(Model Context Protocol) 入门指南
date: 2025-05-23
tags:
  - writing
  - modelcontextprotocol
  - MCP
  - reference
draft: false
---

-  What：什么是 MCP ？
	- **一句话解释**：MCP（Model Context Protocol）是一个为大语言模型（LLM）提供数据和工具上下文的开放标准协议，使开发者能够在他们的数据源和 AI 驱动的应用之间建立安全的双向连接，使应用可以以标准化方式将外部资源和功能暴露给 AI 使用。
	-  **MCP 架构**
	    ![[mcp-architecture.excalidraw|800]]
	    - *Host*：指运行大语言模型（LLM）应用的程序，如 Chat APP(Claude Desktop) 或 IDE(Windsurf, Cursor) 等，它们通过负责管理 MCP Client 与 MCP Server 的连接并使用 Server 提供的资源和工具。
	    - *MCP Client*：是与 MCP 服务器保持 1:1 连接的客户端，通常是运行在 AI 应用中的客户端，它们通过 MCP 协议与服务器进行通信并获取数据、执行工具等。
	    - *MCP Server*：是通过 MCP 协议向客户端提供数据(resource)、工具(tool) 或 prompts  的服务器，将 Client 会将接收到的这些信息供 LLM 使用。
	    - *Local Resource or Database*：指本地的数据源，如计算机上的文件、数据库或服务等，MCP 服务器可以访问这些数据源并通过协议暴露给客户端。
	    - *Remote Services*：是指通过互联网提供的远程服务，例如第三方 API 服务，MCP 服务器可以连接到这些远程服务并将其集成到 AI 应用中
	- **MCP Workflow**
	  ![](https://futurelog-1251943639.cos.accelerate.myqcloud.com/img/20250528215148.png)
-  Why：为什么需要 MCP ？
	- 传统 API 的 MxN 问题：M 个不同 AI 应用，如果要接入 N 个不同的API，需要进行 MxN 次接入集成工作，接口碎片化，开发较低效。-- 思考：OpenAPI 也定义了 Restful API 规范？OpenAPI 只是定义 API 描述规范，并没有定义通信协议规范。
	- Function Call 的问题：本质上也是工具调用，但通常是一次性调用、无双向长连接通信。
	- **协议标准化**：个人觉得这是解决现有问题的关键，协议标准化后，开发者无需为每个工具或数据源单独构建连接，可以简化集成，引入新的工具或数据源，只要它们遵循MCP标准，就可以轻松地集成到现有系统中；通过遵循相同的协议，也可以确保不同的应用程序和服务能够无缝地进行交互。
	-  可以把 MCP 的协议标准化 类比作 USB Type-C 的出现。
		- Before MCP：
		  ![](https://futurelog-1251943639.cos.accelerate.myqcloud.com/img/20250528211822.png)
		- After MCP:
		  ![](https://futurelog-1251943639.cos.accelerate.myqcloud.com/img/20250528214539.png)
		- ![](https://futurelog-1251943639.cos.accelerate.myqcloud.com/img/20250528214929.png)
- How：如何实现和使用 MCP ？
	- 示例 1：日常应用 - 使用 Chat App(Claude Desktop App), IDE(Windsurf) 实现 MCP 工具调用。
	- 示例 2：代码实践 - 实现 MCP Client 和 MCP Server。
	- 示例 3：代码实践 - 基于 Agent 框架实现 MCP 工具调用。
- Summary
	- 优点：
		- **标准化了工具调用协议**：标准化了 LLM 与外部工具的交互方式，让 LLM 能够与遵循这个协议的各种外部工具顺畅交互通信，无需额外集成成本。
		- **面向 LLM 的工具或服务设计**：当前的 SaaS 基本都是让用户通过前端 UI 界面来使用相关能力，未来如果用户都是通过 LLM 来使用 SaaS 能力，那么需要不同的能力开放使用方式，MCP 是目前针对这个问题的解决方案。-- 未来还会有其他的吗？
	- 挑战：
		- 目前 LLM 对与工具调用的规划能力还存在不足，复杂任务还需要通过编写代码来组织工作流。
			- 笔者在 Windsurf IDE 以及 Claude Desktop App 中配置了多个 MCP 工具，针对简单问题（只需要依次调用一两个工具）处理相对还可以，但针对需要规划多个工具协作的场景，大部分情况处理效果都较差。还是需要通过编写代码还组织工作流，从而保障有确定性的执行过程和执行结果。
			- 笔者也通过基于 Agent 框架编写代码测试了 Qwen3 14b 等小尺寸开源模型对 MCP 工具的调用能力和指令遵循能力，在复杂任务上效果较差，并且测试的 OpenAI Agent SDK 框架 和 HuggingFace Smolagent  框架在调用 MCP 工具上也存在问题。-- 待测试其他 Agent 框架？
		- 目前较多 MCP Server 服务不稳定，对于 MCP Server 服务提供方相当于在原有功能或服务提供方式的基础上，额外增加了工作负担，并且可能和平台的当前利益有冲突。
			- 比如百度地图，目前用户通过在他的 App 来使用位置服务能力，能为平台提供广告收益。换成 MCP 工具调用，就只有基于调用次数的收费了。这些平台型公司基于隐私合规以及自身利益考虑，是否有意愿有动力开放相关能力？目前大部分服务提供方都是跟风上了MCP，后续的持续维护完善以及商业模式还有较大挑战。
- 参考
	- [Model Context Protocol Official Documents](https://modelcontextprotocol.io/introduction)
	- [Model Context Protocol (MCP): Landscape, Security Threats, and Future Research Directions](https://arxiv.org/pdf/2503.23278)
	- [Building Agents with Model Context Protocol - Full Workshop with Mahesh Murag of Anthropic](https://www.youtube.com/watch?v=kQmXtrmQ5Zg&ab_channel=AIEngineer)
	- [OpenAI Agents SDK](https://openai.github.io/openai-agents-python/)
	- [Huggingface Smolagents](https://github.com/huggingface/smolagents)
	- [MCP Servers Indexes](https://mcp.so/)

