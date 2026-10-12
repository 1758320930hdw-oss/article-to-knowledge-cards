# Make Knowledge Cards

`make-knowledge-cards` 是一个面向 Codex 的 Skill，用于把文章或文本文件整理成简洁、可复习的知识卡片。

## 项目解决什么问题

阅读长文章时，手动提取重点容易遗漏重要信息，也容易重复记录或加入原文没有的内容。本项目按照原文提取真正重要的知识点，每张卡片只讲一个知识点，帮助用户快速复习和自测。

## 主要功能

- 从用户粘贴的文章中提取知识点。
- 读取用户指定的本地 Markdown（`.md`）或纯文本（`.txt`）文件。
- 输出 5–8 张知识卡片；如果原文信息不足，则输出更少的卡片，不强行凑数。
- 每张卡片包含标题、核心知识、简明解释、例子或自测问题。
- 合并重复内容，优先保留概念、机制、区别、原则和结论等重要信息。
- 只使用原文能够支持的信息，不编造外部事实、例子或因果关系。
- 按原文语言或用户指定的语言输出。

当前不支持网页抓取、PDF、Anki 导出或图形界面。

## 安装方法

本项目不需要额外的 Python 或第三方依赖。将 Skill 文件夹复制到 Codex 可发现的目录：

- 用户级安装：`%USERPROFILE%\.codex\skills\make-knowledge-cards`
- 仅当前项目使用：`<项目目录>\.codex\skills\make-knowledge-cards`

Windows PowerShell 用户级安装示例：

```powershell
$target = Join-Path $HOME ".codex\skills\make-knowledge-cards"
New-Item -ItemType Directory -Force -Path (Split-Path $target) | Out-Null
Copy-Item -Recurse -Force `
  ".\skills\make-knowledge-cards" `
  $target
```

项目级安装时，将目标路径改为项目内的 `.codex\skills\make-knowledge-cards`。

## 使用方法

在 Codex 中调用：

```text
$make-knowledge-cards
```

然后粘贴文章，或提供本地 `.md` / `.txt` 文件路径。例如：

```text
$make-knowledge-cards
请处理 D:\notes\article.txt，并用中文输出。
```

## 输入输出示例

输入：

```text
番茄工作法把工作分成专注时段和休息时段。
常见做法是专注 25 分钟后休息 5 分钟。
每完成四个专注时段，可以安排一次较长休息。
```

输出：

```text
1. 标题：专注与休息交替
   核心知识：番茄工作法交替安排专注时段和休息时段。
   简明解释：工作由专注和休息两个阶段组成循环。
   例子或自测：自测：这种方法由哪两类时段组成？
   答案：专注时段和休息时段。

2. 标题：常见时段长度
   核心知识：常见安排是专注 25 分钟后休息 5 分钟。
   简明解释：文章给出了专注时段和休息时段的具体时长。
   例子或自测：例子：专注 25 分钟，休息 5 分钟。

3. 标题：较长休息的安排
   核心知识：每完成四个专注时段，可以安排一次较长休息。
   简明解释：较长休息安排在一组专注时段完成后。
   例子或自测：自测：完成几个专注时段后可以安排较长休息？
   答案：四个。

说明：原文只支持 3 个独立知识点，因此只输出 3 张，不为凑数拆分或编造。
```

其他文章同样按实际信息量决定卡片数量。
