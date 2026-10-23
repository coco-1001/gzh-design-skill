# Repository Instructions

## 公众号排版前同步闸门

当用户要求“公众号排版”“微信排版”，或提供 `【引言】`、`【正文】`、`【说明】`、`【信息来源】` 要求排版时，在读取正式排版规则和生成 HTML 之前：

1. 先执行 `git fetch origin`，再检查当前仓库、当前分支、当前 `HEAD`、`origin/main` 和 `git status`。
2. 仅当工作区与暂存区均干净、没有本地独有提交、没有分叉，且当前 `HEAD` 只是单纯落后于 `origin/main` 时，执行 `git merge --ff-only origin/main`；已经一致时直接继续。
3. 若存在未提交或已暂存修改、本地独有提交、分叉，或 fast-forward 失败，不得执行 `reset`、强制 `checkout`、覆盖或删除文件，也不得继续排版；直接向用户报告当前 Git 状态和待处理问题。
4. 同步后必须确认当前 `HEAD` 与 `origin/main` 一致，才可继续读取规则并排版。

## 微信公众号日常排版

当用户要求“公众号排版”“微信排版”，或提供 `【引言】`、`【正文】`、`【说明】`、`【信息来源】` 要求排版时：

1. 完成上述同步闸门后，依次读取 `SKILL.md`、`AGENTS.md`、`docs/wechat-layout.md`、`references/theme-blue-white.md`。
2. 除非用户本次明确指定其他主题，否则默认使用正式主题 `蓝白色系（blue-white）`，不要再次询问主题。
3. 严格按照 `docs/wechat-layout.md` 执行；用户本次明确要求优先。
4. 不要再次询问已经固化的日常排版设置。
