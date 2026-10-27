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

### OP-010 · 添加机会分享模板

- 修改对象：Opportunities & Resources（分类 9），原标题提示和正文模板为空。
- 修改后：正文引导填写机会简介、适用对象、地点与时间、含时区的截止日期、原始来源/申请链接及相关利益关系；标题提示为 `Opportunity name and deadline / 机会名称与截止日期`。
- 验证：首次刷新发现正文已保存但标题提示未保留；补填并等待未保存状态出现后单独保存，再次刷新确认两项均保留。副本为 docs/site-content/template-opportunities.md。
- 回退：清空分类 9 的标题提示和正文模板并保存。
- 证据：<https://mcmc-alumni.discourse.group/c/opportunities-resources/9>（Edit this category → Template）。

### OP-011 · 自我介绍栏目模板

- 修改前：Introductions（分类 11）的标题提示与正文模板为空。
- 修改后：加入简单背景、想了解什么、愿意提供什么帮助的双语模板，提醒只分享愿意公开的信息；允许删除不适用的小标题。
- 验证：保存后刷新，标题提示和三段正文均保留。未发布测试主题；普通用户端效果待端到端测试。
- 证据：分类编辑页 Template；正文副本 docs/site-content/template-introductions.md。

### OP-012 · 侧栏显示与欢迎页复核

- 将侧栏标题缩短为 Start here / 入门，链接标签缩短为 Share / 分享机会、Introduce / 自我介绍；目标链接和全站可见性保持原值。
- 保存并确认全站显示，刷新后核对三个入口完整显示。已发布的欢迎帖仍为修订 4；关闭本轮留下的同内容编辑草稿，没有新增帖子。
- 页面效果截图仅存本地 outputs/mcmc-welcome-2026-10-27.png，未上传带登录状态的截图至公开仓库。

### OP-013 · 审批、栏目权限和模板实测

- 只读核对：must_approve_users=true；auto_approve_email_domains 为空；approve_post_count=0；approve_unless_allowed_groups 与 approve_new_topics_unless_allowed_groups 均为 admins、moderators、trust_level_0；approve_suspect_users=true；approve_unless_staged=false。保持原值。
- 旧搜索词 first_post_typing_time 当前返回 Fast typing threshold，实际键 fast_typing_threshold，值 disabled。快速输入检测仍关闭。
- Staff 安全页提示这是预置分类，安全设置不能编辑；未显示可编辑权限矩阵。未修改，也未以普通用户或访客实测其可见性。
- 分别从问答（6）、机会分享（9）、自我介绍（11）点击 New Topic，标题提示和各自正文模板均自动载入；检查后关闭本轮测试草稿，没有发布测试帖子。
- 本轮欢迎帖编辑草稿曾在刷新后恢复，确认已发布内容一致后再次关闭，并等待编辑框消失；不影响已发布修订 4。
- 验证限制：以上模板检查使用管理员会话；没有创建新用户，没有模拟邮箱验证、入站审批或普通用户最终发布。完整注册与普通发帖仍待测试，反垃圾检查仍可能触发审核。

### OP-014 · 同步 Issues、看板与交接资料

- 更新 Issues #2、#4：基础配置已实施，普通用户测试与运营/治理仍待完成；更新 #3 的 Free Plan 和 10 个分类现场结论，仍不宣称性能改善；更新 #5 的逐步记录规则与交接进展。四项写入均返回成功，Issues 保持开放。
- Project 将 #2、#4 从 Todo 移至 In Progress，新增 Done 草稿卡“已完成：首轮站点配置优化（邮箱、资料、引导与模板；2026-10-27）”；刷新确认。其余三个 Issue 仍在 Todo，原归档 Done 卡保留。
- 本地整理 README 阶段 11、CURRENT_STATE、HANDOFF、BACKLOG 和站点文案/模板副本；AGENTS 保留今后每步记录要求。文档编辑时两次补丁格式/匹配校验未通过，未改变线上站点；更正后写入。
- 下面统一提交这些交接内容，再核对远端文件；历史 Word 与 mcmc.html 不修改。没有新增协作者或改变仓库/看板可见性。

### OP-015 · 交接文件提交与完整性核对

- 交接提交：[d5ca75e0286a4de6f1b952d9e4247979853eeafe](https://github.com/1708994293-hue/MCMC/commit/d5ca75e0286a4de6f1b952d9e4247979853eeafe)，写入主分支时校验预期旧提交，未强制覆盖。
- 11 个新增/更新文档的远端 Git blob SHA 与本地 UTF-8 内容一致，内部文档链接检查无缺失。原 mcmc.html 和历史 Word 的 blob SHA 与修改前一致。
- Project 最终为 Todo 3、In Progress 2、Done 2；#2/#4 仍是开放 Issue，首轮配置优化有单独 Done 卡。创建卡片时先进入新 Issue 表单，取消后使用草稿卡；没有新增第六个 Issue。
- 已完成：邮箱域名配置、五个成员字段、欢迎引导、三入口、三模板，以及持续记录规则。待做：普通新用户完整注册/发布、毕业生邮箱例外、角色/隐私进一步验证、运营分工、卡顿测量。
- 未付费、未迁移、未变更账号角色、未对外群发；最终交付附论坛与 GitHub 链接及本地效果截图。后续从 OP-016 继续，不重建已有内容。
