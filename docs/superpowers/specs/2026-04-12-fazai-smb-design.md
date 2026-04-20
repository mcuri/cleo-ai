# Cleo Context Engineering for Small Business Platform

**Date:** 2026-04-12
**Scope:** MVP — Small Business persona only
**Approach:** Profile-Powered Agent Workspace

---

## Vision

Cleo's end goal is to give every small business owner in Brazil a super specialized, context-powered AI directly on WhatsApp — the platform they already live on. No new apps to download, no dashboards to learn. Just a conversation with an AI that knows your business deeply and gets work done.

WhatsApp is the primary interface. It is where users will access Cleo daily, where adoption will scale, and where the product will have the most impact — because in Brazil, WhatsApp isn't just a messaging app, it's infrastructure. The web platform is always available as a secondary interface: a richer environment for onboarding, profile management, and deeper work. But the goal is for users to live in WhatsApp and only go to the web when they need to.

The web platform is also the first step: where the product is built, validated, and refined before WhatsApp integration is introduced.

---

## Problem

**Primary: Small businesses are stretched beyond their means.**

A lean team is simultaneously responsible for marketing, sales, finance, hiring, and operations — each a full-time discipline on its own. Without the bandwidth to go deep on any one area, quality suffers across all of them and critical work gets deprioritized.

Hiring dedicated specialists across every function is out of reach for most small businesses. The expertise gap is real, and it compounds over time. And patching it together with a stack of single-purpose subscriptions doesn't help — each tool has its own cost, its own learning curve, and no shared context with the others. The overhead of managing them adds to an already overloaded plate.

**Secondary: AI hasn't solved this — yet.**

Most small businesses that turn to AI are still using it the wrong way: one-off prompts, generic outputs, no business context carried forward. The interaction is transactional, not cumulative. Each session starts from zero, so the results reflect that. The promise of AI doing meaningful work is there — but without deep context, it stays out of reach.

---

## Goal

Cleo is a context engineering company. We help small businesses in Brazil build a deep, structured understanding of who they are — and then put that context to work across every functional area, on the interfaces they already use.

The missing piece in AI today isn't the model. It's the context. Most businesses interact with AI from scratch every time — no memory, no knowledge, no continuity. Cleo solves that. Build the business profile once, and every interaction gets smarter. No repeated explanations. No generic outputs. Just AI that knows the business and meets users where they are.

---

## Core Loop

A high-level summary of how the platform works end to end. Each step is covered in detail in the sections below.

1. **Onboarding interview** — A structured business diagnostic that builds the profile from day one
2. **Skill selection** — The AI recommends relevant skills based on the business profile
3. **Co-creation** — Each skill is customized to the business before execution
4. **Daily use** — An orchestrator agent handles your requests and dispatches specialized workers to get the job done
5. **Evolution** — Skills and the business profile adapt over time as the business grows

---

## Why Cleo, not ChatGPT?

ChatGPT is a general-purpose AI. Cleo is a context engineering product. The difference isn't the model — it's everything built around it.

- **Engineered context** — your business profile is built once and injected into every interaction, so Cleo always knows who you are
- **Structured, opinionated skills** — not generic prompts, but purpose-built workflows calibrated to your domain
- **Calibrated to Brazilian business reality** — language, market context, and local nuance built in
- **Beyond text** — executes code, generates charts, and produces PDF reports
- **Available where you are** — web today, WhatsApp tomorrow; Cleo meets users on the interfaces they already use
- **Background agents** — work continues in the background while you keep chatting

---

## Target Users (MVP)

**Small Businesses in Brazil**
- Owners and operators who want to automate internal workflows
- Not technical — the product must feel intuitive and immediately valuable
- Portuguese-first experience, calibrated to Brazilian market context and business reality
- Success is measured by: Small Businesses onboarded, retention after month 1, time spent in product

**Content Creators** — post-MVP, same functional core with different UI copy and skill sets.

---

## Architecture: Two Layers

### 1. Profile Layer
A living document about the business. Built during onboarding, enriched continuously through usage. Contains:

**Identity**
- Company name, industry, description
- Products and services
- Target audience
- Tone of voice and brand personality

**Operational Context**
- Current challenges and pain points (e.g., "marketing campaigns underperforming despite branding investment", "lack of visibility on income vs expenses", "inventory control issues")
- Goals and success criteria
- Priorities

The profile is the single source of truth for all agents. It is never static — agents enrich it over time and users can edit any field at any time. User input always takes precedence over anything inferred automatically.

### 2. Agent Workspace Layer
A set of domain-specific workspaces unlocked based on profile recommendations. Users can reach agents in two ways:

**Orchestrator Chat** — a single conversation available from the dashboard. The user types naturally; the orchestrator interprets the request and dispatches the right specialized worker. Best for quick, daily-use requests.

**Agent Workspaces** — dedicated spaces for deeper, focused work within a domain. Each workspace contains:
- **Skills** — curated jobs the agent can execute within that domain
- **Chat** — a direct conversation thread with that agent; proactive presence that surfaces suggestions and follows up on prior sessions
- **Files** — outputs produced within that workspace, tied to the agent's functional area

Every skill execution injects the full business profile as context. The agent never asks for information the profile already contains.

---

## Onboarding Flow

The goal of onboarding is to build a profile rich enough that the first agent output feels personalized, not generic.

### Step 1: URL Snapshot (First Draft)
The user shares links — website, Instagram, LinkedIn, Facebook, or any public URL. The AI fetches and analyzes these to extract:
- From website: company description, products/services, tone of voice, target audience, pricing signals
- From social media: brand personality, content style, posting cadence, audience engagement patterns

This creates a first draft of the profile. It is a starting point, not the source of truth.

### Step 2: Build the Profile (Two Paths — User Chooses)

**AI Interview**
The AI reviews what it found from URLs, presents it transparently ("Here's what I learned about your business — does this look right?"), then asks targeted follow-up questions for what it couldn't determine:
- What's not working right now?
- What does success look like in 6 months?
- Who is your main customer?
- What's your biggest operational challenge?

One question at a time. Conversational. Takes ~5 minutes.

**Brain Dump**
The user writes or pastes anything — a pitch paragraph, a rambling description, notes. The AI structures it into the profile, then asks only for what's missing.

In both paths, user input is authoritative. The profile is human-informed first, URL-assisted second.

### Step 3: Agent Recommendation
Once the profile reaches a minimum viable completeness, the AI recommends an agent stack:
> "Based on your focus on growth and your challenge with marketing ROI, I'd suggest starting with the Marketing Agent and Finance Agent."

The user confirms, adjusts, or adds more agents. Inactive agents are visible but locked, with a description of what they unlock.

### Step 4: First Workspace
The user lands in the dashboard. The orchestrator chat is ready for their first request, and their activated agent workspaces are available for deeper, focused work.

---

## Agents (MVP — Small Business)

### Marketing Agent
Skills include: write a social media campaign, draft an email sequence, generate ad copy for a product, audit current messaging, create a content brief.

### Finance Agent
Skills include: summarize income vs expenses, draft an invoice, identify cash flow gaps, create a budget snapshot, flag financial risks.

### HR Agent
Skills include: write a job description, draft an onboarding document, create a performance review template, write an internal policy, draft a team communication.

Each agent's skill set is informed by the entity profile. The agent pre-fills everything it knows and asks only for job-specific input it doesn't have.

---

## Skill Execution Flow

1. User selects a skill from the skill panel (or the agent proactively suggests one)
2. Agent pre-fills context from the profile, asks only for what's job-specific and missing — short, focused, never a form
3. Agent produces the artifact
4. Artifact appears in the workspace's artifact panel — viewable, editable, downloadable in-app
5. Agent suggests a logical next step to keep momentum
6. If new information was gathered during execution, agent optionally saves it back to the profile

---

## Proactiveness

Proactiveness operates in two distinct modes:

**In-session** — when the user is already chatting, Cleo suggests next steps, flags profile gaps, and keeps momentum. This is free, natural, and always on.
- "You mentioned your Q2 campaign last time — want to review how it performed and plan the next one?"
- "I don't have your pricing information. Want to add it so future outputs are more accurate?"

**Out-of-session** — reserved exclusively for users identified as churn risks. Outbound messages on WhatsApp carry a cost and should be used sparingly. The goal is not to push users back daily — it is to recover users who are drifting away.

The primary retention mechanic is not proactive outreach — it is habit formation. Cleo has to be useful enough that users naturally return and start conversations themselves, the same way they'd message a trusted colleague on WhatsApp.

Proactiveness surfaces in both the orchestrator chat and individual agent workspaces.

---

## User Experience

### Dashboard

- **Chat** — the main entry point; a single conversation with the orchestrator that dispatches specialized workers for any request
- **My Skills** — active skills with co-creation controls to customize them to the business
- **Skill Store** — browse available skills and request new ones
- **Business Profile** — view and edit the full business profile at any time
- **Files** — all uploads and AI-generated outputs in one place
- **History** — past conversations and completed tasks

Agent workspaces are accessible from the dashboard for users who want to go deeper with a specific domain — each with its own chat, skills, and files.

### Daily Use Examples

**User:** "Preciso postar algo essa semana, tô sem ideia"
**AI:** Dispatches Marketing worker → returns content suggestions with Reels scripts tailored to the business profile

**User:** "Esse mês tá apertado"
**AI:** Dispatches Financial worker → returns a cash flow analysis with charts and a downloadable PDF report

---

## Subscription Model

**Starter**
- 1 active agent
- Limited skill executions per month
- Core profile features

**Pro**
- All recommended agents
- Unlimited skill executions
- Full artifact access
- Priority support

Annual plan offered at a discount to drive commitment and reduce churn.

---

## MVP Scope & Boundaries

**In scope:**
- Small Business persona only
- Three agents: Marketing, Finance, HR
- Profile building via AI interview, brain dump, and URL ingestion
- Agent workspaces with skill panel, conversation thread, and artifact panel
- Starter and Pro subscription tiers

**Out of scope for MVP:**
- WhatsApp integration
- Content creator persona
- External integrations (Google Workspace, QuickBooks, Slack, etc.)
- Mobile app
- Team/multi-user accounts

---

## Success Metrics (MVP)

- Number of Small Businesses onboarded
- User retention after month 1
- Time spent in product per session

---

## Future Expansion

- **WhatsApp as primary interface** — Cleo available directly on WhatsApp as the main access point; web remains always available as a secondary interface for onboarding, profile management, and deeper work
- Content creator persona (same functional core, different UI copy and skill sets)
- External integrations (Google Workspace, QuickBooks, social platform APIs)
- Additional agents per persona
- Multi-user / team accounts
