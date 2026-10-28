# 每日美股简报

默认跟踪 TSLA、ORCL、KLAC、LRCX、CRDO、COHR、AMKR、SOFI、PONY、SOUN、DOW、NVO。可在网页添加最多 8 只自选股（总数上限 20），新增代码会显示在行情、新闻和分享链接中；可输入 `NASDAQ:AAPL` 或 `NYSE:IBM` 指定交易所，不写交易所时默认 NASDAQ。

## 预览和新闻

本地可直接打开 `index.html` 预览静态页面，但 `file://` 不能运行新闻接口。动态新闻使用 Cloudflare Pages Functions 与 Workers AI；从 Google News RSS 获取新闻，个股新闻直接显示在股票卡片内，每只股票最多 2 条，新增自选股会自动纳入抓取。宏观与全球要闻独立显示，覆盖美国国债与经济数据、美国政策、霍尔木兹海峡与能源、AI/半导体及中美科技等主题，每个主题最多显示 2 条近两天新闻。标题和摘要会翻译为简体中文并标注可能影响方向。页面打开时加载新闻，页面保持打开时每 6 小时自动刷新，也可手动刷新。

持仓台账支持买入/卖出、股数、成交价、手续费和交易日期，按加权平均成本计算持仓及已实现盈亏。交易记录只存放在当前浏览器的 `localStorage`，不会写进分享 URL，也不会发送到新闻 API；更换浏览器或清除站点数据后记录不会自动迁移。

## 免费部署

将 GitHub 仓库导入 Cloudflare Pages，选择无框架（None），构建命令留空，输出目录填写 `.`。仓库中的 `functions/api/news.js` 会作为 `/api/news` Pages Function 运行；`wrangler.jsonc` 声明了 Workers AI binding，变量名为 `AI`。如果控制面板未自动读取绑定，在 Pages 项目设置的 Functions/Bindings 中手动添加 Workers AI binding `AI`，然后重新部署。部署完成后使用 Cloudflare 提供的 `pages.dev` HTTPS 链接。

Cloudflare Workers Free 当前包含每天 100,000 次 Worker/Functions 请求；Workers AI 每天提供 10,000 Neurons 免费额度，超过额度时模型请求会失败，付费计划可能产生费用。静态文件请求不限量。详见 Cloudflare [Pages Functions 定价](https://developers.cloudflare.com/pages/functions/pricing/)和 [Workers AI 定价](https://developers.cloudflare.com/workers-ai/platform/pricing/)。

## 更新范围

每日自动简报任务在当前对话北京时间 12:00 生成消息，网页中的宏观首报文字仍是 2026-10-16 的固定快照；个股新闻由网页独立获取，事件倒计时按页面日期自动刷新。每日对话简报尚未自动写回网页。

行情由公开 TradingView 数据组件提供，实时性与市场数据权限有关，并非 IBKR 专属报价。新闻翻译可能有误，页面提供原文链接供核对。内容仅作信息整理，不构成投资建议。
