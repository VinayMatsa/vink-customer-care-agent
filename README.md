# Vink Customer Care Agent (Microsoft Power Platform)

An end-to-end AI customer support solution for a fictional electronics retailer, **Vink Electronics**, built with **Copilot Studio**, **Power Automate**, **Dataverse** and a **model-driven app**.

> **Personal project.** Built in my own developer environment to practice Copilot Studio and Power Platform skills hands-on. Vink Electronics is fictional and all sample data is made up.

## Architecture

```mermaid
flowchart LR
    C([Customer]) -->|chat| A

    subgraph CS[Copilot Studio]
        A[Customer Care Agent<br/>generative orchestration]
        B[Billing child agent]
        K[(Knowledge:<br/>Warranty and Returns Policy)]
        T[Topics: identify customer, new ticket,<br/>ticket status, track order, warranty claim,<br/>escalate, rate ticket]
    end

    subgraph PA[Power Automate]
        AF[Agent flows used as tools<br/>find customer, create ticket, list tickets,<br/>list orders, add reply, escalate, RMA,<br/>record CSAT, repair update]
        BF[Background flows<br/>ticket created, status changed,<br/>daily SLA check]
    end

    subgraph DV[Dataverse]
        D[(Contact · Order · Product ·<br/>Service Ticket · Ticket Update ·<br/>Support Team · Warranty Claim)]
    end

    W([Warehouse scan event]) -->|autonomous trigger| A
    A --- B
    A --- K
    A --- T
    A --> AF --> D
    D --> BF -->|emails and alerts| S([Staff and customers])
    D --> M[Vink Care Hub<br/>model-driven app]
```

## What it demonstrates

| Area | Implementation |
|---|---|
| Agent design | Copilot Studio agent with generative orchestration, custom topics, entities (order, ticket and serial numbers) and a Billing child agent |
| Grounding | Warranty and Returns Policy as a knowledge source, with rules in the agent instructions |
| Tools | Power Automate agent flows called as tools to read and write Dataverse |
| AI triage | A prompt suggests subject, category, priority and a staff summary; the customer confirms on an adaptive card, and a duplicate check runs before the ticket is created |
| Autonomous trigger | A warehouse scan event makes the agent update the repair ticket with no one in the chat |
| Data model | Dataverse tables for customers, orders, products, tickets, ticket updates (customer-visible vs internal), support teams and warranty claims, with autonumbers and SLA due dates |
| Staff app | Vink Care Hub model-driven app with security roles, views, charts and a dashboard |
| Automation | Status emails, VIP and urgent alerts, and a daily SLA report, with all addresses held in environment variables |
| Responsible AI | Customer verification (email plus order or customer number), human escalation, and instructions never to ask for card numbers, passwords or one-time codes |

## How to install

1. In Power Apps, go to **Solutions > Import solution**.
2. Select `CustomerCareAgent_1_0_0_1.zip` from this repository.
3. Set the connections and the environment variables (`vin_CCSupportMailbox`, `vin_CCCustomerEmailOverride`) when asked.

## Screenshots

### New ticket with AI triage
![New ticket with AI triage](screenshots/1-new-ticket-ai-triage.png)

### Warranty claim
![Warranty claim](screenshots/2-warranty-claim.png)

### Customer rates a resolved ticket
![Customer rates a ticket](screenshots/3-rate-ticket-chat.png)

### Staff app: ticket form with CSAT
![Ticket form with CSAT](screenshots/4-ticket-form-csat.png)

### Automatic status email
![Automatic status email](screenshots/5-status-email.png)

### Daily SLA report
![Daily SLA report](screenshots/6-daily-sla-report.png)

### Customer Care Overview dashboard
![Dashboard](screenshots/7-dashboard.png)

### Cloud flows in the solution
![Cloud flows in the solution](screenshots/8-flows.png)

## Built with

Copilot Studio · Power Automate · Dataverse · Model-driven Power Apps · AI Builder prompts · Adaptive Cards
