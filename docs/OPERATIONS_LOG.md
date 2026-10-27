# 项目操作记录

从 2026-10-27 起，按用户要求记录每个有意义的检查、修改、验证与回退。时间采用 Asia/Shanghai。浏览器点击和加载动作按其对应的业务步骤合并，不记录私人账号资料或会话。

## 2026-10-27 · 优化实施

### OP-001 · 接受实施授权并建立持续记录规则

- 用户要求：将此前提出的优化付诸实践，完成后写入 GitHub；今后每步操作或修改都要记录。
- 范围：核验并落实当前方案允许的邮箱准入、成员资料、新成员入口、发帖模板、隐私与管理说明；不新增付费订阅或迁移。
- 修改：AGENTS.md 增加逐步 GitHub 记录要求，创建本日志。
- 前置检查：仓库主分支为 `48b8e94f0e98f2e14ae93d34f14c40cab5724d1a`，读取现有 README/HANDOFF/BACKLOG。
- 结果：已获得本轮实施授权；不再把步骤 9 的全部建议一概视为无实施授权。实际结果仍逐项记录。

### OP-002 · 检查论坛会话与既有内容

- 操作：打开论坛首页和管理后台，只读核验。
- 结果：当前会话显示 Sueleven，能够进入 Admin；无需重新登录。
- 找回链接：欢迎帖 `/t/welcome-to-mcmc-alumni-network/5`；自我介绍 `/t/introduce-yourself/14`；经验问答 `/t/what-advice-would-you-give-current-mcmc-students/15`；纪念帖 `/t/in-memoriam-professor-kevin-kit-thompson-founding-master-of-mcmc/31`；Olivia617 项目帖 `/t/project/26`。
- 首页可见欢迎帖及纪念帖 Pinned 标记；纪念帖作者为 Sueleven。系统欢迎帖目前显示作者 system，后续编辑前以现有内容为准。
- 限制：尚未检查具体设置值、普通用户注册/发帖、置顶期限和图片署名。
- 证据：<https://mcmc-alumni.discourse.group/>、<https://mcmc-alumni.discourse.group/admin>。

### OP-003 · 启用澳大邮箱域名准入

- 修改前：`allowed_email_domains` 为空；后台显示 Free Plan。
- 修改后：`allowed_email_domains = um.edu.mo`。界面说明明确包含其子域名，因此覆盖 `connect.um.edu.mo`，无需通配符或重复域名。
- 原因：落实用户要求的澳大邮箱筛选，同时覆盖终身邮箱；不等同于满珍身份认证。
- 验证：保存完成后重新加载同一设置页，仍显示 um.edu.mo，未保存提示消失；当前管理员会话正常。
- 未改动：现有账号、角色、新用户入站审批、其他反垃圾设置。
- 限制：尚无真实普通新账号完成端到端注册测试；Discourse ID 邮箱需满足站点准入。无可用澳大邮箱的毕业生需先联系项目组，不能承诺邀请自动绕过限制。
- 回退：在同一设置项清空允许域名并保存，恢复本轮前状态。
- 证据：<https://mcmc-alumni.discourse.group/admin/site_settings/category/all_results?filter=allowed_email_domains>。

### OP-004 · 创建成员身份和书院关系字段

- 修改前：User fields 页面显示没有自定义字段。
- OP-004a：新增 `Member status / 成员身份`（ID 1），下拉选项为在校生、毕业生、澳大教职员、其他澳大成员；仅新注册必填，可编辑，公开资料页可见；说明明确自填不等于认证。
- OP-004b：新增 `MCMC connection / 与满珍的关系`（ID 2），下拉选项为满珍在校生、满珍毕业生、满珍教职员、其他澳大成员；仅新注册必填，可编辑，不在公开资料页或用户卡显示。
- 验证：两次保存均显示 User field saved，列表显示正确的名称、类型、公开可见性及编辑标记。旧用户不被强制补填（采用 On signup，而非 For all users）。
- 限制：尚未以普通新账号走完注册，未把自填关系用作自动授权依据。
- 回退：可编辑对应字段为 Optional，关闭公开资料显示；不要直接删除已收集的数据。
- 证据：<https://mcmc-alumni.discourse.group/admin/config/user-fields>。

### OP-005 · 创建三个选填资料字段

- OP-005a：新增 `Graduation year / 毕业年份`（ID 3，Text）。
- OP-005b：新增 `Programme / field / 专业或行业`（ID 4，Text）。
- OP-005c：新增 `How I can help / 我能提供的帮助`（ID 5，Textarea）。
- 共同设置：Optional、可自行编辑、填写后公开资料页显示、不显示在注册表单、不显示在用户卡、不启用搜索索引。描述说明可留空及避免私人联系方式和保密信息。
- 验证：每个字段保存后出现 User field saved，列表已列出五个字段及正确类型/可见性；未替任何成员填写资料。
- 执行恢复：创建第三个选填字段时页面尚未进入表单，读取当前状态后重新打开；此前两个字段已保存，未重复创建。
- 回退：关闭相关字段公开显示或修改说明；不直接删除成员已填写的数据。
- 证据：<https://mcmc-alumni.discourse.group/admin/config/user-fields>。

### OP-006 · 复核资料字段和现有栏目

- 重新进入字段 1、2、3 的编辑页：字段 1、2 确认为 On signup；字段 3 为 Optional；可见性、可编辑及注册表单显示符合 OP-004/005 记录。
- 分类页当前实际显示 10 个栏目（Announcements、General、Staff、Student–Alumni Q&A、Introductions、Site Feedback、Careers & Internships、Further Study、Opportunities & Resources、Events & Meetups），未显示 Uncategorized。
- Staff 的栏目说明称管理员/版主私密讨论，实际权限矩阵仍待核验，不能仅凭描述保证访问控制。
- 证据：<https://mcmc-alumni.discourse.group/categories>。

### OP-007 · 更新既有欢迎帖

- 修改对象：主题 5 的首帖，作者保持 system，未创建重复欢迎帖；编辑历史从第 3 版变为第 4 版。
- 修改前：一般用途说明，入门步骤只有栏目名称，没有直接入口和具体准入说明。
- 修改后：加入 Ask Alumni、Share an Opportunity、Introduce Yourself 三个真实链接；说明澳大邮箱、现有新账号入站审核、成员字段可见性，以及保护隐私、机会来源/截止时间、举报与 TL4 非身份认证。
- 验证：保存后重新加载主题，三个入口、双语说明和第 4 版编辑历史均可见。首页此前的 Pinned 与个人已读后的 Unpinned 不混为同一状态，本次未改置顶范围。
- 原文和更新后的 Markdown 保存在 docs/site-content，随本轮资料提交，便于回退；也可通过论坛编辑历史恢复第 3 版。
- 证据：<https://mcmc-alumni.discourse.group/t/welcome-to-mcmc-alumni-network/5>。

### OP-008 · 添加面向全站的三个快速入口

- 修改前：侧栏只有通用 Topics 和部分分类，新用户缺少按目的进入的链接。
- 修改后：创建 `Start here / 从这里开始` 自定义侧栏分区，并勾选 Visible to everyone。包含 Ask Alumni → 分类 6、Share Opportunity → 分类 9、Introduce Yourself → 主题 14。
- 验证：保存后重新加载分类页，三个链接仍出现在侧栏；链接均指向此前核对过的真实站内目标。这里只增加导航，不更改目标页面的访问权限。
- 回退：通过 Edit custom section 编辑或移除这一新建分区。
- 证据：<https://mcmc-alumni.discourse.group/categories>。

### OP-009 · 添加问答栏目发帖模板并核对审核

- 修改对象：Student–Alumni Q&A（分类 6）的 Template。
- 修改前：标题提示与正文模板均为空。
- 修改后：标题提示 `One clear question / 用一句话写清你的问题`；正文分为背景、具体问题、已尝试的方法、相关时间（选填），附中英文与隐私提示。使用普通 Markdown 预填模板，不启用额外表单模式。
- 验证：保存后重新加载栏目编辑页，标题提示、正文与预览保留。模板副本为 docs/site-content/template-questions.md。
- 同步只读核验：Moderation 中 New topic approval = No one、New reply approval = No one；本步没有修改审核配置。
- 回退：清空分类 6 的标题提示和普通正文模板，保存栏目。
- 证据：<https://mcmc-alumni.discourse.group/c/student-alumni-q-a/edit/general>。
