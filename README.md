# AI After-Sales Support at an Educational-Robotics Startup

Case study of the AI after-sales operation I designed and built from scratch at **Robotix**, a startup that sells electronic, LEGO-style robotics kits for children. I worked there as **AI Engineer** from 09/2024 to 07/2025, as the only person on this project, reporting to the **CEO and COO**.

**Why.** Robotix sells through many channels at once: private schools (B2B), families (B2C), public-sector contracts and large retail chains. Every channel generates after-sales questions about orders, returns, warranty, faults, assembly and invoices, by email and by phone. As sales grew, the support team could not keep up: **too many tickets and response times too slow**. The goal was to absorb that growth without hiring at the same rate, while keeping every answer under human control.

```
customer (email / phone) ─► Zendesk ticket ─► n8n workflow
                                                 ├─► classify the query (type, channel)
                                                 ├─► retrieve from internal docs (RAG)
                                                 ├─► draft a reply
                                                 └─► route ─► human reviews, edits, sends
```

> This repository contains **no code**. The real system is internal to the company and was built in n8n. This page explains what I designed, the decisions behind it and the outcome. It uses no internal data or documents.

## Highlights

| Block | What I did | Outcome |
|---|---|---|
| [1. Support strategy](#1-support-strategy) | Customer journey, resolution protocols and operating manuals for every sales channel | One way of working across B2B, B2C, public sector and retail |
| [2. Partners & costs](#2-partners--costs) | Compared logistics providers and repair centres; built the pricing model and budget to scale AI support | Kept current logistics providers; chose a repair centre in Madrid |
| [3. AI pipeline](#3-ai-pipeline) | RAG in n8n on top of Zendesk: classify, draft, route | Human always in the loop |
| [4. Outcome](#4-outcome) | Measured cases handled per person, before and after | **~5× more cases resolved per person** |
| [5. Unified version history](#5-unified-version-history) | Led front-end and back-end of a password-protected, on-premise tool merging the commits of several software vendors | One shared history; each vendor sees only its own work |

---

## 1. Support strategy

*Why it matters:* AI cannot fix a process that does not exist. Before automating anything, each type of question needed a clear owner, a standard answer and an expected response time. That is also what the AI needed to learn from.

**What I did**
- Mapped the **customer journey** after purchase for each sales channel (schools, families, public sector, retail).
- Defined **resolution protocols** for the six most common query types: order status, returns, warranty, technical fault, assembly, invoicing.
- Wrote the **operating manuals**: reply templates per query type, target response times and which channel handles what.

**Retention before returns.** I designed a retention step: before accepting a return, the team member in charge of returns called the customer to see whether the problem could be solved so they could keep the product. I quickly learned how those calls worked, so the protocol fitted them.

---

## 2. Partners & costs

*Why it matters:* after-sales is not only answering messages. A fault or a return turns into shipments and repairs, and those partners decide the real cost and speed of support.

**What I did**
- Compared **logistics providers** and **product repair centres** for the cases that needed a repair, on four criteria: **strategy, contracts, legal requirements and price**.
- Decision: keep the logistics providers already in place for shipments, and use a **repair centre in Madrid**.
- Built the **pricing model and budget** to scale support with AI.

---

## 3. AI pipeline

*Why it matters:* most tickets are repetitive and the answer is already in internal documents. An AI that finds that answer and writes the first draft removes most of the manual work, while a person keeps the final word.

**What I built**
- **Zendesk** as the CRM: every email and phone case becomes a ticket.
- **n8n** workflows on each new ticket:
  1. **Classify** the query by type.
  2. **Retrieve** the relevant passages with **RAG** over internal documents: product documentation and the company's operating procedures.
  3. **Draft** a reply for the agent.
  4. **Route** the ticket to the right person.
- **Human in the loop, always.** In 2024 language models were not reliable enough to reply to customers on their own, so the AI never sent anything: a person reviewed, edited and sent every reply.

---

## 4. Outcome

*Why it matters:* the target was to grow support without growing the team at the same pace.

| Metric | Result |
|---|---|
| Cases resolved per person | **~5× more** than before the AI pipeline |
| Replies sent without human review | 0, by design |

---

## 5. Unified version history

*Why it matters:* the company's software was built by several external vendors, each committing in its own way, and there was no single history of what had changed. Without it, nobody in the company could follow the work or trace a problem back to a change.

**What I did**
- Led the **front-end and back-end** of an internal tool that merged every vendor's changes into **one version history**.
- Hosted it on a **local, password-protected server**.
- **Compartmentalised access:** the company could follow everything that was happening, while each vendor only saw its own work and never the others'.

---

## Limits and next steps

- **Draft-only by design.** Every reply needed a human. With today's models, the next step would be letting the AI answer the safest query types on its own, with explicit rules for escalation to a person.
- **Web chatbot (planned).** The next phase was a chatbot on the website so customers could solve common questions (assembly, order status, FAQ) on their own, before a ticket is opened.
- **No public code.** The system is internal and built in n8n, so this repository documents the design and results only.

## Stack

Zendesk · n8n · LLM with retrieval-augmented generation (RAG) over internal documentation

## Author

**Carles Font** · Telecommunications Engineer (UPC) · [GitHub](https://github.com/carles-font-alavedra)
