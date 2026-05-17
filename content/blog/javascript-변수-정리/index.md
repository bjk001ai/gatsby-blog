---
title: "JavaScript 변수 정리 - var, let, const 완벽 정리"
date: "2026-05-17"
description: "자바스크립트 변수 선언 방식인 var, let, const의 차이를 예제와 함께 완벽하게 정리합니다."
---

## 들어가며

자바스크립트를 처음 배우면 변수 선언 방식이 세 가지나 있어서 헷갈리기 쉽습니다.
`var`, `let`, `const` — 각각 언제 써야 할까요? 이 글에서 완벽하게 정리해드립니다!

---

## 한눈에 비교

| 구분 | var | let | const |
|------|-----|-----|-------|
| 스코프 | 함수 스코프 | 블록 스코프 | 블록 스코프 |
| 재선언 | ✅ 가능 | ❌ 불가 | ❌ 불가 |
| 재할당 | ✅ 가능 | ✅ 가능 | ❌ 불가 |
| 호이스팅 | ✅ 발생 | ⚠️ TDZ | ⚠️ TDZ |

---

## var — 쓰지 마세요 🚫

`var`는 자바스크립트 초창기부터 있던 변수 선언 방식입니다.
하지만 여러 문제점 때문에 요즘은 거의 사용하지 않아요.

### 문제점 1 — 재선언이 가능해서 실수하기 쉬움

\`\`\`javascript
var name = "철수";
var name = "영희"; // 재선언해도 에러 없음 😱
console.log(name); // "영희"
\`\`\`

### 문제점 2 — 함수 스코프라 블록 밖에서도 접근 가능

\`\`\`javascript
if (true) {
  var age = 20;
}
console.log(age); // 20 — 블록 밖에서도 접근됨 😱
\`\`\`

### 문제점 3 — 호이스팅으로 undefined 발생

\`\`\`javascript
console.log(score); // undefined (에러가 아님!)
var score = 100;
\`\`\`

---

## let — 재할당이 필요할 때 ✅

`let`은 ES6(2015)에서 등장한 블록 스코프 변수입니다.
값이 바뀔 수 있는 변수에 사용해요.

\`\`\`javascript
let count = 0;

count = 1; // 재할당 가능 ✅
count = 2; // 재할당 가능 ✅

let count = 3; // ❌ SyntaxError: 재선언 불가
\`\`\`

### 블록 스코프 예시

\`\`\`javascript
if (true) {
  let message = "안녕하세요";
  console.log(message); // "안녕하세요" ✅
}
console.log(message); // ❌ ReferenceError: 블록 밖 접근 불가
\`\`\`

---

## const — 기본값으로 사용 🏆

`const`는 한번 선언하면 재할당이 불가능한 상수입니다.
요즘은 **기본적으로 const를 사용**하고, 재할당이 필요할 때만 let으로 바꾸는 방식을 권장해요.

\`\`\`javascript
const PI = 3.14;
PI = 3.15; // ❌ TypeError: 재할당 불가
\`\`\`

### ⚠️ 주의 — 객체/배열은 내부 변경 가능

\`\`\`javascript
const user = { name: "철수", age: 20 };
user.age = 21; // ✅ 내부 프로퍼티 변경은 가능!
user = {}; // ❌ 재할당은 불가
\`\`\`

---

## 실전에서 이렇게 써요

\`\`\`javascript
// 1. 기본적으로 const 사용
const API_URL = "https://api.example.com";
const userInfo = { name: "철수", age: 20 };

// 2. 값이 바뀌어야 하면 let
let currentPage = 1;
currentPage += 1;

// 3. var는 사용하지 않음 🚫
var oldWay = "쓰지 마세요";
\`\`\`

---

## 결론 💡

> **const를 기본으로, 재할당 필요하면 let, var는 절대 사용하지 말 것!**

| 상황 | 선택 |
|------|------|
| 값이 절대 안 바뀜 | `const` |
| 값이 바뀔 수 있음 | `let` |
| 레거시 코드 유지보수 | `var` (어쩔 수 없을 때만) |

---

## 참고 자료

- [MDN - var](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/var)
- [MDN - let](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/let)
- [MDN - const](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/const)