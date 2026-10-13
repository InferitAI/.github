<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./inferit-lockup-reverse-2400w.png">
  <img alt="The Inferit logo: a black postage stamp printed 1µ, with an orange µ, in front of a grey sibling stamp, next to the word inferit." src="./inferit-lockup-2400w.png" width="300">
</picture>

# Inferit

**The peer-to-peer market for AI inference.**

Anyone can sell inference for any model, at their own price. Buyers and agents pay per request, and each request goes to the cheapest healthy seller on Inferit.

[![Website](https://img.shields.io/badge/inferit.cc-website-141414?labelColor=6B6D71)](https://inferit.cc)
[![App](https://img.shields.io/badge/inferit.app-open%20the%20app-141414?labelColor=6B6D71)](https://inferit.app)
[![Docs](https://img.shields.io/badge/docs-inferit.cc%2Fdocs-141414?labelColor=6B6D71)](https://inferit.cc/docs)
[![npm](https://img.shields.io/npm/v/inferit-seller?label=inferit-seller&color=141414&labelColor=6B6D71)](https://www.npmjs.com/package/inferit-seller)
[![X](https://img.shields.io/badge/X-%40inferit__-141414?logo=x&logoColor=ECEAE4&labelColor=6B6D71)](https://x.com/inferit_)
[![Status](https://img.shields.io/badge/status-testnet%20demo-141414?labelColor=6B6D71)](https://inferit.cc/docs/security-trust)

</div>

---

## Two ways in

| | **Buy** | **Sell** |
|---|---|---|
| Start | An API key from the [Buy workspace](https://inferit.app/buy), or x402 per request from a wallet, with no account and no API key | One command on your own computer, with a token from **Add a machine** in the [Sell workspace](https://inferit.app/sell) |
| What you run | Any OpenAI-compatible client: change the base URL and the key | Ollama, LM Studio, vLLM or llama.cpp. The app dials out, so you need no open port and no domain |
| Money | Per-token prices, charged per request in µ (micro-dollars). A key spends your balance under a ceiling you sign, with an expiry the contract enforces | Your own price per 1M tokens, paid per request to the payout wallet you register (test ITC on the testnet) |
| Guide | [Quickstart](https://inferit.cc/docs/quickstart) · [Agents and x402](https://inferit.cc/agents) | [Sell from your own PC](https://inferit.cc/docs/sellers/quickstart) |

### Buy with an API key

Create a key in the [Buy workspace](https://inferit.app/buy) and keep it in your environment as `INFERIT_API_KEY`.

```python
import os
from openai import OpenAI

client = OpenAI(
    base_url="https://api-production-c74b9.up.railway.app/v1",
    api_key=os.environ["INFERIT_API_KEY"],
)
response = client.chat.completions.create(
    model="qwen/qwen-2.5-14b-instruct",
    messages=[{"role": "user", "content": "Explain a spending cap in one sentence."}],
)
print(response.choices[0].message.content)
```

Name a model with a live offer ([inferit.app/models](https://inferit.app/models)), or send `model="auto"` and Inferit picks the model. Auto chooses among ranked models with a healthy seller that fit the request, weighing a published quality ranking (Artificial Analysis Intelligence Index, read 2026-10-06) against this request's price. It never reads the prompt, and the `x-inferit-model` header names the model that answered. When no ranked model has a healthy seller, auto answers `503 no_eligible_model` and nothing is charged; a named model keeps working. The method is on [inferit.cc/docs/routing](https://inferit.cc/docs/routing).

An agent can skip the key: a call with no key gets `402 Payment Required` with a quote; the agent signs the payment with an x402 v2 client and resends the same request. See [inferit.cc/agents.md](https://inferit.cc/agents.md).

### Sell from your own computer

```bash
npx -y inferit-seller connect --token icn_… && npx -y inferit-seller install-service
```

The app finds your local model server, matches its models to the catalog and runs as a background service that restarts after a reboot. Set your prices in the [Sell workspace](https://inferit.app/sell).

---

## Repositories

| Repository | What it is |
|---|---|
| [inferit-seller](https://github.com/InferitAI/inferit-seller) | Sell inference from your own computer with one command. Apache-2.0, on npm as `inferit-seller` |
| [whitechain-x402-facilitator](https://github.com/InferitAI/whitechain-x402-facilitator) | The first public x402 v2 facilitator for Whitechain, live on Whitechain Sepolia (testnet). Apache-2.0 |
| [inferit-examples](https://github.com/InferitAI/inferit-examples) | Runnable examples for LangChain, the Vercel AI SDK, LiteLLM, CrewAI and OpenCode, paying with an API key or x402 |
| [inferit-agent-example](https://github.com/InferitAI/inferit-agent-example) | A minimal TypeScript agent that pays Inferit per request with x402: no account and no API key |
| [model-catalog](https://github.com/InferitAI/model-catalog) | The models the Inferit API knows, as open data: ids, aliases, context windows and licence classes (CC BY 4.0) |
| [awesome-inferit](https://github.com/InferitAI/awesome-inferit) | Docs, guides, repositories and endpoints for Inferit, in one index |
| [awesome-x402-whitechain](https://github.com/InferitAI/awesome-x402-whitechain) | x402 resources for Whitechain: the spec, SDKs, EIP-3009, the testnet, facilitators and examples |
| [branding](https://github.com/InferitAI/branding) | The Inferit logo files, colours, type and usage rules |

Inferit runs the market API and the router; their code is private.

---

> **Status:** Testnet demo on Whitechain Sepolia. Prices settle in Inferit Test Credit (ITC), a test token with no monetary value. The contracts are not audited. Inferit has no token.

<div align="center">

**[Website](https://inferit.cc)** · **[App](https://inferit.app)** · **[Docs](https://inferit.cc/docs)** · **[API reference](https://inferit.cc/docs/api-reference)** · **[X](https://x.com/inferit_)**

</div>
