# dsh-light-preset

DeepSeek Harness 的轻量 agent 预设（模式 id：`light`，显示名 Light）。

面向日常本地编码与接口调试：保留文件、命令、技能、计划、压缩与 Office 工具，去掉子代理、工作流、日程和历史目标。

## 包含内容

- 指令与上下文：`persona`、`agent-instructions`（AGENTS.md）、`time-context`
- 文件与命令：`read` `write` `edit` `read_image` `glob` `grep` `pwsh`（非 Windows 为 `bash`）、`job_*`
- 技能：`skill` + `skill-filesystem`（不加载内置技能目录，只读项目/用户技能）
- 计划与上下文：`exit_plan_mode`、自动压缩、`/compact`
- 交互：`ask_user_question`、`todo_write`、`web_search`/`web_fetch`、`present`
- Office：`tool-office`（仅在加载 office 技能后出现）

不包含：`subagent`/`subagent_fork`/`send_message`/`list_agents`/`interrupt_agent`、`workflow`、`schedule_*`、`create_goal`/`get_goal`/`update_goal`。

## 兼容性

- 需要 DSH `>= 0.2.2-rc.2`（`engines.dsh`）。
- DSH 0.2.1 及更早版本没有 `@deepseek-ai/dsh-tool-office` 与 `officeKit` 服务，安装会被兼容性检查拒绝。
- 预设 id 为 `light`：如果 profile 里已有同名预设，声明加载会失败，请先移除旧 preset。

## 安装

通过 DSH 的插件管理器安装（Plugins 页面，或让 agent 调用 `plugin_manager`）：

```text
plugin_manager install_bundle target=github:zhonghes/dsh-light-preset#v1.0.0
```

安装后新建会话，在模式列表里选择「Light」。已有会话保持原模式，不会自动切换。

## 说明

- 内置技能目录（`$DSH_BUNDLED_SKILL_DIR`）不加载；宿主挂载的技能（如 office 系列、Windows 沙箱诊断）仍会出现在技能列表里，这是宿主行为，预设无法移除。
- Office 三个工具（`office_render`、`office_convert`、`office_recalculate`）在加载任意 office 技能后才出现，未加载时不占工具 schema。

## License

MIT
