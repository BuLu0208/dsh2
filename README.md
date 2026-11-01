# 冷夜的 dsh 小作坊 (dsh2)

基于 [DeepSeek Harness](https://github.com/deepseek-ai/deepseek-harness) 最新源码 + [dsh-purge 1.1.71 满血版](https://github.com/BuLu0208/dsh-purge1171) 内置构建。

## 这是什么

一个独立的 macOS 桌面客户端（`dsh2`），与官方 `DeepSeek Harness` **完全并存、互不干扰**：

| 维度 | 官方 DSH | 冷夜的 dsh 小作坊 |
|---|---|---|
| 应用名 | DeepSeek Harness | **冷夜的 dsh 小作坊** |
| Bundle ID | com.deepseek.harness | **com.buluo.dsh2** |
| 配置目录 | `~/.dsh` | **`~/.dsh2`** |
| URL Scheme | `dsh://` | **`dsh2://`** |
| 内置插件 | — | **冷夜的全能破甲助手** |

## 构建方式

全部在 GitHub Actions 上完成，本地零编译：

```bash
# 手动触发
gh workflow run build-dsh2.yml -f dsh_ref=master

# 或打 tag 触发
git tag build-$(date +%Y%m%d) && git push origin --tags
```

产物：`dsh2-<version>-mac-arm64-unsigned.dmg`（未签名，ad-hoc 可用）

## 内置内容

### 冷夜的全能破甲助手 (dsh-purge 1.1.71)

- 三处自我限制条款已清洗并重新加密
- 完整的 agent-loop / system-prompt host 补丁已适配最新 DSH
- 开箱即用，无需手动「清洗 → 应用」

### 已修复的 21 个 host 补丁

| # | 补丁 | 状态 |
|---|---|---|
| 6 | SANDBOX_DENY_FILE_WRITE | ✅ 已适配 |
| 9 | APPROVAL_AUTO_GRANT | ✅ 已适配 |
| 10 | APPROVAL_CONFIG_DEFAULT_NEVER | ✅ 已适配 |
| 13 | ESCALATION_WIDENING_EXEMPT | ✅ 已适配 |
| 14 | ESCALATION_GRANT_UNCONDITIONAL | ✅ 已适配 |
| 15 | SANDBOX_CONFINE_PASSTHROUGH | ✅ 已适配 |
| 16 | FS_FENCE_DISABLED | ✅ 已适配 |
| 17 | FS_OBSERVATION_INTENT_FREE | ✅ 已适配 |
| 18 | REPEAT_TOOL_REMINDER_DISABLED | ✅ 已适配 |
| 19 | TOOL_RESULT_PRUNER_DISABLED | ✅ 已适配 |
| 21 | BASH_TIMEOUT_RESTORE | ⚪ 官方已符合 |
| 22 | READ_CAPS_RAISED | ✅ 已适配 |
| 23 | SUBAGENT_MAXDEPTH_RAISED | ✅ 已适配 |
| 24 | PRESET_FETCH_ENABLED | ⚪ 官方已符合 |
| 42 | SETTINGS_LEGACY_API | ⚪ 仅兼容第三方老插件 |
| 55 | SYSTEM_PROMPT_REPLACE_HEAD | ✅ 已适配 |
| 66 | SYSTEM_PROMPT_RENDER_GUARD | ✅ 已适配 |
| 67 | AGENT_LOOP_MESSAGES_GUARD | ✅ 已适配 |
| 68 | SYSTEM_NODES_CONTENT_GUARD | ✅ 已适配 |
| 74 | ASSEMBLE_BEFORE_PRESTEP | ✅ 已适配 |
| 83 | DESKTOP_HOST_CLOSE_NO_FATAL | ✅ 已适配 |

## 目录结构

```
.github/workflows/build-dsh2.yml   构建工作流
patches/host.patch                 21 个 host 补丁适配
patches/branding.patch             品牌参数化
```

## 安装

1. 从 Actions 产物下载 `.dmg`
2. 拖入 `/Applications`
3. 首次打开需右键 → 打开（未签名）
4. 数据自动落在 `~/.dsh2`，与官方版完全隔离

## 许可

- DSH 源码：MIT（DeepSeek AI）
- dsh-purge：MIT（原作者见 [signature section](https://github.com/YuJunZhiXue/dsh-purge)）
- 本仓库：仅构建配方与适配补丁
