# 百度收录处理清单

## 先处理最关键的问题

1. 确认正式域名 `http://www.manhart.top` 可以稳定访问，并让 IP 地址、`http://manhart.top`、`www.manhart.top` 统一 301 跳转到这个地址。
2. 确认服务器可以公网访问 `robots.txt` 和 `sitemap.xml`。
3. 登录百度搜索资源平台，添加并验证站点。
4. 在普通收录里提交首页和 sitemap，优先提交：
   - `http://www.manhart.top/`
   - `http://www.manhart.top/products.html`
   - `http://www.manhart.top/about.html`
   - `http://www.manhart.top/service.html`
   - `http://www.manhart.top/featured.html`
   - `http://www.manhart.top/news.html`
   - `http://www.manhart.top/store.html`
   - `http://www.manhart.top/product-detail.html`
5. 申请 ICP 备案并在页脚展示备案号。国内搜索引擎对企业官网的信任判断会明显受域名、备案、品牌一致性影响。

## 已在代码里补强的项目

- 首页标题改为“曼哈特门官网 - 浙江曼哈特安防科技有限公司 | MANHART”。
- 每个页面都改成唯一标题，避免所有页面在百度里显示成同一个名称。
- 每个页面补充更明确的品牌词、公司全称和门类关键词。
- 首页增加 Organization 结构化数据，帮助搜索引擎识别公司名称、品牌别名、地址和电话。
- `robots.txt` 明确允许 `Baiduspider` 抓取。
- `sitemap.xml` 的更新时间改为 `2026-06-19`。

## 后续观察

提交后不要立刻用普通搜索判断是否成功。先在百度搜索资源平台看抓取诊断、索引量、抓取异常。新站从发现到收录常见需要数天到数周，普通收录只能加快发现，不保证一定收录。
