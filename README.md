# Load Testing Platform

AI-native distributed load testing platform with scenario auto-generation, intelligent result analysis, and seamless Kubernetes integration — closing the gap between "test ran" and "root cause found."

## The Problem

Load testing is broken in practice:

- **Scenario creation is tedious** — most teams skip it entirely, running only smoke tests
- **Result analysis is manual** — tools produce percentile distributions but not actionable diagnosis
- **Distributed execution adds operational complexity** — no open-source tool provides Kubernetes operator support
- **No tracing integration** — linking test ramp-up to downstream service degradation requires manual correlation

The research gap: existing tools produce data; none synthesize it into recommendations. This is why 70% of development teams run less than adequate performance tests.

## What This Does

### Scenario Generation (AI-Native)
- **Auto-generate from OpenAPI specs** — LLM reads endpoint definitions, infers realistic user journeys
- **HAR file recording** — capture production traffic patterns, auto-convert to load test scenarios
- **Natural language descriptions** — "simulate 500 checkout users with 10s think time, ramping up over 5 minutes"
- **No manual scripting required** — the most labor-intensive step automated away

### Result Analysis (AI-Native)
- **Plain-language summaries** — "checkout service degraded 35ms per 100 concurrent users; bottleneck is the database query at line 47 of OrderService.java"
- **Anomaly detection** — identifies bimodal latency distributions, sudden p99 spikes
- **Bottleneck hypothesis generation** — "given test results + architecture description, here are ranked hypotheses with validation steps"
- **Regression detection** — compare against historical baselines with statistical significance testing

### Distributed Execution
- **Kubernetes-native** — ephemeral test worker pods via Operator
- **AWS Lambda support** — serverless scale-out without infrastructure
- **Cost tracking** — see what each test costs to run
- **Real-time observability** — integrate with OpenTelemetry for trace correlation during tests

### Trace Correlation
- **Link test requests to distributed traces** — see the exact service/database that became the bottleneck
- **Latency attribution** — not just "API was slow" but "order-service → payment-gateway call latency increased due to connection pool exhaustion on payment-db"

## Key Differentiators

| Feature | This Platform | k6 | Apache JMeter | Gatling | Artillery | NeoLoad |
|---------|---|---|---|---|---|---|
| **Scenario auto-gen** | ✓ (AI from OpenAPI/HAR) | — | — | — | — | (Manual GUI) |
| **Result analysis** | ✓ (LLM narration) | — | — | — | — | (AI-assisted) |
| **Trace correlation** | ✓ (Native OTEL) | Grafana plugin | No | No | No | (APM integration) |
| **Kubernetes operator** | ✓ | Cloud only | Manual | Enterprise only | No | No |
| **Open source** | ✓ | ✓ (AGPL) | ✓ | ✓ Community | ✓ (MPL) | — |
| **Language support** | JavaScript/YAML | JavaScript | XML/GUI | Java/Scala/JS | YAML/JS | GUI/Java |

## Market & Opportunity

- **Market size**: $255M (2026) → $464M (2035) at 6.8% CAGR (broader market $1.4B → $4.7B)
- **AI-augmented subset**: $1.01B (2025) → $4.64B (2034) at 18.3% CAGR
- **Buyers**: QA/SDET engineers, SREs, platform engineers, development teams
- **Open-source gap**: No OSS tool provides scenario generation + intelligent analysis + Kubernetes native execution

## Research Foundation

- **Traditional test automation coverage plateaued at 25%** — AI is the only viable path to break the ceiling
- **Gartner launched inaugural Magic Quadrant for AI Augmented Software Testing (Oct 2025)**
- **Forrester renamed category to "Autonomous Testing Platforms"** (Q3 2025)
- **70% of enterprises projected to integrate AI-augmented testing by 2028** (vs. 20% in early 2025)

## Quick Start

```bash
# Generate scenario from OpenAPI spec
load-test scenario-gen --openapi=checkout-api.yaml --output scenario.js

# Or record from production HAR
load-test scenario-from-har --har=production-traffic.har --sample=100

# Run distributed load test
load-test run scenario.js \
  --duration=10m \
  --ramp-up=2m \
  --kubernetes=my-cluster \
  --trace-backend=tempo

# Analyze with AI insights
load-test analyze --results=run-123 --summary
# → "Checkout service degraded 35ms per 100 concurrent users; bottleneck is the database query at line 47"
```

## Target Users

1. **QA/SDET Engineers** — scenario generation removes tedium; sophisticated assertions built-in
2. **SREs** — capacity planning, SLO validation, pre-deployment sign-off
3. **Platform/DevOps Teams** — Kubernetes-native execution, cloud cost attribution
4. **Development Teams** — shift-left performance testing in the CI/CD pipeline
5. **Startups** — zero licensing cost, cloud-efficient execution

## Related Standards

- ISO/IEC 25010 — Software Quality Model with performance efficiency sub-characteristics
- ISTQB Certified Tester — Performance Testing (CT-PT) certification curriculum
- Core Web Vitals (Google/W3C) — user-centric performance metrics (LCP, INP, CLS)
- Google SRE Practices — quantifying confidence through stress testing beyond rated capacity

---

Built on research from ICPE 2020 (microservices performance testing challenges) and LTB 2024 workshop on emerging AI-native testing. [Read the full research](./research.md) | [Feature roadmap](./features.md)
