---
marp: true
theme: default
paginate: true
backgroundImage: url('https://marp.app/assets/hero-background.svg')
style: |
    section {
        background: 
            linear-gradient(135deg, rgba(245, 247, 250, 0.95) 0%, rgba(195, 207, 226, 0.95) 100%),
            repeating-linear-gradient(45deg, transparent, transparent 40px, rgba(59, 130, 246, 0.08) 40px, rgba(59, 130, 246, 0.08) 80px),
            repeating-linear-gradient(-45deg, transparent, transparent 40px, rgba(30, 64, 175, 0.05) 40px, rgba(203, 203, 218, 1) 80px);
        background-color: #ffffff;
        color: #2c3e50;
        font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
    }
    h1 {
        color: #1e3a8a;
        font-weight: 700;
        text-shadow: 1px 1px 2px rgba(0,0,0,0.1);
        border-bottom: 3px solid #3b82f6;
        padding-bottom: 0.3em;
    }
    h2 {
        color: #1e40af;
        font-weight: 600;
        border-left: 5px solid #3b82f6;
        padding-left: 0.5em;
    }
    strong {
        color: #dc2626;
        font-weight: 700;
    }
    code {
        background: rgba(59, 130, 246, 0.1);
        padding: 0.2em 0.4em;
        border-radius: 3px;
        color: #1e40af;
        border: 1px solid rgba(59, 130, 246, 0.2);
    }
    a {
        color: #2563eb;
        text-decoration: none;
        border-bottom: 1px solid #2563eb;
        transition: all 0.2s ease;
    }
    a:hover {
        color: #1e40af;
        border-bottom-color: #1e40af;
    }

    img {
      border: 2px solid #1e40af;
      box-shadow: 2px 2px;
      border-radius: 20px 20px;
    }
---

# Lecture 4: On-chain Agentic Payments
## _Dr. Stefano Balietti_  



<!-- (https://marp.app/assets/marp.svg) -->



---

# Warm-up 

![bg left:40% 80%](https://static0.gamerantimages.com/wordpress/wp-content/uploads/2022/09/James-Bond-Daniel-Craig-007.jpg)

<!-- (https://assets1.ignimgs.com/2020/10/31/0-signed-photo-of-sean-connery-posing-as-james-bond-1280x720-1604162798616.jpg)  -->

**What did we learn last week?**

- What is an agent?



<!-- An AI agent is a software system that can perceive its environment, reason or decide based on those perceptions, and then act autonomously toward achieving a goal.

Formally, from AI theory:

An agent is anything that perceives its environment through sensors and acts upon that environment through actuators.
(Russell & Norvig, “Artificial Intelligence: A Modern Approach”)

When we say AI agent today, especially in the LLM era, we mean:

A program that uses artificial intelligence models (like GPTs or other ML models) to make context-aware decisions and perform goal-directed actions, often interacting with APIs, tools, or other systems. -->

---

# Refresher: Components of an AI Agent

![width:400px](https://www.promptingguide.ai/_next/image?url=%2F_next%2Fstatic%2Fmedia%2Fagent-components.6066d990.png&w=1080&q=75)

---

# Refresher: Components of an AI Agent


- **Model**: GPT-4, Llama, Claude...

- **Tools**: External systems and interfaces the agent can interact with, such as web search, code execution environments, calculators, or image generators. 

- **Memory**:
  - Short-term (working) memory: Maintains context within a single session or conversation for coherence and reasoning. [mem0](https://mem0.ai/blog/memory-in-agents-what-why-and-how)

  - Long-term memory: Persists information across sessions and tasks, supporting user personalization, context continuity, and history recall.

<!-- 
---

# Refresher: Components of an AI Agent

- **Reasoning/Generation**: LLMs (e.g., Llama, Claude) Central for natural language understanding and synthesis.

- **Policy/Planner**: Structures work into actionable steps, enabling the agent to manage complex objectives, not just answer atomic queries.​

- **Tools**: Lets the agent interact with and manipulate resources outside its own knowledge—essential for tasks requiring real-time data or actions like code execution or web search.​

-**Retriever**: Provides rapid, targeted access to a broader or more current body of knowledge than the LLM’s static context. This is essential for up-to-date information, detailed documents, or organization-specific data.​ -->

---

## Do you know this number?

<span style="margin-top: 0%; font-size:400px;">404</span>

---
## What about this number?

<span style="margin-top: 0%; font-size:400px;">402</span>

---
## What about this number?

<div style="margin-top: 0%; font-size:400px;"><strong>x</strong>402</div>

<!-- ---


## Embed video

<video controls width="600">
    <source src="example.mp4" type="video/mp4">
</video>

---

## JavaScript example
<div id="chart"></div>
<script>
    document.getElementById('chart').innerHTML = '<b>Interactive chart here</b>';
</script> -->

---

# Today's Agenda

1. **The Payment Problem** & HTTP 402
2. **Blockchain Basics** - Why it matters
3. **Stablecoins** - The building block of micropayments
4. **AI + Blockchain** - The convergence
5. **x402 Protocol** - Architecture & demo
6. **Economics, Risks & Future**

---

# The Payment Problem

![bg right:40% 80%](https://images.unsplash.com/photo-1563986768609-322da13575f3?w=800)

## Current Limitations

- **High fees** (2-3%), **slow settlement** (2-5 days)
- **Geographic friction**, **no micropayments**
- **Intermediary dependency**

## HTTP 402: Reserved Since 1997

```http
HTTP/1.1 402 Payment Required
```

**Why never implemented?**
- No universal payment protocol
- Can't scale micropayments economically

> *"The internet was built for information, not value"*

---

# Blockchain Solves Payment Problems

![bg right:40% 80%](https://images.unsplash.com/photo-1639762681485-074b7f938ba0?w=800)

## Traditional vs. Blockchain

| Traditional | Blockchain (L2) |
|-------------|------------|
| 2-3% fees | <0.01% fees |
| 2-5 day settlement | Seconds |
| Business hours | 24/7/365 |
| Geographic limits | Global |
| $1+ minimum | $0.0001+ viable |
| Intermediaries | Peer-to-peer |

**Key Properties:** Decentralized, trustless, programmable, transparent

---

# The Volatility Problem

![bg right:40% 80%](https://images.unsplash.com/photo-1611974789855-9c2a0a7236a3?w=800)

## Crypto's Achilles Heel

**Bitcoin on Monday:** $50,000
**Bitcoin on Friday:** $35,000 (-30%)

**Problem for payments:**
- Merchant receives $100 → worth $70 next day
- Unpredictable business costs
- Can't budget or plan
- **Nobody wants to transact in volatile assets**

> *"Blockchain solved technical problems but created an economic one"*

---

# Stablecoins: The Solution

![bg right:40% 85%](https://images.unsplash.com/photo-1639762681485-074b7f938ba0?w=800)

## Cryptocurrency + Price Stability

**Stablecoin:** Digital currency pegged to stable asset (usually USD)

**Always:** 1 USDC = $1.00 USD
**Always:** 1 USDT = $1.00 USD

## How They Work

**Fiat-backed:** Every token backed by $1 in bank (USDC, USDT)
**Crypto-backed:** Over-collateralized with crypto (DAI)
**Algorithmic:** Supply adjusts algorithmically (mostly failed)

---

# Stablecoin Market Overview

![bg right:40% 80%](https://images.unsplash.com/photo-1559526324-4b87b5e36e44?w=800)

## Market Size (2024)

- **Total market cap:** $180B+
- **Daily volume:** $50-100B
- **Growth:** 15% YoY

## Top Stablecoins

| Coin | Market Cap | Backing |
|------|-----------|---------|
| USDT (Tether) | $120B | Fiat |
| USDC (Circle) | $35B | Fiat |
| DAI (MakerDAO) | $5B | Crypto |
| BUSD (Binance) | Discontinued | Fiat |

---

# Why Stablecoins Matter for Payments

![bg right:40% 80%](https://images.unsplash.com/photo-1563986768609-322da13575f3?w=800)

## Combining Best of Both Worlds

**From Blockchain:**
- Fast settlement (seconds)
- Low fees (<$0.01)
- 24/7/365 availability
- Global reach
- Programmable

**From Fiat:**
- Price stability
- Predictable value
- Familiar unit of account

**Result:** Perfect for micropayments & machine economies

---

# Stablecoin Use Cases Today

## 1. **Cross-Border Remittances**
- Traditional: 7% fee, 3-5 days
- Stablecoins: 0.1% fee, minutes
- **Market:** $700B annually

## 2. **DeFi & Trading**
- On/off ramp for crypto trading
- Yield generation (5-8% APY)
- Lending/borrowing collateral

## 3. **Emerging Market Inflation Hedge**
- Argentina (140% inflation) → USDT adoption
- Turkey, Lebanon, Venezuela
- Access to USD without bank account

---

# Stablecoins Enable Micropayments

![bg right:40% 85%](https://images.unsplash.com/photo-1639762681485-074b7f938ba0?w=800)

## Why Perfect Match

**Problem:** Can't send $0.001 via Visa/PayPal
- Minimum fees make it uneconomical
- Settlement overhead too high

**Solution:** Stablecoins + Layer 2
- Send $0.0001 with $0.000001 fee
- Instant settlement
- No intermediaries

**Example:**
Pay $0.01 per article read
Pay $0.001 per API call
Pay $0.0001 per data packet

---

# Regulatory Status of Stablecoins

![bg right:40% 80%](https://images.unsplash.com/photo-1563013544-824ae1b704d3?w=800)

## Growing Acceptance

**US:**
- Circle (USDC): Regulated, audited reserves
- Proposed stablecoin legislation (2024)
- Fed exploring digital dollar

**EU:**
- MiCA regulation (2024): Clear framework
- Stablecoins must hold reserves 1:1
- Consumer protection rules

**Risks:**
- De-pegging events (USDC briefly $0.88 in 2023)
- Regulatory uncertainty
- Centralization concerns

---

# AI + Blockchain Convergence

![bg right:40% 90%](https://images.unsplash.com/photo-1635070041078-e363dbe005cb?w=800)

## Why They Need Each Other

**AI Agents Need Blockchain:**
- Autonomous payments (no human approval)
- Micropayment efficiency
- Transparent accounting
- 24/7 operation

**Blockchain Needs AI:**
- Dynamic pricing & negotiation
- Fraud detection
- Smart decision-making

**Result:** Autonomous machine economy

---

# x402 Protocol Architecture

![bg right:40% 80%](https://images.unsplash.com/photo-1639762681485-074b7f938ba0?w=800)

## How It Works

1. **Request** → Client requests resource
2. **402 Response** → Server: "$0.001 required"
3. **Payment** → Client pays USDC/stablecoin
4. **Verification** → Smart contract validates
5. **Access** → Resource delivered
6. **Stream** → Continuous micropayments

**Powered by:** Stablecoins (USDC) on L2 networks

**Key Features:** 
- Sub-second latency
- Predictable costs (no volatility)
- Sub-cent payments viable

---

# Use Case 1: Real-Time Market Data

![bg right:40% 80%](https://images.unsplash.com/photo-1611974789855-9c2a0a7236a3?w=800)

**Scenario:** AI trading agent needs NYSE Level 2 data

**Traditional:**
- $10k-50k/month subscription
- Pay for nights/weekends (unused)
- Annual contracts

**With x402 + Stablecoins:**
- Pay $0.0001 USDC per data packet
- Usage-based: $500-2k/month
- AI decides value per millisecond
- Predictable costs (no volatility)
- **ROI: 80-95% cost reduction**

---

# Use Case 2: AI Model Training

![bg right:40% 90%](https://images.unsplash.com/photo-1558494949-ef010cbdcc31?w=800)

**Scenario:** Training 70B model across 1,000 GPUs

**Traditional (AWS/Azure):**
- $3,060/hour × 1,000 GPUs
- Minimum 1-hour billing
- Crash at 58 min? Pay full hour
- **48-hour cost:** ~$147k

**With x402 + Stablecoins:**
- Pay $0.00085 USDC/GPU-sec
- Auto-migrate to cheaper GPUs
- Exact costs (no crypto volatility)
- **48-hour cost:** ~$110k USDC
- **Savings: 25%+ (failures avoided)**

<!-- 

---

# Use Case 3: Research & Content

![bg right:40% 80%](https://images.unsplash.com/photo-1504711434969-e33886168f5c?w=800)

**Scenario:** AI scanning 10,000 academic papers

**Traditional:**
- $39.95/paper or $2k/year
- **Total cost:** $399k (paywalls)
- Result: AI blocked, piracy

**With x402:**
- $0.001-0.05 per paper
- **Total cost:** $100-500
- Authors earn 70% directly
- **New revenue:** $30M+ for publishers

**Impact:** Democratizes research access

---

# Use Case 4: API Economy

![bg right:35% 90%](https://images.unsplash.com/photo-1558494949-ef010cbdcc31?w=800)

**Scenario:** Weather AI using 50 data sources

**Traditional:**
- $500-5k/month per API
- **Total:** $25k-250k/month
- Manual integration, contracts

**x402:**
- AI tries 50, pays 5 best
- **$2.50 vs. $25k/month**
- Instant access, no contracts

```javascript
const forecast = await weatherAI.compose({
  sources: await discoverAPIs('weather'),
  budget: 0.50
});
```

-->

---

# Economic Impact

![bg right:40% 80%](https://images.unsplash.com/photo-1611974789855-9c2a0a7236a3?w=800)

## Market Size

- **Stablecoin market:** $180B (2024)
- **M2M payments:** $1T+ by 2030
- **Stablecoin transactions:** $50-100B daily

## Why Stablecoins Win

- Merchants accept predictable value
- AI agents can budget accurately
- Cross-border without forex risk
- Programmable compliance (KYC/AML)

<!-- 

---

# Challenges & Solutions

![bg right:40% 85%](https://images.unsplash.com/photo-1614064641938-3bbee52942c7?w=800)

## Technical

- **Scalability:** L2 networks, state channels
- **Privacy:** Zero-knowledge proofs
- **Interoperability:** Cross-chain bridges
- **Security:** Formal verification, AI auditing

## Regulatory

- **AML/KYC** compliance
- **Securities laws** (token classification)
- **Tax reporting** challenges
- **Frameworks:** EU MiCA, US legislation

-->

---

# Demo: x402 in Action

![bg right:40% 90%](https://images.unsplash.com/photo-1620712943543-bcc4688e7485?w=800)

## Live Flow

1. AI discovers API endpoint
2. Receives **402 Payment Required**
3. Evaluates price vs. value
4. Opens payment channel
5. Streams micropayments
6. Receives real-time data
7. Closes channel

**Time:** < 2 seconds complete cycle

---

# Demo Code Example

```javascript
// x402 Payment Flow with Stablecoins
class AIAgent {
  async accessResource(url) {
    let response = await fetch(url);
    
    // Handle 402 Payment Required
    if (response.status === 402) {
      const { price, address } = await response.json();
      // price: "0.001" (USDC)
      
      // Evaluate & pay with USDC stablecoin
      if (this.shouldPay(price)) {
        const payment = await this.usdcWallet.pay({
          to: address,
          amount: price,  // Predictable $0.001 cost
          currency: 'USDC'
        });
        
        // Retry with payment proof
        response = await fetch(url, {
          headers: { 'X-Payment-Proof': payment.hash }
        });
      }
    }
    return response;
  }
}
```

---

# Real-World Examples

![bg right:40% 80%](https://images.unsplash.com/photo-1639762681485-074b7f938ba0?w=800)

**Circle (USDC)** - $35B stablecoin, powers payments
**Stripe** - Added USDC payment support (2024)
**Visa** - USDC settlement on Ethereum/Solana
**PayPal PYUSD** - $500M stablecoin launch
**Coil** - Web monetization with stablecoins
**Helium** - IoT devices pay each other in stablecoins

## Why Finance Professionals Care

- **Stablecoins = new payment rails** (disrupting Swift, Visa)
- Banks issuing own stablecoins (JPM Coin, Wells Fargo)
- $180B market growing 15% YoY
- Skills: stablecoin economics, regulatory frameworks

---

# Investment Opportunities

![bg right:40% 80%](https://images.unsplash.com/photo-1559526324-4b87b5e36e44?w=800)

## Where Money Flows

**Stablecoin Infrastructure:**
- Circle (USDC): $5B raised, Coinbase backed
- Tether (USDT): $120B market cap
- L2 networks: Polygon, Base (Coinbase L2)

**Traditional Finance Entering:**
- Visa: USDC settlement network
- PayPal: PYUSD stablecoin
- Stripe: Stablecoin payment processing

**VC 2024:** $15B+ in stablecoin/payment infrastructure

---

# Major Risks

![bg right:40% 90%](https://images.unsplash.com/photo-1563013544-824ae1b704d3?w=800)

**Stablecoin-Specific Risks:**
- **De-pegging:** USDC fell to $0.88 (2023, SVB crisis)
- **Centralization:** Circle/Tether can freeze accounts
- **Reserve transparency:** Not all stablecoins audited
- **Regulatory shutdown:** SEC could restrict issuance

**Technical:**
- Smart contract bugs: $3.8B lost (2022-23)
- Network congestion on L1 (L2 solves this)

**Regulatory:**
- US: Pending stablecoin legislation
- EU: MiCA requires strict reserves
- China: Banned all crypto including stablecoins

**Operational:**
- Lost keys = lost funds (no recovery)
- No chargebacks (good & bad)

---

# Research Opportunities

![bg right:40% 80%](https://images.unsplash.com/photo-1504711434969-e33886168f5c?w=800)

## Open Questions

1. **Stablecoin reserve management** - Optimal backing ratios
2. **Systemic risk** - What if USDT/USDC de-peg permanently?
3. **Micropayment economics** - Game theory of AI negotiations
4. **Regulatory design** - Balancing innovation & consumer protection
5. **Cross-border flows** - Impact on monetary policy

## Resources

**Stablecoins:** Circle.com, Tether.to, MakerDAO
**Technical:** Ethereum.org, Base.org (Coinbase L2)
**Academic:** Journal of Blockchain Research, BIS papers on stablecoins

---

# Summary: Key Takeaways

![bg right:40% 80%](https://images.unsplash.com/photo-1635070041078-e363dbe005cb?w=800)

1. **Stablecoins solve crypto's volatility problem** ($180B market)
2. **Perfect for micropayments** - predictable value + blockchain speed
3. **HTTP 402** (1997) finally viable with stablecoins
4. **x402 + stablecoins** = AI agents can transact autonomously
5. **Use cases:** 80-95% cost reduction (data, compute, APIs)
6. **Major players:** Circle, Visa, Stripe, PayPal entering
7. **Risks:** De-pegging, regulation, centralization

## The Revolution

**Building Block:** Stablecoins provide stable value
**Infrastructure:** Blockchain provides programmability
**Result:** Value flows at speed of data with predictable costs

---

# Thank You!

## Questions & Discussion

**Contact:**
Dr. Stefano Balietti
[Email address]
[Office hours]

**Additional Resources:**
- Course materials: [link]
- Research papers: [link]
- Code examples: [link]

**Next Lecture:**
Decentralized Finance (DeFi) and Smart Contract Security

---

# Backup Slides

## For Additional Questions

*Technical deep-dives and extended material*

