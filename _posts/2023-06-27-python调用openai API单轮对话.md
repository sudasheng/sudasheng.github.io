---
layout: mypost
title: python调用openai API单轮对话
categories: [python]
---

### 安装和/或升级到最新版本的 OpenAI Python 库
```bash
pip install --upgrade openai
```
### chat API 调用示例
```python
import openai
# chatgpt-key，示例为无效key
openai.api_key = "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"
# 可选-添加代理，clash默认端口7890
import os
os.environ["HTTP_PROXY"] = "http://127.0.0.1:7890"
os.environ["HTTPS_PROXY"] = "http://127.0.0.1:7890"
# 示例 OpenAI Python 库请求
response = openai.ChatCompletion.create(
    model="gpt-3.5-turbo",
    messages=[
        {"role": "system", "content": "You are a helpful assistant."},
        {"role": "user", "content": "Knock knock."},
        {"role": "assistant", "content": "Who's there?"},
        {"role": "user", "content": "Orange."},
    ],
    temperature=0,
)
# 提取回复
print(response['choices'][0]['message']['content'])
```
### 如何pua模型
```python
response = openai.ChatCompletion.create(
    model=MODEL,
    messages=[
        {"role": "system", "content": "你是个简洁的助手。你的回答简明扼要，切中要害而不是详细阐述。"},
        {"role": "user", "content": "你能解释一下分数是怎么算的吗?"},
    ],
    temperature=0,
)

print(response["choices"][0]["message"]["content"])
```
### 少样本提示，伪造对话让模型更容易回答出想要的结果
```python
response = openai.ChatCompletion.create(
    model=MODEL,
    messages=[
        {"role": "system", "content": "你是一个乐于助人、遵循规则的助手。"},
        {"role": "user", "content": "帮我把下面的企业术语翻译成通俗易懂的英语。"},
        {"role": "assistant", "content": "当然，我很乐意!"},
        {"role": "user", "content": "新的协同效应将有助于推动营收增长。"},
        {"role": "assistant", "content": "物事相互协调配合将增加收入。"},
        {"role": "user", "content": "我们在有更多空闲时间时再回头，探讨增加杠杆的机会。"},
        {"role": "assistant", "content": "我们在忙碌程度较低时再讨论如何做得更好。"},
        {"role": "user", "content": "这次的战略转变意味着我们没有时间为客户交付的成果做全面而彻底的准备。"},
    ],
    temperature=0,
)

print(response["choices"][0]["message"]["content"])
```
### 计算tokens数量