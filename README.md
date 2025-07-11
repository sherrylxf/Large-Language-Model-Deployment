# 大语言模型部署体验项目

本项目旨在探索多种主流大语言模型的本地部署过程，并进行统一问答测试与横向性能对比，帮助理解不同模型的风格、响应速度和推理能力差异。

---

## 本项目部署的三个模型：

| 序号 | 模型名称              | 来源 / 获取方式                                                                | 部署说明            |
|----| ----------------- | ------------------------------------------------------------------------ | --------------- |
| 1  | Qwen-7B-Chat      | `git clone https://www.modelscope.cn/qwen/Qwen-7B-Chat.git`              | 魔搭 CPU 部署完成     |
| 2  | ChatGLM3-6B       | `git clone https://www.modelscope.cn/ZhipuAI/chatglm3-6b.git`            | 魔搭 CPU 部署完成    
| 3  | ChatGPT-4o        | 在线使用（[https://chat.openai.com/）](https://chat.openai.com/）)              | 免部署，网页交互即可      |

---

## 部署过程（详细部署教程见：[Tutorial.md](模型部署教程)）

> 以下为各模型的部署或运行截图：

### 模型克隆与加载

* Qwen 克隆成功
![模型部署完成.png](%E7%AC%AC%E4%B8%80%E4%B8%AA%E6%A8%A1%E5%9E%8B%E2%80%94%E9%80%9A%E4%B9%89%E5%8D%83%E9%97%AE/%E6%A8%A1%E5%9E%8B%E9%83%A8%E7%BD%B2%E5%AE%8C%E6%88%90.png)

* ChatGLM3 克隆成功
![模型部署完成.png](%E7%AC%AC%E4%BA%8C%E4%B8%AA%E6%A8%A1%E5%9E%8B%E2%80%94ChatGLM3/%E6%A8%A1%E5%9E%8B%E9%83%A8%E7%BD%B2%E5%AE%8C%E6%88%90.png)


### 本地运行与输出示例

* Qwen 输出示例
![问题1.png](%E7%AC%AC%E4%B8%80%E4%B8%AA%E6%A8%A1%E5%9E%8B%E2%80%94%E9%80%9A%E4%B9%89%E5%8D%83%E9%97%AE/%E9%97%AE%E9%A2%981.png)

* ChatGLM3 输出示例

![问题1.png](%E7%AC%AC%E4%BA%8C%E4%B8%AA%E6%A8%A1%E5%9E%8B%E2%80%94ChatGLM3/%E9%97%AE%E9%A2%981.png)

* ChatGPT-4o 网页回答截图

![问题1.png](%E7%AC%AC%E4%B8%89%E4%B8%AA%E6%A8%A1%E5%9E%8B%E2%80%94Chatgpt4o/%E9%97%AE%E9%A2%981.png)

---

## 问答横向对比分析（详细见文档：[大语言模型之间的横向对比分析.md](%E5%A4%A7%E8%AF%AD%E8%A8%80%E6%A8%A1%E5%9E%8B%E4%B9%8B%E9%97%B4%E7%9A%84%E6%A8%AA%E5%90%91%E5%AF%B9%E6%AF%94%E5%88%86%E6%9E%90.md)）

我们选取了一组具有代表性的问题，在3个模型上进行统一测试，分析它们在以下方面的表现：

### 统一测试问题

> **示例问题：**
> “请说出以下两句话的区别：1、冬天：能穿多少穿多少；2、夏天：能穿多少穿多少。”

### 回答效果对比表

| 模型名称             | 语言理解  | 回答逻辑  | 幽默感   | 输出流畅性 | 响应速度     | 备注           |
| ---------------- | ----- | ----- | ----- | ----- | -------- | ------------ |
| **Qwen-7B-Chat** | ★★★★☆ | ★★★★☆ | ★★★☆☆ | ★★★★☆ | 中（CPU部署） | 有中国特色表达      |
| **ChatGLM3-6B**  | ★★★☆☆ | ★★★☆☆ | ★★★☆☆ | ★★★☆☆ | 中（CPU部署） | 输出偏短，表达中规中矩  |
| **ChatGPT-4o**   | ★★★★★ | ★★★★★ | ★★★★★ | ★★★★★ | 快（云端API） | 表达自然，具有幽默与逻辑 |

---

## 鸣谢

感谢以下模型与平台支持：

* [Qwen by Alibaba](https://www.modelscope.cn/qwen/Qwen-7B-Chat)
* [ChatGLM3 by ZhipuAI](https://www.modelscope.cn/ZhipuAI/chatglm3-6b)
* [ChatGPT-4o by OpenAI](https://chat.openai.com)

---
