# poe-to-gpt

一个转换器，可以将 POE 提供的 API 令牌转换为 OpenAI 的 API 格式，从而使依赖于 OpenAI API 的其他应用程序可以使用 POE 的 API。

这是一个工具，将 Poe官方网站提供的 API 密钥转换为兼容的 OpenAI API 密钥。它使 Poe API 密钥可以与依赖于 OpenAI API 密钥的工具一起使用。开发此工具的主要原因是为中国大陆用户提供便利和稳定性，因为他们发现订阅和充值 OpenAI API 不太方便。

请注意，目前**仅限 Poe 订阅者访问 API 密钥**。

poe 订阅者获取API key地址：[https://poe.com/api_key](https://poe.com/api_key)

## 安装

### 更改配置文件

```bash
vim config.toml
```

### 编写docker compose并运行

```yml
services:
  poe-to-gpt:
    image: a15355447898a/poe-to-gpt:latest
    container_name: poe-to-gpt
    ports:
      - "3700:3700"
    volumes:
      - ./config.toml:/app/config.toml
    restart: unless-stopped
```

```bash
# 启动容器，默认运行在端口 3700
docker-compose up -d
```

## 使用

请查看 [OpenAI 文档](https://platform.openai.com/docs/api-reference/chat/create) 以获取有关如何使用 ChatGPT API 的更多详细信息。

只需在您的代码中将 `https://api.openai.com` 替换为 `http://localhost:3700` 即可开始使用。

> 注意：请务必输入自定义 API 密钥（对应字段为 `config.toml` 中的 `accessTokens` ）

支持的路由：

- /chat/completions
- /v1/chat/completions

## 支持的模型参数（对应poe上机器人名称）。

> 传参可忽略大小写

GPT-3.5-Turbo

GPT-4o-Mini

ChatGPT-4o-Latest

o1

o1-mini

o1-preview

o3-mini 

o3-mini-high

Claude-3.5-Sonnet

Claude-3.5-Haiku

Claude-3-opus

Gemini-2.0-Flash

Gemini-1.5-Pro

Gemini-1.5-Pro-Search

DeepSeek-R1

DALL-E-3
