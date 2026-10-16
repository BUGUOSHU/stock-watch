# 每日美股简报

默认跟踪 TSLA、ORCL、KLAC、LRCX、CRDO、COHR、AMKR、SOFI、PONY、SOUN、DOW、NVO。可在网页添加最多 8 只自选股（总数上限 20），新增代码会显示在行情、新闻和分享链接中；可输入 `NASDAQ:AAPL` 或 `NYSE:IBM` 指定交易所，不写交易所时默认 NASDAQ。

## 预览和新闻

本地可直接打开 `index.html` 预览页面布局、持仓清单、首报和事件倒计时。动态新闻翻译需要部署到 Vercel 并启用 AI Gateway；新闻从 Google News RSS 获取，每只股票最多显示 2 条，最多 40 条。市场报价和行业 ETF 涨跌通过 TradingView 网页组件显示。

持仓台账支持买入/卖出、股数、成交价、手续费和交易日期，按加权平均成本计算持仓及已实现盈亏。交易记录只存放在当前浏览器的 `localStorage`，不会写进分享 URL，也不会发送到新闻 API；更换浏览器或清除站点数据后记录不会自动迁移。

## 部署

将项目根目录部署到 Vercel。`api/news.js` 为 Vercel Node.js Function，运行环境需提供 AI Gateway（Vercel OIDC 或 `AI_GATEWAY_API_KEY`），可通过 `AI_TRANSLATION_MODEL` 覆盖翻译模型。成功部署后获得可公开分享的 HTTPS 链接；网页的分享按钮复制当前地址。

## 更新范围

每日自动简报任务在当前对话北京时间 12:00 生成消息，网页中的首报文字目前是 2026-10-16 的固定快照；新闻由网页加载时单独获取，事件倒计时按页面日期自动刷新。每日对话简报尚未自动写回网页。

行情由公开 TradingView 数据组件提供，实时性与市场数据权限有关，并非 IBKR 专属报价。新闻翻译可能有误，页面提供原文链接供核对。内容仅作信息整理，不构成投资建议。
