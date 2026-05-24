# APIKey Leak

GitHub AI 密钥泄漏扫描器 — 搜索 GitHub 上意外暴露的 AI 厂商 API Key 并自动验证有效性。

## 支持的厂商

OpenAI / DeepSeek / Anthropic / Google AI / HuggingFace / xAI / Cohere / Replicate / Together AI / Mistral / Groq / Perplexity / Jina AI / Voyage AI / Fireworks AI / DeepInfra / Novita AI / SiliconFlow / AI21 Labs

## 功能

- 多 Token 并发搜索，突破 GitHub 速率限制
- 自动验证密钥有效性 + 查询可用模型列表 + 余额查询
- 日期分片搜索，突破单查询 1000 条上限
- 支持 Star 筛选（高星仓库 / 低星仓库）
- 支持排序方式选择（最新提交 / 最佳匹配）
- 结果导出 JSON + CSV

## 安装

```bash
pip install -r requirements.txt
```

## 使用

### 交互模式（推荐）

```bash
python APIKey_leak.py
```

按提示 4 步完成配置：
1. 输入 GitHub Token（支持多 Token 并发）
2. 选择目标厂商
3. 设置搜索范围（1~10，范围越大越慢）
4. 选择排序/筛选方式

### 命令行模式

```bash
python APIKey_leak.py --token "ghp_xxx,ghp_yyy" --providers OPENAI DEEPSEEK --start-page 1 --end-page 3 --days 7 --no-interactive
```

| 参数 | 说明 |
|------|------|
| `--token` | GitHub Token，多个逗号分隔 |
| `--providers` | 厂商，如 OPENAI DEEPSEEK |
| `--start-page` / `--end-page` | 页码范围 |
| `--days` | 搜索最近 N 天，默认 7 |
| `--sort` | 排序字段 `indexed`，留空=最佳匹配 |
| `--order` | 排序方向 `desc` / `asc` |
| `--stars` | Star 筛选，如 `>50` 或 `<5` |
| `--output` | 输出 JSON 路径 |
| `--csv` | 输出 CSV 路径 |
| `--no-interactive` | 纯自动模式，跳过交互 |

### 获取 GitHub Token

https://github.com/settings/tokens → 创建 classic token，无需勾选任何权限。

## 排序/筛选说明

| 选项 | 效果 |
|------|------|
| 最新提交 | 按索引时间降序 |
| 最多Star | 只看 Star > 50 的仓库 |
| 最少Star | 只看 Star < 5 的仓库 |
| 最佳匹配 | GitHub 默认相关度排序 |

## 免责声明

仅限授权的安全研究、渗透测试和教育用途。使用者自行承担所有法律责任。
