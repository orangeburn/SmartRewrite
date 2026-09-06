# Speech Renderer

Speech Renderer 用于把原始母稿重建为适合真人表达的 Speech 稿。

核心目标：

**信息已经完成，真人负责最后表达。**

Speech Renderer 先建立共用的演讲路径和最小充分表达单元，再根据场景选择输出模式。

## 输出模式

### Teleprompter Mode

默认模式。

适合播客、视频录制、提词器和需要稳定连续表达的场景。

控制的是：

**这一刻完整要表达什么。**

完整规则见 [`modes/teleprompter.md`](./modes/teleprompter.md)。

### Stage Mode

适合上台演讲、分享会、纸稿或平板辅助演讲，以及需要更大现场演绎空间的场景。

控制的是：

**接下来这一小段需要把什么事情讲明白。**

Stage Mode 通过最小充分演讲块把结构和记忆负担外置到讲稿，让演讲者用眼睛触发表达。

完整规则见 [`modes/stage.md`](./modes/stage.md)。

## 共用规则

Speech Renderer 必须执行双向语义覆盖检查：

- Output → Source：不得新增母稿不存在的命题和关系；
- Source → Output：不得遗漏母稿有效语义。

完整规则见 [`references/semantic-coverage.md`](./references/semantic-coverage.md)。

总入口见 [`SKILL.md`](./SKILL.md)。

Speech Renderer 必须遵守 [`../../core/principles.md`](../../core/principles.md)。
