---
name: wechat-materials-index-free
description: 在用户指定的 Easy WebBridge 浏览器会话中，只读整理本人公众号素材库当前可见内容：按主题筛选并最多提取20条名称、类型、可见日期与使用待办，交付带逐条页面来源和缺项说明的 Markdown 草稿。适用于一次性盘点已授权页面；登录、验证码、风控、权限不足或所有权不明时停止，历史内容未显示时作为缺项保留，不把可见清单说成完整历史盘点。
---

# 公众号素材库目录

把当前看得见的公众号素材，整理成可继续编辑的目录草稿；它不猜测隐藏历史，也不替你发布。

## 输入

- `browserId`：用户明确指定的 Easy WebBridge 浏览器环境。
- 本人已打开或可进入的素材库页面；可附 `theme` 主题条件。
- 可选：`draft_fill_authorized: true`，仅允许填写草稿，绝不点击发布或发送。

## 结果

返回不超过 20 条可见素材，每条含素材名称、类型、主题、当前可见日期、使用待办和页面来源；另列筛选条件、采集时间、缺项及范围限制。表格超过 100 行或页面内容超出单次范围时，要求分批处理。

## 前置依赖

这是浏览器 Skill。先安装并登录 **Easy WebBridge**：

- GitHub 主下载：<https://github.com/xxjrq/easy-webbridge>
- Gitee 备用下载：<https://gitee.com/xxjrq/easy-webbridge>

运行前通过用户给出的 `browserId` 选择唯一 EasyBR 环境；一项任务只创建、使用自己的 session/标签组，不广播到其他账号、不接管或关闭已有页面。使用安装目录中的 CLI 入口 `/path/to/easy-webbridge/cli/easy-webbridge.mjs`（将 `/path/to/easy-webbridge` 替换为用户的安装目录），不要另造浏览器 API。

```bash
# 先核对本机已安装 CLI 的实际命令；不在公开记录中写入 browserId 或 session 值。
node /path/to/easy-webbridge/cli/easy-webbridge.mjs --help

# 以用户提供的 browserId 创建本任务自有标签组；<run-id> 是本次临时值。
node /path/to/easy-webbridge/cli/easy-webbridge.mjs navigate <browserId> <material-library-url> \
  --new-tab --session wechat-materials-index-free-<run-id> --group-title "公众号素材盘点"

# 读取当前任务页的可见文本；每次导航、筛选或滚动后立即重新快照并刷新 refs。
node /path/to/easy-webbridge/cli/easy-webbridge.mjs snapshot <browserId> <tabId> \
  --visibility visible --text-mode page
```

后续步骤始终复用同一 `browserId`、session 和标签组；只在确有并行对照需要时增加同组标签页。结束时仅可关闭本任务创建且已核对所有权的 session，绝不关闭用户原有页面或其他任务组。

## 执行边界

1. 先确认页面属于用户本人且可见；默认只读。登录页、验证码、风控、权限不足或所有权不明时停止，说明原因，不绕过。
2. 在自己的标签组中打开素材库并快照可见网页内容；按主题条件筛选。只读取页面上可见字段，最多 20 条。
3. 每条记录保留来源（页面标题、可见位置或可复访 URL）与未显示字段。不可见历史素材只写入缺项，绝不声称已完整盘点。
4. 输出 Markdown 草稿。即使获得草稿填充授权，也只填写草稿，不点击最终“发布”“发送”等不可逆按钮。

## 输出模板

```markdown
# 素材库目录草稿
范围：当前可见素材库｜主题：<主题或未限定>｜采集：<当前日期>

| 素材名称 | 类型 | 主题 | 当前可见日期 | 使用待办 | 来源 |
| --- | --- | --- | --- | --- | --- |
| … | … | … | … | … | 素材库页面：<可见位置/URL> |

## 缺项与限制
- 仅覆盖本次页面当前可见的 <n>/20 条；历史或分页未显示内容未盘点。
- <登录、权限、字段缺失或筛选限制>
```

离线格式验证可运行 `bash scripts/self-test.sh`。`fixtures/` 是离线页面资料模拟，绝非在线采集记录。
