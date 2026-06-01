# 3-Layer Order Management System: LarkBase + n8n + Astro

> 🏗️ **Resilient Architecture Case Study**  
> A production system handling 100+ orders/day for an F&B manufacturer.  
> 👤 Architect: [Do Thanh Vinh (Kevin Do)](https://github.com/dothanhvinh17)  
> 🔗 Full case study: [vinhautomation.com/en/projects/fbb-order-automation-case-study](https://www.vinhautomation.com/en/projects/fbb-order-automation-case-study)

## 🎯 Problem Solved

Manual order entry across multiple channels (retail, wholesale, supermarket) was:
- ❌ Time-consuming: 5-10 mins per order with multi-product entries
- ❌ Error-prone: Forgotten order IDs, wrong quantities, duplicate records
- ❌ Fragile: No fallback when automation systems failed

## ️ Solution: 3-Layer Decoupled Architecture
[ Interface Layer ] → [ Automation Layer ] → [ Data Layer ]
Astro Admin n8n Workflows LarkBase Core
(Failover UI) (Chat-triggered) (15+ relational tables)


### Layer 1: Data Core (LarkBase)
- 15+ interconnected tables: `orders`, `order_details`, `products`, `customers`, `inventory`...
- Normalized schema with explicit foreign keys
- Real-time dashboard views for CEO oversight

### Layer 2: Automation (n8n)
- 29-node workflow: Lark Messenger → validate → write to 2 tables → reply confirmation
- Rule-based validation (zero AI dependency) → deterministic, easy to debug
- Error handling with retry logic + fallback notifications

### Layer 3: Interface (Astro Admin)
- Static admin web deployed on Cloudflare Pages (free tier)
- Role-based auth (1 admin + 4 staff users)
- Direct LarkBase sync as failover channel when n8n/VPS is down

## 🔄 Three Order Entry Paths

| Path | Mechanism | Use Case |
|------|-----------|----------|
| **Chat (Primary)** | Lark Messenger + n8n workflow | Daily operations, trained staff |
| **Web Form (Failover)** | Astro Admin → direct DB write | Emergency when n8n down |
| **Native (Manual)** | LarkBase UI direct entry | Data correction, power users |

> 💡 **Key Insight**: Decoupling layers allows changing UI or automation without touching the core data schema — essential for long-term maintainability.

## 📂 Repository Structure

n8n-larkbase-3layer-order-system/
├── README.md
├── LICENSE
├── .gitignore
├── architecture/ # Diagrams & data flow docs
├── larkbase/ # Schema examples & query patterns
├── n8n-workflow/ # Anonymized workflow JSON & node reference
├── astro-admin/ # Form/UI snippets & auth patterns
├── screenshots/ # Blurred UI & execution examples
└── docs/ # Deployment & failover testing guides

## 🔐 Anonymization & Security

This repo contains **anonymized, educational content only**:
- ❌ No real client names, business rules, or sensitive data
- ❌ No production credentials or API keys
- ❌ No proprietary business logic

All screenshots will have sensitive fields blurred. Use this repo to learn architecture patterns, not to replicate a specific business.

## 🧭 Next Steps & Roadmap

- [ ] Upload architecture diagram (SVG/PNG)
- [ ] Add anonymized n8n workflow JSON (29 nodes)
- [ ] Document LarkBase schema patterns (generic)
- [ ] Share Astro admin form snippet (failover UI)
- [ ] Write deployment & failover testing guide

##  Contributing & Feedback

- Found an issue in the anonymized example? → Open an issue
- Have an architecture improvement? → Submit a PR
- Want to discuss a similar use case? → Email [vinh@vinhautomation.com](mailto:vinh@vinhautomation.com)

## 📄 License

MIT License — Free to use, modify, and share for learning purposes.  
Not for commercial replication of the specific business implementation.

---

🔗 **More by this creator:**  
[github.com/dothanhvinh17](https://github.com/dothanhvinh17) | [vinhautomation.com/en/projects](https://www.vinhautomation.com/en/projects/)
