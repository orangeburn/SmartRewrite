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

1. **Core**：定义所有 Renderer 共用的内容边界、忠实原则和输入约束。
2. **Renderers**：根据具体使用场景，独立完成文稿重建。

当前 Renderer：

- **TTS Renderer**：把正式文章转写为适合连续收听、人工朗读和 TTS 的完整口播稿。
- **Speech Renderer**：面向真人演讲场景。规则正在定义中。

未来可以继续扩展其他 Renderer，但都必须遵守同一套 Core 约束。

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
        └── README.md
```

## Core

`core/principles.md` 存放所有 Renderer 共用的总纲和内容边界。

Renderer 不得自行覆盖 Core 规则。场景规则只处理该场景如何表达，不重新定义母稿、忠实对象或跨 Renderer 的关系。

## TTS Renderer

现有 `article-to-spoken-script` 能力迁移为 `renderers/tts`。

它负责把正式文章重建成适合播客、旁白、人工朗读或 TTS 的完整口播稿，重点处理：

- Content Fidelity
- Conversational Reconstruction
- Spoken Syntax Reconstruction
- Audio Delivery

完整规则见 [`renderers/tts/SKILL.md`](./renderers/tts/SKILL.md)。

## Speech Renderer

`renderers/speech` 用于开发真人演讲场景的转写规则。

当前已确定的形态是：

- 可直接进入提词器使用；
- 每个表达单元包含必要信息；
- 不依赖临场组织大段内容；
- 具体规则继续独立定义。

## 使用方式

调用时应同时提供：

- 原始母稿完整正文；
- 目标 Renderer；
- 时长、字数、语速、受众等场景约束，如有；
- 必须保留、删除或调整的内容，如有。

默认只输出目标场景成稿，不输出内部分析、重排方案和检查过程。

SmartRewrite 的目标，是让同一份已经成立的内容，在不同表达场景里继续成立。