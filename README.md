# hosted-pages · 通用托管页（A 路线静态版）

> 当前阶段标注：**Phase 0A 止血动作**——静态托管 + 免费表单后端，0 元、人不写代码；完整设计见 `docs/v3-通用落地页方案.md` §2.2（A1）。
> 生成日期：2026-10-03 ｜ 数据源：`docs/registry-v2.json`（110 行）+ `docs/projects/*-事实卡.md`
> **部署是 🔴 人的动作**；**✅ 部署已完成 2026-10-05（方案 B · GitHub Pages）**：`https://autodevorder.github.io/publicize-pages/`，直连实测根 `/` 200 + 5 页全 200，workers.dev 全部作废；**表单后端 ✅ 已配置 2026-10-04**：6 处 `form action` 已替换为 `https://formspree.io/f/xqpekkav`（表单 `publicize-hosted-pages`），无需再改。

## 0. 目录结构

```
hosted-pages/
├── template.html            # 通用模板（字段占位 + 🔴标记，新项目从它复制）
├── README.md                # 本文件
└── p/<slug>/index.html      # 已生成的页面（URL = /p/<slug>/）
    ├── validation-os/        # 有事实卡 · landing.mode=own（自有站为主收口，本页为镜像）
    ├── d-hrs/                # 有事实卡 · hosted
    ├── competition/          # 有事实卡 · hosted
    ├── quantitative/         # 无卡 · draft · 🔴待补占位
    └── geo/                  # 无卡 · draft · 🔴待补占位
```

## 1. 部署三步（二选一，Cloudflare Pages 或 GitHub Pages）

### 0）部署前门禁（15min，🔴，一票否决）
在你的网络下实测可达性：手机 + 电脑各打开 `https://<你的子域>.pages.dev` 与 `https://<你的账号>.github.io`——**不可达 = 白建**（`v3-通用落地页方案.md` §6 R1；本机 `github.com` 曾连接被重置）。哪个可达用哪个。

### 方案 A：Cloudflare Pages（推荐，免费子域不需买域名）
1. **建站**：登录 Cloudflare → Workers & Pages → Create → Pages → **Direct Upload** → 起名（如 `publicize`）→ 把本目录内容（`template.html` + `p/` + `README.md`）作为构建输出目录上传（拖拽/`wrangler pages deploy` 均可）。得到 `https://publicize.pages.dev`。
2. **配置表单后端**：**✅ 已完成 2026-10-04** —— 表单 `publicize-hosted-pages`，endpoint `https://formspree.io/f/xqpekkav` 已写入 template + 5 页共 6 处 `form action`（`GET` 探测返回 405 = 端点存活，Formspree 只收 POST）。免费层 50 提交/月（账户级）、30 天历史——量起来前先够用。
   - ⚠️ **Formspree 注册邮箱必须点确认链接**才开始收件；未确认前首次提交会失败。确认后跑一遍下方第 3 步冒烟。
3. **回填 + 冒烟**：把可用 URL 回填 `docs/registry-v2.json` 对应行的 `landing.url`（`/p/<slug>/` → 完整 URL）→ 打开 `/p/competition/?utm_source=zhihu&utm_medium=answer&utm_campaign=c1-001`，确认页内显示「来源」徽标、提交一个测试邮箱、在 Formspree 后台看到 `slug/utm_*` 字段 → 回填 `docs/归因台账.md`。

### 方案 B：GitHub Pages（备选，注意可达性风险）
1. **建站**：把 `hosted-pages/` 内容推到仓库（建议独立 `gh-pages` 分支，内容放**分支根目录**，这样 URL 才是 `/p/<slug>/`）→ 仓库 Settings → Pages → Deploy from a branch → 选该分支 `/ (root)` → 得到 `https://<账号>.github.io/<仓库名>/`。若只能用 `main` 分支的 `/docs` 文件夹，则 URL 会带 `/hosted-pages/` 前缀，**回填 registry 与 UTM 链接时必须按实际前缀写**。
2. **配置表单后端**：同方案 A 第 2 步（GitHub Pages 无 Functions，收单必须走 Formspree/Google Forms）。
3. **回填 + 冒烟**：同方案 A 第 3 步；另注意 GitHub Pages **无自定义校验**，honeypot/时长拦截要靠 Formspree 自带 + 每周 5min 人肉清垃圾。

> 换托管不换 slug（R2/R5）：页面文件与 registry 行都不动，只改域名前缀。

## 2. 每页预填 UTM 链接清单（格式对齐 `v1-发布配套包.md` §2）

**规则（配套包 §1，照抄不改）**：`utm_campaign = 内容ID = 折扣码`，三者永久一致、永不复用；`utm_medium` 固定三值 `answer / shortpost / engineering`；同一条内容发第二平台只换 `utm_source`，campaign 不换。
**✅ host 已最终化（2026-10-05）**：最终域名 = `https://autodevorder.github.io/publicize-pages`（GitHub Pages，直连可达）。下面 15 条链接已替换完毕、直接复制可用。
**内容ID 为本批预留命名**：🔴发布前由人确认并登记进 `docs/归因台账.md`（确认即冻结，不得与已用 ID 冲突）；这批项目均无定价页，折扣码=内容ID 规则沿用但暂不部署码。

| 页面 | 内容ID（=折扣码） | 平台/形态 | 完整链接（✅ 已最终化，直接复制可用） |
|---|---|---|---|
| validation-os | **q2-001** | 知乎 / answer | `https://autodevorder.github.io/publicize-pages/p/validation-os/?utm_source=zhihu&utm_medium=answer&utm_campaign=q2-001` |
| validation-os | **q2-002** | 即刻 / shortpost | `https://autodevorder.github.io/publicize-pages/p/validation-os/?utm_source=jike&utm_medium=shortpost&utm_campaign=q2-002` |
| validation-os | **q2-003** | V2EX / engineering | `https://autodevorder.github.io/publicize-pages/p/validation-os/?utm_source=v2ex&utm_medium=engineering&utm_campaign=q2-003` |
| competition | **c1-001** | 知乎 / answer | `https://autodevorder.github.io/publicize-pages/p/competition/?utm_source=zhihu&utm_medium=answer&utm_campaign=c1-001` |
| competition | **c1-002** | 即刻 / shortpost | `https://autodevorder.github.io/publicize-pages/p/competition/?utm_source=jike&utm_medium=shortpost&utm_campaign=c1-002` |
| competition | **c1-003** | V2EX / engineering | `https://autodevorder.github.io/publicize-pages/p/competition/?utm_source=v2ex&utm_medium=engineering&utm_campaign=c1-003` |
| d-hrs | **h1-001** | 知乎 / answer | `https://autodevorder.github.io/publicize-pages/p/d-hrs/?utm_source=zhihu&utm_medium=answer&utm_campaign=h1-001` |
| d-hrs | **h1-002** | 即刻 / shortpost | `https://autodevorder.github.io/publicize-pages/p/d-hrs/?utm_source=jike&utm_medium=shortpost&utm_campaign=h1-002` |
| d-hrs | **h1-003** | V2EX / engineering | `https://autodevorder.github.io/publicize-pages/p/d-hrs/?utm_source=v2ex&utm_medium=engineering&utm_campaign=h1-003` |
| quantitative | **qt1-001** | 知乎 / answer | `https://autodevorder.github.io/publicize-pages/p/quantitative/?utm_source=zhihu&utm_medium=answer&utm_campaign=qt1-001` |
| quantitative | **qt1-002** | 即刻 / shortpost | `https://autodevorder.github.io/publicize-pages/p/quantitative/?utm_source=jike&utm_medium=shortpost&utm_campaign=qt1-002` |
| quantitative | **qt1-003** | V2EX / engineering | `https://autodevorder.github.io/publicize-pages/p/quantitative/?utm_source=v2ex&utm_medium=engineering&utm_campaign=qt1-003` |
| geo | **geo1-001** | 知乎 / answer | `https://autodevorder.github.io/publicize-pages/p/geo/?utm_source=zhihu&utm_medium=answer&utm_campaign=geo1-001` |
| geo | **geo1-002** | 即刻 / shortpost | `https://autodevorder.github.io/publicize-pages/p/geo/?utm_source=jike&utm_medium=shortpost&utm_campaign=geo1-002` |
| geo | **geo1-003** | V2EX / engineering | `https://autodevorder.github.io/publicize-pages/p/geo/?utm_source=v2ex&utm_medium=engineering&utm_campaign=geo1-003` |

> **存量不破坏**：ValidationOS 已发的 q1-001/002/003 三条链接指向 `https://www.validation-os.com/waitlist`，**不迁移、不改链**（`v3-通用落地页方案.md` §4.4）；q2-* 只用于**新内容**走托管页镜像时使用，选哪条由人拍板。
> 页内已埋 UTM 读取脚本：从 URL query 捕获 `utm_source/utm_medium/utm_campaign` → 页内「来源」徽标 + 注入 hidden 字段（另有 `slug/referrer/ts_loaded/hp`），表单后端配置后即完成归因透传。

## 3. 🔴 待人清单（本目录相关）

| # | 事项 | 说明 | 状态 |
|---|---|---|---|
| 1 | Gate 0 可达性实测 | 15min，部署前做，不可达换方案 | ✅ 电脑侧已测（GitHub Pages 直连 200） |
| 2 | 部署（A 或 B） | 登录托管平台属红线，AI 不代做 | ✅ **已完成 2026-10-05（方案 B · GitHub Pages）** |
| 3 | 表单后端配置 | 逐页回填 `form action`（Formspree/Google Forms），未配置前提交不入库 | ✅ 已配置 2026-10-04（6/6） |
| 4 | 5 页人审 | 对照事实卡查编造（🟡终审，20min）——重点：三张卡页的局限/能力表述 | ✅ **已拍板 2026-10-05（A/B/C/D 按建议）**，落地 4 页改动，见 `终审预检报告.md` §5 |
| 5 | 内容ID 拍板冻结 | q2/c1/h1/qt1/geo1 系列确认后登记归因台账 | ✅ **已冻结 2026-10-05**：口径 A + 15 个 ID 全勾，已登记 `docs/归因台账.md` §1 |
| 6 | registry `landing.url` 回填 | 部署拿到真实域名后，把 5 行的 `/p/<slug>/` 换成完整 URL | ✅ **已完成 2026-10-05**（5 行已回填） |
