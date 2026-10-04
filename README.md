# 公众号素材库目录

把自己公众号后台**当前可见**的素材快速整理成有来源的目录草稿。输入是你指定的浏览器环境、本人素材库页面和主题条件；结果是最多 20 条素材的名称、类型、主题、当前可见日期、使用待办，以及缺项与覆盖范围说明。仅当登录、验证码、风控、权限不足或所有权不明时停止；历史内容未显示时仍交付当前可见素材，并把历史范围列为缺项，不会假称完成全库盘点。

![公众号素材库目录推广图](assets/promo.png)

## 安装

```bash
npx skills add xxjrq/wechat-materials-index-free
```

这是浏览器 Skill，需先安装 Easy WebBridge： [GitHub 主下载](https://github.com/xxjrq/easy-webbridge) ｜ [Gitee 备用下载](https://gitee.com/xxjrq/easy-webbridge)。运行时由你提供 browserId；Skill 每个任务只管理自己的 session/标签组，不触碰已有页面或其他账号。

## 输入与交付

输入：`browserId`、本人素材库页面、可选主题条件；单次最多读取 20 个可见素材。输出为 Markdown 草稿，含每条页面来源和“仅当前可见内容”的范围声明。默认只读；即使授权填充草稿，也绝不点击发布或发送。

## 安全边界

只读取网页可见内容。遇到登录、验证码、风控、权限不足或所有权不明立即停止；分页或历史不可见内容明确列为缺项。离线样例在 `fixtures/`，用于验证格式，不代表真实在线采集。

## 自检

```bash
bash scripts/self-test.sh
```

## 来源与许可

业务用途参考 [OpenCLI](https://github.com/jackwener/OpenCLI) 及其 [微信浏览器适配说明](https://github.com/jackwener/OpenCLI/blob/main/docs/adapters/browser/weixin.md)；本仓库为原创工作流说明，未复制其实现。仓库采用 [MIT License](LICENSE)。

## 离线样例

[成功资料](fixtures/success-visible-materials.json)和[登录阻断资料](fixtures/failure-login-required.json)与原 visible-materials.json/login-required.json 逐字一致，仅提供明确的成功/失败文件名。自检验证资料字段与停止合同，不代表已在线采集素材，也不证明登录成功。
