# AI-NFT 元数据

创建 AI-NFT 和传统 NFT 的方式类似，**不同**之处在于增加了一个额外字段 `ai_agent`，用于描述与该 NFT 相关的 AI 代理的配置和使用的引擎，该信息存储在元数据中。

## 支持的 AI 引擎

| 引擎                            | 引擎名称 | 角色文件                                                                                                                                      |
| ------------------------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| [Eliza](https://github.com/elizaOS/eliza) 由 ElizaOS 提供 | eliza    | - [文档](https://elizaos.github.io/eliza/docs/core/characterfile/) <br> - [模板](https://github.com/elizaOS/characterfile) <br> - [示例](https://github.com/elizaOS/eliza/tree/main/characters) |

## AI-NFT 元数据 JSON

| 字段                        | 类型   | 描述                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ---------------------------- | ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **ai_agent**（新增字段）     | 对象   | <p>定义与该 NFT 关联的 AI 代理的配置。</p><ul><li><strong>engine</strong>（字符串）：用于运行 AI 代理的引擎。默认为 "eliza"。</li><li><strong>character</strong>（对象）：描述 AI 代理的角色文件 JSON。查看 <a href="https://github.com/elizaOS/characterfile?tab=readme-ov-file">此处</a>。</li></ul>                                                                                                                                                                                     |
| **name**                     | 字符串 | 资产的名称。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| **description**              | 字符串 | 资产的描述。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| **image**                    | 字符串 | 指向资产 logo 的 URI。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| **animation_url**           | 字符串 | 指向资产动画的 URI。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| **external_url**            | 字符串 | 指向定义资产的外部 URL，例如游戏的官网。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| **attributes**               | 数组   | <p>定义资产特征的属性数组。</p><ul><li><strong>trait_type</strong>（字符串）：属性的类型。</li><li><strong>value</strong>（字符串）：该属性的值。</li></ul>                                                                                                                                                                                                                                                                                                                                        |
| **properties**               | 对象   | <p>定义资产的附加属性。</p><ul><li><p><strong>files</strong>（数组）：要包含在资产中的附加文件。</p><ul><li><strong>uri</strong>（字符串）：文件的 URI。</li><li><strong>type</strong>（字符串）：文件的类型。例如 <code>image/png</code>，<code>video/mp4</code> 等。</li><li><strong>cdn</strong>（布尔值，可选）：文件是否从 CDN 提供。</li></ul></li><li><strong>category</strong>（字符串）：资产的媒体类别，例如 <code>video</code>、<code>image</code> 等。</li></ul> |

## 示例

```json
{
  // AI 代理字段
  ai_agent: {
    engine: "eliza",
    character: {
      // 代理名称
      name: "eliza",
      // 背景信息
      bio: [
        "Bio 行是每个简短的片段，可以随机组合在一起。",
        "我们发现通过随机化并选择部分 bio 内容可以增加熵。",
        "这种“熵”有助于扩展可能的输出范围，从而生成更多样但持续相关的回答。"
      ],
      lore: [
        "Lore 行是每个简短的片段，可以随机组合在一起，就像 bio 一样。",
        "然而，这些通常更具事实性或历史性，较少是传记性质的。",
        "Lore 行可以从聊天记录和推文中提取，作为角色或发生过的事情。",
        "Lore 也应该随机化并从中取样，以增加上下文的熵。"
      ],
      // ... //xxx.character.json 来自 https://github.com/elizaOS/eliza/tree/main/characters
    }
  },
  // 典型的 NFT 元数据标准
  name: 'My NFT',
  description: '这是一个在 Solana 上的 NFT',
  image: imageUri[0],
  external_url: 'https://example.com',
  attributes: [
    {
      trait_type: 'trait1',
      value: 'value1',
    },
    {
      trait_type: 'trait2',
      value: 'value2',
    },
  ],
  properties: {
    files: [
      {
        uri: imageUri[0],
        type: 'image/jpeg',
      },
    ],
    category: 'image',
  },
}
