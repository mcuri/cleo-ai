# Cleo AI — UI Prototype Design

**Date:** 2026-04-19
**Scope:** Full app shell prototype — single HTML file
**Status:** Approved

---

## Overview

A self-contained HTML prototype of the Cleo AI interface for SMBs. The goal is to communicate the product concept clearly and iterate quickly before committing to a real implementation. No build tools, no dependencies — opens in any browser.

---

## Visual Style

- **Background:** White and light blue (#f8faff)
- **Primary accent:** Blue (#3b6ef8)
- **Secondary accent:** Light blue tint (#eef1ff, #d0dbff)
- **Text:** Near-black (#1a1a1a), muted grey (#888) for secondary
- **Font:** Inter (loaded from Google Fonts)
- **Feel:** Clean, modern, familiar SaaS — approachable for non-technical SMB users

---

## App Shell

A persistent shell wrapping all views. Only the main content area changes between views.

### Sidebar (always visible)

- **Top:** Cleo logo + wordmark
- **Home link** → Dashboard view
- **AGENTS section:**
  - Marketing (active, clickable)
  - Finance (active, clickable)
  - HR (locked/greyed — Starter plan)
- **ACCOUNT section:**
  - Profile (clickable)
- Active item highlighted with blue background pill

### Navigation behavior

Vanilla JS swaps the main content area between 4 views:
1. Home Dashboard (default)
2. Marketing Agent workspace
3. Finance Agent workspace
4. Profile

No page reloads. Active sidebar item updates on each view change.

---

## View 1 — Home Dashboard

Default landing view after login.

### Contents

- **Greeting header:** "Bom dia, Maria" + today's date
- **Agent cards (3):** One card per agent containing:
  - Agent name and icon
  - One proactive nudge in Portuguese
  - "Ir para o agente →" button that navigates to that workspace
- **Recent artifacts strip:** Last 4 outputs across all agents as small cards — filename, output type, agent label
- **Profile completeness bar:** Subtle bottom prompt — "Seu perfil está 70% completo — adicione informações de precificação para melhorar os resultados" — links to Profile view

### Sample data

Use a Brazilian clothing e-commerce called **Eufloria**. Profile is 70% complete. Marketing agent has a campaign draft ready. Finance nudge: "3 boletos estão vencidos — quer que eu ajude a acompanhar?" HR is locked (Starter plan).

---

## View 2 & 3 — Agent Workspace (Marketing + Finance)

Both workspaces share the same layout. Marketing is pre-populated; Finance shows an empty state.

### Layout (chat-centered)

- **Header:** Agent name + one-line description in Portuguese (e.g. "Sua especialista em marketing")
- **Skill pills:** Horizontal scrollable row of pills just above the input bar
  - Marketing: "Campanha nas redes sociais", "Sequência de e-mails", "Texto de anúncio", "Auditar comunicação", "Brief de conteúdo"
  - Finance: "Resumo de receitas e despesas", "Redigir boleto/fatura", "Identificar gaps de fluxo de caixa", "Criar snapshot de orçamento"
  - Clicking a pill pre-fills the chat input with a prompt starter in Portuguese
- **Conversation thread:**
  - Agent messages: left-aligned, blue bubble (#eef1ff, blue text)
  - User messages: right-aligned, white bubble with grey border
  - First message is always a proactive agent greeting in Portuguese referencing prior context
- **Inline artifacts:** Skill output appears as an attached card in the thread
  - Card contains: filename, file type badge, preview snippet (1–2 lines), "Ver" and "Baixar" action links
- **Input bar:** Fixed at the bottom — text input + send button (blue), placeholder "Rode uma skill ou pergunte qualquer coisa..."

### Marketing workspace — pre-populated conversation (Portuguese)

1. Agent: "Bem-vinda de volta! Da última vez, estávamos trabalhando na campanha de verão da Eufloria. Já criei dois posts — quer revisar?"
2. *(inline artifact card: "Campanha_Verao_Eufloria.docx" — 2 posts para Instagram e TikTok)*
3. User: "Ficou ótimo! Pode redigir o e-mail de lançamento também?"
4. Agent: "Claro! Aqui está um rascunho do e-mail para a sua lista:"
5. *(inline artifact card: "Email_Lancamento_Colecao.txt")*

### Finance workspace — empty state

Agent greeting: "Olá! Sou sua especialista financeira. Posso ajudar a acompanhar receitas, redigir faturas e identificar riscos no fluxo de caixa. Por onde quer começar?"
Skill pills visible. No prior conversation.

---

## View 4 — Profile

A structured read/edit view of the business profile.

### Layout

- **Header:** Business name ("Eufloria") + "Editar perfil" button
- **Completeness bar:** Progress indicator (70%) with tooltip listing missing fields in Portuguese (precificação, tamanho do time)
- **Sections (collapsible), all labels in Portuguese:**
  - **Identidade:** Nome da empresa, setor, descrição, tom de voz, personalidade da marca
  - **Produtos & Serviços:** Lista de produtos/coleções
  - **Público-alvo:** Descrição do cliente ideal
  - **Desafios & Objetivos:** Dores atuais, critérios de sucesso, prioridades
  - **Agentes:** Quais estão ativos, quais estão bloqueados e por quê
- **Field interaction:** Each field shows label + value. Clicking the value makes it editable inline (simple contenteditable for the prototype)
- **"Refazer entrevista com IA" button** at the bottom of each section

### Sample data (Eufloria)

- Setor: Moda feminina — e-commerce
- Descrição: "E-commerce brasileiro de roupas femininas com identidade própria, focado em peças exclusivas e produção sustentável"
- Tom de voz: Sofisticado, próximo, feminino
- Público-alvo: Mulheres entre 25–40 anos, Brasil, interessadas em moda consciente e estilo autoral
- Desafios: "Produzir conteúdo para redes sociais com consistência sem aumentar o time", "Entender melhor o retorno de cada campanha"
- Objetivos: "Lançar coleção de inverno com campanha integrada", "Aumentar recorrência de compra da base de clientes"

---

## Prototype Constraints

- **Single HTML file** — all CSS and JS inline or in `<style>`/`<script>` tags
- **No backend** — all data is hardcoded sample content
- **No real auth** — prototype starts on the Home Dashboard directly
- **Language:** All UI copy and sample content in Brazilian Portuguese
- **Interactions:** Sidebar navigation, skill pill click (pre-fills input), send button (appends a mock agent reply), inline contenteditable for Profile fields
- **HR workspace:** Not implemented — clicking HR in sidebar shows a "Em breve / Faça upgrade para desbloquear" state

---

## File Output

`fazai-smb-design.html` → replaced by a new file: `cleo-ai-prototype.html` in the project root.

---

## Success Criteria

The prototype is successful if:
- A non-technical stakeholder can navigate all 4 views without explanation
- The agent workspace feel is clear — skills, conversation, and artifacts all make sense
- The profile view communicates the "living document" concept
- It's shareable as a single file with no setup
