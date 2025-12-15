# 🚀 AI-Powered Self-Healing Playwright Automation Framework

> **Enterprise-Grade End-to-End Test Automation using Playwright, TypeScript & AI (LLMs)**

---

## 📌 Overview

Modern web applications evolve rapidly. UI changes such as updated IDs, modified DOM structures, or redesigned components often cause **automation test failures**, leading to flaky tests, broken CI pipelines, and high maintenance overhead.

This project introduces an **AI-powered Self-Healing Test Automation Framework** built using **Playwright + TypeScript**, designed to **automatically detect, heal, and recover from locator failures at runtime** using **LLM-based reasoning**.

The framework is **resume-ready, production-quality, and interview-defensible**, demonstrating strong **SDET / QA Automation expertise**, scalable architecture, CI/CD readiness, and **practical AI integration**.

---

## 🎯 Project Goals

The primary objective of this framework is to:

- Detect broken UI locators dynamically at runtime
- Heal selectors automatically using AI/LLM reasoning
- Retry failed test steps with healed locators
- Persist updated selectors for future executions
- Reduce flaky tests and manual maintenance
- Improve CI stability and trust in automation results

---

## ❗ Problem Statement

Traditional test automation frameworks:

- Fail immediately when locators change
- Require frequent manual updates
- Produce flaky results due to async UI behavior
- Break CI/CD pipelines
- Increase long-term maintenance cost

### ✅ Solution

This framework **adapts dynamically instead of failing fast**, by introducing an **AI Self-Healing Layer** on top of Playwright.

---

## 🧠 High-Level Architecture

```

Test Layer (E2E Specs)
↓
Page Object Layer (UI Actions)
↓
Smart Locator Resolver
↓
AI Self-Healing Engine
↓
Utilities / Config / Logging / Reporting

```

Each layer is **independent, testable, and scalable**, following **clean architecture and separation of concerns**.

---

## 📁 Project Structure

```

ai-self-healing-playwright/
│
├── src/
│   ├── tests/
│   │   └── e2e/
│   │       ├── login.spec.ts
│   │       ├── checkout.spec.ts
│   │       └── user-flow.spec.ts
│   │
│   ├── pages/
│   │   ├── BasePage.ts
│   │   ├── LoginPage.ts
│   │   └── DashboardPage.ts
│   │
│   ├── locators/
│   │   ├── login.locators.json
│   │   └── dashboard.locators.json
│   │
│   ├── ai/
│   │   ├── HealingEngine.ts
│   │   ├── LocatorAnalyzer.ts
│   │   ├── LLMClient.ts
│   │   └── HealingStrategy.ts
│   │
│   ├── core/
│   │   ├── TestSetup.ts
│   │   ├── RetryHandler.ts
│   │   └── PlaywrightHooks.ts
│   │
│   ├── utils/
│   │   ├── Logger.ts
│   │   ├── DomSnapshot.ts
│   │   ├── FileUtils.ts
│   │   └── EnvLoader.ts
│   │
│   └── config/
│       ├── playwright.config.ts
│       ├── env.dev.ts
│       ├── env.qa.ts
│       └── env.prod.ts
│
├── reports/
│   ├── allure-results/
│   └── html-report/
│
├── .github/workflows/
│   └── playwright-ci.yml
│
├── package.json
├── tsconfig.json
├── README.md
└── .env

````

---

## 🧩 Module Responsibilities

### 1️⃣ Test Layer (E2E Specs)

- Contains **only business workflows**
- Uses **Page Objects exclusively**
- No locators or Playwright low-level APIs
- Clean, readable, scenario-driven tests

```ts
test('User login flow', async ({ page }) => {
  const login = new LoginPage(page);
  await login.login('user', 'password');
});
````

---

### 2️⃣ Page Object Layer

* Encapsulates all UI actions
* Uses **smart locator resolver**
* Never fails immediately on missing locators
* Exposes methods like:

  * `smartClick`
  * `smartFill`
  * `smartWait`

---

### 3️⃣ Smart Locator Management

* Locators stored in JSON files
* Each element supports:

  * One primary selector
  * Multiple fallback selectors
* Locators are **updated automatically after healing**

```json
{
  "loginButton": {
    "primary": "#login-btn",
    "fallbacks": [
      "button:has-text('Login')",
      "//button[contains(text(),'Login')]"
    ]
  }
}
```

---

### 4️⃣ AI Self-Healing Engine (Core Feature)

The self-healing engine activates when Playwright throws:

* `Element not found`
* `Timeout exceeded`
* `Strict mode violation`

#### Mandatory Healing Flow

1. Capture failed selector
2. Capture DOM snapshot
3. Extract element context (tag, text, attributes)
4. Send structured prompt to LLM
5. Receive 3–5 alternative selectors
6. Validate selectors in browser
7. Select the best working locator
8. Update locator JSON automatically
9. Retry the failed action
10. Log healing event and outcome

---

### 5️⃣ LLM Integration

* Pluggable LLM client architecture
* Supports:

  * OpenAI
  * Azure OpenAI
  * Local LLMs (Ollama, LM Studio)

#### Prompt Strategy

* Prefer accessibility-based selectors
* Prefer stable attributes (`aria-*`, `role`, `data-*`)
* Avoid brittle XPath
* Return Playwright-compatible selectors only

---

### 6️⃣ Retry & Stability Engine

* No blind retries
* Retry **only after healing**
* Track flaky behavior over time
* Prevent infinite retry loops

---

### 7️⃣ Logging & Reporting

#### Logging

* Structured JSON logging
* Separate AI-healing logs
* Logs include:

  * Original selector
  * Healed selector
  * Confidence score
  * Retry result

#### Reporting

* Allure report integration
* Screenshots on failure
* Video recordings for retries
* Healed steps clearly marked in reports

---

## 🔄 Execution Flow

```
Test Step
 → Locator Lookup
 → Action Attempt
 → Failure Detected
 → AI Healing Engine
 → Locator Validation
 → Retry Action
 → Test Continues
```

---

## ⚙️ Tech Stack

| Category       | Technology                        |
| -------------- | --------------------------------- |
| Language       | TypeScript, JavaScript            |
| Automation     | Playwright                        |
| AI             | OpenAI / Azure OpenAI / Local LLM |
| Design Pattern | Page Object Model                 |
| Reporting      | Allure                            |
| CI/CD          | GitHub Actions                    |
| Logging        | Winston / Custom Logger           |
| Config         | dotenv, tsconfig                  |

---

## 🧪 Sample E2E Scenarios

* User Login → Dashboard Navigation
* User Registration Flow
* Checkout & Payment Flow
* Role-Based Access Validation
* Cross-Browser Execution

---

## 🚦 CI/CD Pipeline

* GitHub Actions workflow
* Triggered on PR & main branch
* Parallel execution
* Upload test reports, screenshots, videos
* Build fails **only if healing fails**

---

## 🏆 Best Practices Followed

* Clean architecture
* SOLID principles
* Zero hard-coded selectors
* Environment isolation
* AI used **only when failures occur**
* Enterprise-grade observability
* Interview-ready, maintainable codebase

---

## 📌 Resume Impact Statement

> Designed and implemented an AI-powered self-healing Playwright automation framework using TypeScript, enabling automatic recovery from UI locator failures, reducing test maintenance effort and significantly improving CI pipeline stability.

---

## 📬 Next Enhancements (Optional)

* Visual AI comparison
* Historical flaky test analytics
* Confidence-based healing approval
* Dashboard for healing metrics

---

## 👨‍💻 Author

**SDET / QA Automation Engineer**
Focused on scalable test architecture, CI/CD stability, and AI-driven automation solutions.
