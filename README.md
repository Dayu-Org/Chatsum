# Chatsum
Take Chat as the entry point, to enable LLM to the whole process of daily Workflow.

## 关于`data`目录下多人多轮对话Summary数据说明
1. 主要基于[NaturalConv](https://arxiv.org/abs/2103.02548)数据+GPT生成
2. NaturalConv是两人多轮对话，每个dialog大概10轮（每人交替10句chat），共20句chat左右，内容涉及6个领域
3. 构建Pipeline
    1. 将相邻几组dialog合并，模拟2-6人对话场景，同时保证dialog内chat的顺序不变
    2. 将所有chat以30-50轮chunk成chat group（大概对应4k Context Window训练）或100轮的chat group（对应8k Context Window）
    3. 封装成Alpaca的格式：其中`input`为`"".join(["<|im_start|>{}<|im_end|>\n".format(chat) for chat in chat_group])`
    4. `Output`主要有GPT生成（3.5或4），整体质量高
