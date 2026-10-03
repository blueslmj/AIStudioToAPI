# API 使用示例

本文档提供了简要的 API 使用示例，包括 OpenAI 兼容 API、Gemini 原生 API 和 Anthropic 兼容 API 格式。

## 🤖 OpenAI 兼容 API

```bash
curl -X POST http://localhost:7860/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer your-api-key-1" \
  -d '{
    "model": "gemini-flash-lite-latest",
    "messages": [
      {
        "role": "user",
        "content": "你好，最近怎么样？"
      }
    ],
    "stream": false
  }'
```

### 🌊 使用流式响应

```bash
curl -X POST http://localhost:7860/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer your-api-key-1" \
  -d '{
    "model": "gemini-flash-lite-latest",
    "messages": [
      {
        "role": "user",
        "content": "写一首关于秋天的诗"
      }
    ],
    "stream": true
  }'
```

### 🖼️ 生成图片 [官方文档](https://ai.google.dev/gemini-api/docs/image-generation?hl=zh-cn)

```bash
curl -X POST http://localhost:7860/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer your-api-key-1" \
  -d '{
    "model": "gemini-2.5-flash-image",
    "messages": [
      {
        "role": "user",
        "content": "生成一只小猫"
      }
    ],
    "stream": false
  }'
```

#### 🫗 流式生成

```bash
curl -X POST http://localhost:7860/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer your-api-key-1" \
  -d '{
    "model": "gemini-2.5-flash-image",
    "messages": [
      {
        "role": "user",
        "content": "生成一只小猫"
      }
    ],
    "stream": true
  }'
```

### 📐 文本嵌入 [官方文档](https://ai.google.dev/gemini-api/docs/embeddings?hl=zh-cn)

```bash
curl -X POST http://localhost:7860/v1/embeddings \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer your-api-key-1" \
  -d '{
    "model": "gemini-embedding-001",
    "input": "什么是人工智能？"
  }'
```

### 💬 Responses API

```bash
curl -X POST http://localhost:7860/v1/responses \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer your-api-key-1" \
  -d '{
    "model": "gemini-flash-lite-latest",
    "input": "请用三句话总结函数式编程的核心思想。",
    "stream": false
  }'
```

#### 🌊 流式 Responses API

```bash
curl -X POST http://localhost:7860/v1/responses \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer your-api-key-1" \
  -d '{
    "model": "gemini-flash-lite-latest",
    "input": [
      {
        "role": "user",
        "content": [
          {
            "type": "input_text",
            "text": "写一首关于秋天的短诗。"
          }
        ]
      }
    ],
    "stream": true
  }'
```

## ♊ Gemini 原生 API 格式

```bash
curl -X POST http://localhost:7860/v1beta/models/gemini-flash-lite-latest:generateContent \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer your-api-key-1" \
  -d '{
    "contents": [
      {
        "role": "user",
        "parts": [
          {
            "text": "你好，最近怎么样？"
          }
        ]
      }
    ]
  }'
```

### 🌊 使用流式响应

```bash
curl -X POST http://localhost:7860/v1beta/models/gemini-flash-lite-latest:streamGenerateContent?alt=sse \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer your-api-key-1" \
  -d '{
    "contents": [
      {
        "role": "user",
        "parts": [
          {
            "text": "写一首关于秋天的诗"
          }
        ]
      }
    ]
  }'
```

### 🖼️ 生成图片 [官方文档](https://ai.google.dev/gemini-api/docs/image-generation?hl=zh-cn)

```bash
curl -X POST http://localhost:7860/v1beta/models/gemini-2.5-flash-image:generateContent \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer your-api-key-1" \
  -d '{
    "contents": [
      {
        "role": "user",
        "parts": [
          {
            "text": "生成一只小猫"
          }
        ]
      }
    ]
  }'
```

#### 🫗 流式生成

```bash
curl -X POST http://localhost:7860/v1beta/models/gemini-2.5-flash-image:streamGenerateContent?alt=sse \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer your-api-key-1" \
  -d '{
    "contents": [
      {
        "role": "user",
        "parts": [
          {
            "text": "生成一只小猫"
          }
        ]
      }
    ]
  }'
```

### 🎵 Lyria 音乐生成 [官方文档](https://ai.google.dev/gemini-api/docs/music-generation?hl=zh-cn)

#### 生成 30 秒音乐片段

```bash
curl -X POST http://localhost:7860/v1beta/models/lyria-3-clip-preview:generateContent \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer your-api-key-1" \
  -d '{
    "contents": [
      {
        "parts": [
          {
            "text": "创作一首 30 秒的欢快原声民谣，使用吉他和口琴。"
          }
        ]
      }
    ]
  }'
```

#### 生成完整歌曲

```bash
curl -X POST http://localhost:7860/v1beta/models/lyria-3.5:generateContent \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer your-api-key-1" \
  -d '{
    "contents": [
      {
        "parts": [
          {
            "text": "创作一首关于归途的史诗电影配乐，以钢琴独奏开场，逐渐加入弦乐，并在结尾达到高潮。"
          }
        ]
      }
    ]
  }'
```

### 🎧 音频转写 [官方文档](https://ai.google.dev/gemini-api/docs/transcribe?hl=zh-cn)

```bash
curl -X POST http://localhost:7860/v1beta/models/gemini-3.5-transcribe:generateContent \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer your-api-key-1" \
  -d '{
    "contents": [
      {
        "parts": [
          {
            "fileData": {
              "fileUri": "YOUR_FILE_URI",
              "mimeType": "audio/mp3"
            }
          }
        ]
      }
    ]
  }'
```

### 🎤 TTS 语音合成 [官方文档](https://ai.google.dev/gemini-api/docs/speech-generation?hl=zh-cn)

#### 基础 TTS（默认声音）

```bash
curl -X POST http://localhost:7860/v1beta/models/gemini-2.5-flash-preview-tts:generateContent \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer your-api-key-1" \
  -d '{
    "contents": [
      {
        "role": "user",
        "parts": [
          {
            "text": "你好，这是一个语音合成测试。"
          }
        ]
      }
    ],
    "generationConfig": {
      "responseModalities": ["AUDIO"]
    }
  }'
```

#### 指定声音

可选声音：`Kore`、`Puck`、`Charon`、`Fenrir`、`Aoede`

```bash
curl -X POST http://localhost:7860/v1beta/models/gemini-2.5-flash-preview-tts:generateContent \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer your-api-key-1" \
  -d '{
    "contents": [
      {
        "role": "user",
        "parts": [
          {
            "text": "你好，这是一个语音合成测试。"
          }
        ]
      }
    ],
    "generationConfig": {
      "responseModalities": ["AUDIO"],
      "speechConfig": {
        "voiceConfig": {
          "prebuiltVoiceConfig": {
            "voiceName": "Kore"
          }
        }
      }
    }
  }'
```

#### 多人对话

对话内容写在 prompt 中，使用 `multiSpeakerVoiceConfig` 配置多个说话者的声音（最多 2 个）。

```bash
curl -X POST http://localhost:7860/v1beta/models/gemini-2.5-flash-preview-tts:generateContent \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer your-api-key-1" \
  -d '{
    "contents": [
      {
        "role": "user",
        "parts": [
          {
            "text": "TTS the following conversation between Joe and Jane:\nJoe: How are you today Jane?\nJane: I am doing great, thanks for asking!"
          }
        ]
      }
    ],
    "generationConfig": {
      "responseModalities": ["AUDIO"],
      "speechConfig": {
        "multiSpeakerVoiceConfig": {
          "speakerVoiceConfigs": [
            {
              "speaker": "Joe",
              "voiceConfig": {
                "prebuiltVoiceConfig": {
                  "voiceName": "Charon"
                }
              }
            },
            {
              "speaker": "Jane",
              "voiceConfig": {
                "prebuiltVoiceConfig": {
                  "voiceName": "Kore"
                }
              }
            }
          ]
        }
      }
    }
  }'
```

> 💡 **提示**：TTS 响应返回的是 `audio/L16;codec=pcm;rate=24000` 格式的 base64 编码音频数据，需要解码后转换为 WAV 格式播放。

### 📐 文本嵌入 (Embeddings) [官方文档](https://ai.google.dev/gemini-api/docs/embeddings?hl=zh-cn)

使用 `embedContent` 或 `batchEmbedContents` 端点生成文本嵌入向量。

#### 单个文本嵌入

```bash
curl -X POST http://localhost:7860/v1beta/models/gemini-embedding-001:embedContent \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer your-api-key-1" \
  -d '{
    "model": "models/gemini-embedding-001",
    "content": {
      "parts": [
        {
          "text": "什么是人工智能？"
        }
      ]
    }
  }'
```

#### 单条 batch 文本嵌入

```bash
curl -X POST http://localhost:7860/v1beta/models/gemini-embedding-001:batchEmbedContents \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer your-api-key-1" \
  -d '{
    "requests": [
      {
        "model": "models/gemini-embedding-001",
        "content": {
          "parts": [
            {
              "text": "什么是人工智能？"
            }
          ]
        }
      }
    ]
  }'
```

#### 批量文本嵌入

```bash
curl -X POST http://localhost:7860/v1beta/models/gemini-embedding-001:batchEmbedContents \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer your-api-key-1" \
  -d '{
    "requests": [
      {
        "model": "models/gemini-embedding-001",
        "content": {
          "parts": [
            {
              "text": "什么是人工智能？"
            }
          ]
        }
      },
      {
        "model": "models/gemini-embedding-001",
        "content": {
          "parts": [
            {
              "text": "机器学习和深度学习有什么区别？"
            }
          ]
        }
      }
    ]
  }'
```

## 👤 Anthropic 兼容 API

```bash
curl -X POST http://localhost:7860/v1/messages \
  -H "Content-Type: application/json" \
  -H "x-api-key: your-api-key-1" \
  -H "anthropic-version: 2023-06-01" \
  -d '{
    "model": "gemini-flash-lite-latest",
    "max_tokens": 1024,
    "messages": [
      {
        "role": "user",
        "content": "你好，最近怎么样？"
      }
    ],
    "stream": false
  }'
```

### 🌊 使用流式响应

```bash
curl -X POST http://localhost:7860/v1/messages \
  -H "Content-Type: application/json" \
  -H "x-api-key: your-api-key-1" \
  -H "anthropic-version: 2023-06-01" \
  -d '{
    "model": "gemini-flash-lite-latest",
    "max_tokens": 1024,
    "messages": [
      {
        "role": "user",
        "content": "写一首关于秋天的诗"
      }
    ],
    "stream": true
  }'
```
