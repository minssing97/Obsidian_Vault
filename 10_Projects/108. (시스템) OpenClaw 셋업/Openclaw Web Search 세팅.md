---
aliases:
  - openclaw web search 세팅
tags:
  - openclaw
  - websearch
---
https://chatgpt.com/c/69a3f994-5dac-83a7-ac3e-d9b5d8c0a9ea
## docker-compose.yml 파일
### 'gemini-2.5-flash'이렇게 안 쓰고 'gemini 2.5 flash' 쓰면 안됨

{
  "tools": {
    "web": {
      "search": {
        "enabled": true,
        "provider": "<font color="#ff0000">gemini</font>",
        "gemini": {
          "model": "<font color="#ff0000">gemini-2.5-flash</font>"
        }
      }
    }
  }
}

![[Pasted image 20260301183908.png]]