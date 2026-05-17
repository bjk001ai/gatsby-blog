---
title: "악명 높은 CORS 개념 & 해결법 완벽 정리 🌐"
date: "2026-05-15"
description: "웹 개발자라면 누구나 한번쯤 만나는 CORS 에러, 원인과 해결법을 완벽하게 정리합니다."
---

## 들어가며

웹 개발을 하다 보면 반드시 만나는 에러가 있습니다.

\`\`\`
Access to fetch at 'https://api.example.com' from origin 
'http://localhost:3000' has been blocked by CORS policy
\`\`\`

바로 **CORS 에러**입니다. 오늘 이 에러를 완벽하게 이해하고 해결해봐요!

---

## CORS란?

**CORS (Cross-Origin Resource Sharing)** 는 브라우저가 다른 출처의 리소스를 요청할 때 적용되는 보안 정책입니다.

### Origin(출처)이란?

\`\`\`
https://www.example.com:443/path

Protocol: https
Host: www.example.com  
Port: 443
\`\`\`

> Protocol + Host + Port 세 가지가 모두 같아야 **같은 출처**예요!

### 같은 출처 vs 다른 출처

\`\`\`
기준: https://www.example.com

✅ 같은 출처: https://www.example.com/about
❌ 다른 출처: http://www.example.com (Protocol 다름)
❌ 다른 출처: https://api.example.com (Host 다름)
❌ 다른 출처: https://www.example.com:8080 (Port 다름)
\`\`\`

---

## 왜 CORS가 필요할까?

CORS는 **SOP(Same-Origin Policy, 동일 출처 정책)** 때문에 생겼어요.

SOP가 없다면 악성 사이트에서 내 은행 사이트 API를 마음대로 호출할 수 있어요. 이를 막기 위해 브라우저가 다른 출처 요청을 기본적으로 차단합니다.

\`\`\`
악성사이트(evil.com) → 내 은행 API(bank.com/api) 호출 시도
→ 브라우저가 CORS 정책으로 차단! 🛡️
\`\`\`

---

## CORS 동작 방식

### 단순 요청 (Simple Request)

GET, POST 등 조건을 만족하면 바로 요청을 보내요.
서버가 응답 헤더에 `Access-Control-Allow-Origin`을 포함하면 OK!

\`\`\`
브라우저 → 서버: "나 example.com인데 데이터 줄 수 있어?"
서버 → 브라우저: "응, Access-Control-Allow-Origin: * 허용해"
브라우저: OK ✅
\`\`\`

### 예비 요청 (Preflight Request)

PUT, DELETE나 커스텀 헤더가 있는 요청은 먼저 **OPTIONS** 요청으로 허용 여부를 확인해요.

\`\`\`
브라우저 → 서버: OPTIONS 요청 (이런 요청 해도 돼?)
서버 → 브라우저: 허용 목록 응답
브라우저 → 서버: 실제 요청 전송
\`\`\`

---

## CORS 해결법

### 방법 1 — 서버에서 헤더 설정 (가장 정석) ✅

\`\`\`javascript
// Node.js Express 예시
app.use((req, res, next) => {
  res.header("Access-Control-Allow-Origin", "*"); // 모든 출처 허용
  res.header("Access-Control-Allow-Methods", "GET, POST, PUT, DELETE");
  res.header("Access-Control-Allow-Headers", "Content-Type, Authorization");
  next();
});
\`\`\`

\`\`\`javascript
// cors 패키지 사용 (더 간편)
const cors = require('cors');
app.use(cors({
  origin: 'http://localhost:3000' // 특정 출처만 허용
}));
\`\`\`

---

### 방법 2 — 프록시 서버 사용

\`\`\`javascript
// package.json에 proxy 설정 (React)
{
  "proxy": "http://api.example.com"
}

// 이제 /api/data로 요청하면 자동으로 프록시됨
fetch('/api/data')
\`\`\`

---

### 방법 3 — Nginx 프록시 설정

\`\`\`nginx
server {
  location /api/ {
    proxy_pass http://api.example.com/;
    add_header Access-Control-Allow-Origin *;
  }
}
\`\`\`

---

## 자주 하는 실수 ⚠️

### 1. 브라우저 익스텐션으로 해결하려는 것
개발 중에만 임시방편으로 쓸 수 있지만, 실제 서비스엔 적용 불가예요.

### 2. `Access-Control-Allow-Origin: *` 남용
모든 출처를 허용하면 보안에 취약해져요. 특정 도메인만 허용하는 게 좋아요.

\`\`\`javascript
// ❌ 보안에 취약
res.header("Access-Control-Allow-Origin", "*");

// ✅ 특정 도메인만 허용
res.header("Access-Control-Allow-Origin", "https://www.mysite.com");
\`\`\`

---

## 결론 💡

> **CORS는 브라우저의 보안 정책이라 서버에서 해결해야 해요!**

| 상황 | 해결법 |
|------|--------|
| 내가 서버 제어 가능 | 서버에서 CORS 헤더 설정 |
| 서버 제어 불가 | 프록시 서버 사용 |
| 개발 중 임시 | 프록시 설정 (package.json) |

CORS를 이해하면 웹 개발이 한층 더 편해집니다 😊