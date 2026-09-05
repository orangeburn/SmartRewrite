# SmartRewrite

SmartRewrite 是一个以正式文章为原始母稿、面向不同使用场景进行独立转写的文稿重建框架。

## 总纲

**任何场景转写都必须回到原始母稿，不允许以其他 Renderer 的输出作为输入源。**

所有 Renderer 都直接读取原始母稿，并彼此平级：

```text
原始母稿
├── TTS Renderer
├── Speech Renderer
└── 其他场景 Renderer
```

每个 Renderer 只负责解决自己的表达场景问题。不同 Renderer 可以重排信息、改变句法和交付形态，但都必须直接回溯到原始母稿。

## 工作模型

SmartRewrite 分为两层：

1. **Core**：定义所有 Renderer 共用的内容来源、Fidelity Contract、概念锚词、内容单元、依赖关系和回溯验收。
2. **Renderers**：根据具体使用场景，独立完成文稿重建。

当前 Renderer：

- **TTS Renderer**：把正式文章转写为适合连续收听、人工朗读和 TTS 的完整口播稿。
- **Speech Renderer**：把正式文章重建为适合真人演讲、播客录制和提词器使用的 Speech 稿。

## 目录结构

```text
SmartRewrite/
├── README.md
├── LICENSE
├── core/
│   └── principles.md
└── renderers/
    ├── tts/
    │   ├── SKILL.md
    │   ├── references/
    │   └── agents/
    └── speech/
        ├── README.md
        ├── SKILL.md
        └── agents/
```

## Core

`core/principles.md` 定义所有 Renderer 共用的总纲、内容边界、重建基础和回溯标准。

## TTS Renderer

TTS Renderer 的目标是：**表达已经完成，声音负责执行。**

它重点处理完整口播措辞、聊天式重建、口语句法和 Audio Delivery。

完整规则见 [`renderers/tts/SKILL.md`](./renderers/tts/SKILL.md)。

## Speech Renderer

Speech Renderer 的目标是：**信息已经完成，真人负责最后表达。**

它把 Core 内容重建为一条由最小充分表达单元组成的连续演讲路径，最终文稿可以直接进入提词器使用，同时允许演讲者自然改变措辞、语序和局部连接。

完整规则见 [`renderers/speech/SKILL.md`](./renderers/speech/SKILL.md)。

## 使用方式

调用时提供：

- 原始母稿完整正文；
- 目标 Renderer；
- 时长、字数、语速、受众等场景约束，如有；
- 必须保留、删除或调整的内容，如有。

默认只输出目标场景成稿，不输出内部分析、重排方案和检查过程。

SmartRewrite 的目标，是让同一份已经成立的内容，在不同表达场景里继续成立。