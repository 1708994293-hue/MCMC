# 当前配置与验证范围

现场核验日期：2026-10-27（Asia/Shanghai）。完整过程见 [操作日志](OPERATIONS_LOG.md)。以下是当日快照，未来修改须更新。

## 站点与注册

| 项目 | 当前值 / 结论 |
| --- | --- |
| 地址 | https://mcmc-alumni.discourse.group/ |
| 后台方案 | Free Plan；本轮未升级 |
| allowed_email_domains | um.edu.mo；由空值改为该域名，保存刷新确认；UI 说明自动包含子域名 |
| 包含示例 | @um.edu.mo、@connect.um.edu.mo；邮箱不是满珍身份认证 |
| must_approve_users | true，保持原值；新用户登录前仍需管理员或版主批准 |
| auto_approve_email_domains | 空，保持原值 |
| allow_new_registrations / invite_only | true / false，保持原值 |
| login_required | false，保持原值；内容默认按公开阅读理解 |
| 例外流程 | 无可用澳大邮箱的毕业生通过已有书院/校友渠道联系项目组；正式处理规则仍待确定 |

邮箱规则已保存不等于所有注册路径均已端到端实测；未创建测试账号，未测试邀请码绕过、邮箱变更、旧账号影响或 Discourse ID 特殊路径。

## 用户资料字段

修改前无自定义字段；现在共五个，全部允许本人事后修改，均不显示在用户名卡片且不设为可搜索。

| ID | 名称 / 类型 | 要求 | 注册页 | 公开资料页 |
| --- | --- | --- | --- | --- |
| 1 | Member status / 成员身份，Dropdown | On signup | 显示 | 显示 |
| 2 | MCMC connection / 与满珍的关系，Dropdown | On signup | 显示 | 不显示 |
| 3 | Graduation year / 毕业年份，Text | Optional | 不显示 | 填写后显示 |
| 4 | Programme / field / 专业或行业，Text | Optional | 不显示 | 填写后显示 |
| 5 | How I can help / 我能提供的帮助，Textarea | Optional | 不显示 | 填写后显示 |

身份选项：在校生、毕业生、澳大教职员、其他澳大成员。满珍关系选项：满珍在校生、满珍毕业生、满珍教职员、其他澳大成员，均为中英双语。两个必填字段仅要求新注册者填写，不强迫全部现有用户补填；其余字段说明提醒可留空，勿填写私人标识或联系方式。所有值自报，不能充当认证。

## 引导与模板

- 欢迎主题 5 原位更新为双语介绍、三个入口、注册说明和隐私提示；作者仍为 system，现修订 4。
- 全站侧栏 Start here / 入门：Ask Alumni / 提问 → 分类 6；Share / 分享机会 → 分类 9；Introduce / 自我介绍 → 主题 14。
- 分类 6：具体问题、个人背景、已做尝试、可选时间；标题提示 One clear question / 用一句话写清你的问题。
- 分类 9：机会内容、条件、时间地点、截止时间及时区、原始来源、关系披露；标题提示 Opportunity name and deadline / 机会名称与截止日期。
- 分类 11：个人简介、希望了解什么、能分享或帮助什么；标题提示 Say hello and share an interest / 打个招呼，分享一个兴趣。
- 使用普通 Markdown 主题模板，未启用结构化 Form template。正文源文件见 [site-content](site-content/README.md)。
- 三套模板均在保存刷新后确认，并分别打开新主题编辑框验证自动载入。测试使用管理员账号，未发布测试主题，已关闭本轮测试草稿。

## 日常发帖与安全检查（只读核对，未修改）

| 设置 | 现场值 |
| --- | --- |
| approve_post_count | 0 |
| approve_unless_allowed_groups | admins, moderators, trust_level_0 |
| approve_new_topics_unless_allowed_groups | admins, moderators, trust_level_0 |
| fast_typing_threshold | disabled；以旧关键词 first_post_typing_time 搜索可找到 |
| approve_suspect_users | true |
| approve_unless_staged | false |
| 问答分类 New topic approval / New reply approval | No one / No one |

以上支持普通成员无需常规逐帖预审的意图，但可疑行为及其他反垃圾规则仍可能进入审核。新账号批准入站是另一环节，未关闭。普通成员实际发布结果尚未测试。

## 分类与真实内容入口

当前列表 10 个：Announcements 5、General 4、Staff 3、Student–Alumni Q&A 6、Introductions 11、Site Feedback 2、Careers & Internships 7、Further Study 8、Opportunities & Resources 9、Events & Meetups 10。历史 Uncategorized 未显示。

Staff 描述声称只向管理员/版主显示，Security 页说明这是安全设置不可编辑的预置分类；未以非管理员身份验证，也没有新建私密分区。

| 主题 | 已确认链接 |
| --- | --- |
| 欢迎 | [Welcome to MCMC Alumni Network](https://mcmc-alumni.discourse.group/t/welcome-to-mcmc-alumni-network/5) |
| 自我介绍 | [Introduce Yourself / 自我介绍](https://mcmc-alumni.discourse.group/t/introduce-yourself/14) |
| 问答 | [What advice would you give current MCMC students?](https://mcmc-alumni.discourse.group/t/what-advice-would-you-give-current-mcmc-students/15) |
| 纪念文章 | [In Memoriam: Professor Kevin “Kit” Thompson](https://mcmc-alumni.discourse.group/t/in-memoriam-professor-kevin-kit-thompson-founding-master-of-mcmc/31) |
| 学生项目支持帖 | [各位澳大满珍毕业生快回母校支援学弟学妹的project](https://mcmc-alumni.discourse.group/t/project/26) |

首页观察到欢迎与纪念主题的 Pinned 标记；未检查全站/分类置顶期限。欢迎帖阅读后的个人 Unpinned 状态不能推断为管理员取消了置顶。

## 仍未完成

真实新账号的注册、邮箱限制和普通发帖完整测试；无澳大邮箱毕业生的规则；核心账号角色复核；Staff 访客/成员可见性测试；纪念帖图源和置顶期限；卡顿测量；运营分工与用户引入。没有付费、迁移、角色变更或群发。
