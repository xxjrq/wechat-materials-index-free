# WeChat Material Library Index

Create a sourced Markdown inventory from the currently visible items in your own WeChat Official Account material library. Provide a user-selected browser environment, the library page, and an optional theme filter; receive up to 20 visible items with name, type, theme, visible date, follow-up, source, and explicit gaps.

![Promo](assets/promo.png)

## Install

```bash
npx skills add xxjrq/wechat-materials-index-free
```

This browser skill requires Easy WebBridge: [GitHub](https://github.com/xxjrq/easy-webbridge) or [Gitee mirror](https://gitee.com/xxjrq/easy-webbridge). The user supplies a browserId. One task uses only its own session/tab group and never takes over existing pages or other accounts.

It is read-only by default. Login, CAPTCHA, risk control, insufficient permission, or unclear ownership stops the run. Non-visible history is recorded as a gap while the currently visible materials are still delivered; visible results are never represented as a complete historical inventory. Offline simulated fixtures are included for format validation only.

Run `bash scripts/self-test.sh` for the repository self-test.

## Offline fixtures

[Success data](fixtures/success-visible-materials.json) and [login-blocked data](fixtures/failure-login-required.json) are unchanged copies of the original fixture files, under explicit success/failure filenames. The self-test checks input fields and the stop contract; it does not prove live collection or login success.
