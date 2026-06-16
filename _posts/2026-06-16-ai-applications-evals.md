---
layout: post
title: AI应用评测
slug: ai-applications-evals
date: 2026-06-16
---
这篇笔记基于下列资料：
[Evals faq](https://hamel.dev/blog/posts/evals-faq/)
[Your AI product needs evals](https://hamel.dev/blog/posts/evals/index.html)
[Using LLM-as-a-judge for evaluation: a complete guide](https://hamel.dev/blog/posts/llm-judge/index.html)

处理（AI应用）问题有三个步骤：评测、调试、改变模型行为或系统。评测是第一步。

评测的重心是通过查看模型的原始输出、工具调用轨迹来发现真实存在的问题。如果是开发阶段，可以合成数据进行评测。合成数据集/实际数据集需要包括的维度有产品的功能、场景、用户需求和特征。可以采取模型（llm-as-a-judge）和人类评测。为了减少查看数据的干扰，可以做/定制一个模型输出的查看器；模型和人类都对模型输出进行详细评论和打分，可以对比意见；二元打分（e.g. 通过/失败）好于分数评分（详细评论可以弥补二元打分信息/区分度不够的问题）；积累部分评估意见后可以对错误例子进行归类，可以利用模型对未评估的例子进行自动归类。

其他的评测方式还有单元测试和A/B测试。单元测试适合有明确可以衡量的输出的任务（e.g. 需要根据输入创建一个联系人）；需要定期进行。评测需要进行成本评估。资料里还提到了很多操作细节，如谁来执行错例评估（专家/工程师/外包），可以先大致了解。
