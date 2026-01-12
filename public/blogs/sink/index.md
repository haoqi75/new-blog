# Sink - CloudFlare链接缩短器
![INIT](https://raw.githubusercontent.com/ccbikai/Sink/master/public/image.png)

## 体验
请访问 [Sink.Cool](https://sink.cool/dashboard) 体验演示。使用下方网站令牌登录：
访问令牌: `SinkCool`

## 什么是Sink？
Sink 是一款开源的、可自行托管的链接缩短服务，完全基于 [Cloudflare](https://www.cloudflare.com/) 的基础设施运行。它兼具简洁性和强大的功能，对于那些既想掌控链接管理，又想享受云端性能和可靠性的用户来说，是一个极具吸引力的选择。
由于 CloudFlare 免费套餐足以支持 Sink 的运行，因此可以免费部署 Sink。

## 主要特点
1. 高效的网址缩短：
	* 将冗长的网址压缩成简洁易分享的链接。
	* 非常适合用于社交媒体帖子、电子邮件营销和印刷材料。
2. 综合分析：
	* 追踪点击率、地理位置数据和引荐来源。
	* 深入了解受众行为和广告系列效果。
3. 自定义短网址：
	* 创建品牌化、易于记忆的短链接（例如，yourdomain.com/summer-sale）。
	* 提升用户对链接的认知度和信任度。
4. AI短网址生成：
	* 利用人工智能自动生成相关且吸引人的链接别名。
	* 节省手动自定义链接的时间。
5. 链接过期：
	* 为临时推广活动或有时效性的内容设置短链接的有效期。
	* 增强对共享信息的安全性和控制。
6. 无服务器架构：
	* 利用 Cloudflare Workers 实现可扩展性和低延迟性能。
	* 无需进行传统的服务器管理。
7. 注重隐私：
	* 自行托管链接数据，确保符合数据保护法规。
	* 完全掌控您的链接信息和分析数据。

## 如何构建
开源仓库：【[链接直达](https://github.com/ccbikai/Sink)】
1. 将此仓库fork到您的 GitHub 帐户。
2. 创建**KV 命名空间**或**Worker KV**（在“存储和数据库” -> “KV”下），并复制命名空间 ID。
3. 在`wrangler.jsonc`将`kv_namespaces`里的ID更新为您自己的命名空间 ID。
4. 在Cloudflare Workers中创建一个项目。（当然，pages也可以，但建议Workers）
5. 选择Sink存储库，然后使用以下构建和部署命令（默认已填）：
	构建命令：`pnpm run build`或`npm run build`
	部署命令：`npx wrangler deploy`
6. 保存并部署项目。
7. 首次部署会报出此错误（若没有请跳过此步骤）：
```
✘ [ERROR] A request to the Cloudflare API (/accounts/用户	ID/workers/scripts/sink/versions) failed.
You need to enable the Analytics Engine. Head to the Cloudflare Dashboard to enable: https://dash.cloudflare.com/用户ID/workers/analytics-engine [code: 10089]
```
请在**Analytics Engine（分析引擎）**开启那个功能（在“存储和数据库” -> “Analytics Engine（分析引擎）”下）点击**Enable**。再重试部署。
8. 首次部署完成后会自动绑定KV以及其他信息，转到“设置” -> “变量和密钥” -> “添加”，并配置以下环境变量：
	`NUXT_SITE_TOKEN`：必须至少包含8 个字符。此令牌用于授予您访问控制面板的权限。
	`NUXT_CF_ACCOUNT_ID`：查找您的帐户 ID。URL里面就有。
	`NUXT_CF_API_TOKEN`：创建一个至少具有 帐户.帐户分析（`Account.Account Analytics`）权限的Cloudflare API 令牌。
9. 绑定域名，即可使用。



