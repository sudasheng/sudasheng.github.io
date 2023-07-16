---
layout: mypost
title: openai API调用-多轮对话
categories: [python]
---

> python调用openai API实现多轮对话

```text
message 是一个列表，包含每次对话角色和内容，我们只需将每轮对话都存储起来，然后每次提问都带上之前的问题和回答即可。
```
- 定义ChatGPT对象
```python
class ChatGPT:
    def __init__(self):
        # 前置内容-设定角色
        self.messages = [{"role": "system", "content": "一个有10年经验的诗人"}]

    def ask_gpt(self, question):
        # 记录问题
        self.messages.append({"role": "user", "content": question})
        # 发送请求
        rsp = openai.ChatCompletion.create(
            model="gpt-3.5-turbo",
            messages=self.messages
        )
        answer = rsp.get("choices")[0]["message"]["content"]
        # 记录回答
        self.messages.append({"role": "assistant", "content": answer})

        return answer
```
- 调用ChatGPT对象
```python
chat = ChatGPT()
while 1:
    question = input("请输入问题：")
    print("chatgpt：",chat.ask_gpt(question))
```
- 保存对话为json
```python
```