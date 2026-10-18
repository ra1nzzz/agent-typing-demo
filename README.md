# Agent 打字机

STEPX Neo 上的最小演示：Agent 向 `demo_inbox.txt` 写入文本，App 逐字显示，用户可实时看到“Agent 在输入”。

## 下载

见 Releases 中的 `AgentTypeDemo-1.1.0.apk`。

## 应用信息

| 项 | 值 |
| --- | --- |
| 应用名 | Agent 打字机 |
| 包名 | com.stepx.typedemo |
| 版本 | 1.1.0 (versionCode 2) |
| minSdk / targetSdk | 23 / 34 |
| 体积 | 约 21 KB |
| 权限 | 无 |

## 双向对话（1.1.0）

- 下方输入框写内容，点「发送」→ 追加到 `outbox.txt`
- Agent 读取 `outbox.txt`，把回复写入 `inbox.txt`
- App 轮询 `inbox.txt`，新消息逐字打出

文件格式：`inbox.txt` 首行 `#序号`，其余为正文；`outbox.txt` 每行 `序号|时间|内容`。

## 原理

1. App 首次启动时在自己外部目录创建 `demo_inbox.txt`：
   `/sdcard/Android/data/com.stepx.typedemo/files/demo_inbox.txt`
2. App 每 150ms 轮询该文件；内容变化时，把与已显示文本的差量逐字打出（长文本自动加速）。
3. Agent 只负责写文件，不触碰 UI，因此不需要无障碍、不需要模拟点击。

## 使用

1. 安装并打开 App；
2. 由端侧写入 `demo_inbox.txt`；
3. 返回 App 即可看到逐字输入过程。

清空文件内容，画面会从空白重新开始。
