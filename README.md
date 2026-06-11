# free-ai-router Web UI

> free-ai-router 的可视化演示页面
>
> 单 HTML 文件,GitHub Pages 免费托管

---

## 这是什么?

[free-ai-router](https://github.com/fast118/free-ai-router) 的 Web Demo,让你**直观看到 fallback 流程**。

**功能:**
- 可视化 4 步 fallback 链路
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

# 配 key
export GITHUB_TOKEN=ghp_xxx
export GROQ_API_KEY=gsk_xxx
export GEMINI_API_KEY=AIzaSy_xxx

# 跑
free-ai-router ask "你的问题"
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

## License

MIT