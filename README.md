# free-ai-router Web UI

> free-ai-router 的可视化演示页面
>
> 单 HTML 文件,GitHub Pages 免费托管
> v0.2：8 provider 真实数据 + 健康状态 + 成本计算器

---

## 这是什么?

[free-ai-router](https://github.com/fast118/free-ai-router) 的 Web Demo,让你**直观看到 fallback 流程**。

**功能:**
- 可视化 **8 provider** fallback 链路(5×minimax 包月 + 3×deepseek 按量)
- 🆕 **健康状态面板** — 展示哪些 provider 上次 health_check 标记为 unhealthy
- 🆕 **成本计算器** — 6 个模型实测价格对比
- 🆕 **跳过 health_check unhealthy** toggle — 模拟 v0.2 自动跳过坏 key
- 模拟跑请求(可勾选"模拟失败"看效果)
- 实时统计(总请求 / 触发 fallback / 节省费用)
- 真实命令行用法示例

## 部署

**GitHub Pages:**
1. 推代码到 `fast118/free-ai-router-webui` 仓库
2. Settings → Pages → Source 选 `main` 分支
3. 几分钟后访问 `https://fast118.github.io/free-ai-router-webui/`

**本地预览:**
```bash
py -m http.server 8000
# 访问 http://localhost:8000
```

## 截图(运行后)

```
┌────────────────────────────────────────────┐
│     🔀 free-ai-router                       │
│     多 AI 后端链式 fallback 路由器            │
├────────────────────────────────────────────┤
│  [github_models] → [groq] → [gemini] → [sk│
│  illai.top]                                 │
│                                            │
│  跑请求: 模拟 fallback 流程...               │
│  → [1/4] github_models... ✗ 429             │
│  → [2/4] groq... ✓ 成功 (180ms)            │
│                                            │
│  统计:                                      │
│  总请求: 5 | Fallback: 2 | 节省: $25        │
└────────────────────────────────────────────┘
```

## 实际跑 (跟 Web UI 配合)

```bash
# 装
pip install free-ai-router

# 5 minimax 包月 + 3 deepseek 按量
set MINIMAX_API_KEY_1=sk-cp-xxx1
set MINIMAX_API_KEY_2=sk-cp-xxx2
set MINIMAX_API_KEY_3=sk-cp-xxx3
set MINIMAX_API_KEY_4=sk-cp-xxx4
set MINIMAX_API_KEY_5=sk-cp-xxx5
set DEEPSEEK_API_KEY_1=sk-xxx1
set DEEPSEEK_API_KEY_2=sk-xxx2
set DEEPSEEK_API_KEY_3=sk-xxx3

# 3. 跑
py smart_router.py "你的问题"
py smart_router.py --status      # 看 8 个 provider 状态
```

实际跑出来的 fallback 流程跟 Web UI 模拟的一样,只是 Web UI 是不调 API 的演示。

## 文件结构

```
free-ai-router-webui/
├── index.html      # 单文件 demo(HTML + CSS + JS 全在这里)
├── assets/         # 预留:放截图
└── README.md
```

## 跟生态的配合

```
free-ai-router-webui (Web 演示)
  ↓ 看完想装
free-ai-router (CLI)
  ↓ 撞限速
api.skillai.top (国内中转)
  ↓ 付费用户
```

## v0.2 更新 (2026-06-20)

- ✨ **8 provider 真实数据**：从原 4 provider (skillai.top 时代) 升级到 5×minimax 包月 + 3×deepseek 按量
- ✨ **健康状态面板**：顶部显示 ok/失败数 + 最后检查时间
- ✨ **跳过 unhealthy toggle**：模拟 v0.2 smart_router 自动跳过 health_check 标记的坏 key
- ✨ **成本计算器**：6 个模型 (MiniMax-M3 / M2.7 / deepseek-chat / reasoner / gpt-4o / claude-sonnet-4) 实测价格对比
- ✨ **重置统计 / 清日志按钮**：UX 改进
- ✨ **移动端响应式**：≤700px 自动单列布局
- ✅ 零依赖（单 HTML，~22KB）

## v0.2 vs v0.1

| 项 | v0.1 (06-11) | v0.2 (06-20) |
|---|------|------|
| provider 数 | 4 (skillai.top) | 8 (5 minimax + 3 deepseek) |
| 真实数据 | ❌ 模拟 | ✅ 匹配 router_config.json |
| 健康状态 | ❌ | ✅ 顶部 panel |
| 成本计算 | ❌ | ✅ 6 模型对比 |
| 跳过 unhealthy | ❌ | ✅ toggle 模拟 |
| 响应式 | ❌ | ✅ 移动端单列 |
| 文件大小 | 8 KB | 22 KB |

## License

MIT


## 💬 联系

扫码加微信群（AI 工具使用 / 提 issue / 需求讨论）：

![微信群](assets/wechat-qr.png)

或提 [GitHub Issue](https://github.com/fast118/free-ai-router-webui/issues)
