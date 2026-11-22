# Inbound Lead Enrichment & Routing (Claude + HubSpot + Gmail)

An end-to-end RevOps and Marketing Operations automation built in **n8n** that ingests inbound form submissions, scrapes live prospect company websites via **Jina.ai**, evaluates Ideal Customer Profile (ICP) fit using **Claude**, deduplicates and enriches records in **HubSpot**, and routes leads into instant sales alerts or automated nurture tracks in under 10 seconds.

>**[Watch the Live Walkthrough](https://www.loom.com/share/444dec4761a04800836e03c7f413ef8b)**

<img width="1710" height="691" alt="image" src="https://github.com/user-attachments/assets/c3875fc9-ca8b-4340-bf0f-a9e95042e0a8" />

---

## Business Problem & Impact

Manual inbound lead qualification slows down speed-to-lead, creates inconsistent scoring across reps, and forces SDRs to spend 15–20 minutes researching form fills before sending a first-touch communication.

| Metric / Process | Manual Sales Process | Automated AI RevOps Pipeline |
| :--- | :--- | :--- |
| **Account Research** | Manual website & LinkedIn review | **Automated Markdown extraction (Jina.ai)** |
| **Lead Qualification** | Subjective rep judgment | **Standardized 0–100 LLM rubric (Claude)** |
| **CRM Hygiene** | Manual entry; high duplicate risk | **Email-keyed Upsert (Create or Update)** |
| **First-Touch Outreach** | Written from scratch per lead | **Pre-drafted, pain-point-specific copy** |

---

## System Architecture

```mermaid
flowchart LR
    A[Inbound Form / Webhook] --> B[Jina.ai Reader API<br>Scrape Company URL]
    B --> C[Claude<br>ICP Scoring & Outreach Draft]
    C --> D[JavaScript Code Node<br>Sanitize & Parse JSON]
    D --> E[HubSpot CRM<br>Create or Update Contact]
    E --> F{Lead Score Tier?}
    F -- "Tier 1: score 80+" --> G[Gmail Alert<br>Instant Sales Notification + Draft]
    F -- "Tier 2: score between 50–79" --> H[HubSpot Static List: Tier 2<br>Nurture Track]
    F -- "Tier 3: score below 50" --> I[HubSpot Static List: Tier 3<br>Nurture Track]
```
