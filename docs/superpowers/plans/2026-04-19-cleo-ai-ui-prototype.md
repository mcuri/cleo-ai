# Cleo AI UI Prototype — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a single self-contained HTML prototype of the Cleo AI interface for SMBs, using Eufloria (Brazilian clothing e-commerce) as the sample brand, all content in Portuguese.

**Architecture:** One file (`cleo-ai-prototype.html`) with inline CSS, HTML, and vanilla JS. Four views (Home, Marketing, Finance, Profile) are rendered inside a persistent shell — a labeled sidebar shows/hides views without page reloads. HR is a locked/upgrade state.

**Tech Stack:** HTML5, CSS3 (custom properties, flexbox), vanilla JavaScript, Inter font (Google Fonts)

---

## File Structure

| File | Responsibility |
|------|---------------|
| `cleo-ai-prototype.html` | Everything — shell, all views, CSS, JS |

Internal structure within the file:
- `<style>` — CSS custom properties + all component styles
- `<body>` — sidebar + `#main` content area containing all view divs
- `<script>` — `showView()`, skill pill handler, send button, collapsible sections

---

## Task 1: HTML Skeleton + CSS Foundation

**Files:**
- Create: `cleo-ai-prototype.html`

- [ ] **Step 1: Create the file with full skeleton**

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Cleo AI</title>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
  <style>
    :root {
      --blue: #3b6ef8;
      --blue-light: #eef1ff;
      --blue-mid: #d0dbff;
      --bg: #f8faff;
      --white: #ffffff;
      --text: #1a1a1a;
      --text-muted: #888888;
      --border: #e0e8ff;
      --sidebar-w: 200px;
      --radius: 8px;
    }
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body {
      font-family: 'Inter', sans-serif;
      background: var(--bg);
      color: var(--text);
      display: flex;
      height: 100vh;
      overflow: hidden;
      font-size: 14px;
    }
    /* SIDEBAR */
    #sidebar {
      width: var(--sidebar-w);
      background: var(--white);
      border-right: 1px solid var(--border);
      display: flex;
      flex-direction: column;
      padding: 20px 12px;
      flex-shrink: 0;
    }
    /* MAIN */
    #main {
      flex: 1;
      overflow-y: auto;
      display: flex;
      flex-direction: column;
    }
    /* VIEWS */
    .view { display: none; flex: 1; flex-direction: column; }
    .view.active { display: flex; }
  </style>
</head>
<body>
  <div id="sidebar"><!-- Task 2 --></div>
  <div id="main">
    <div id="view-home" class="view active"><!-- Task 3 --></div>
    <div id="view-marketing" class="view"><!-- Task 4 --></div>
    <div id="view-finance" class="view"><!-- Task 5 --></div>
    <div id="view-hr" class="view"><!-- Task 7 --></div>
    <div id="view-profile" class="view"><!-- Task 6 --></div>
  </div>
  <script>
    // Task 2+
  </script>
</body>
</html>
```

- [ ] **Step 2: Open in browser and verify**

Open `cleo-ai-prototype.html` in your browser. You should see a blank page with a white left column (200px) and a light blue-grey main area. No content yet — that's expected.

- [ ] **Step 3: Commit**

```bash
git add cleo-ai-prototype.html
git commit -m "feat: add HTML skeleton and CSS foundation for Cleo AI prototype"
```

---

## Task 2: Sidebar + Navigation

**Files:**
- Modify: `cleo-ai-prototype.html` — sidebar HTML, nav CSS, `showView()` JS

- [ ] **Step 1: Replace `<div id="sidebar"><!-- Task 2 --></div>` with sidebar HTML**

```html
<div id="sidebar">
  <div class="sidebar-logo">
    <div class="logo-mark">C</div>
    <span class="logo-name">Cleo</span>
  </div>

  <nav class="sidebar-nav">
    <div class="nav-label">INÍCIO</div>
    <a class="nav-item active" data-view="home" onclick="showView('home')">
      <span class="nav-icon">⌂</span> Dashboard
    </a>

    <div class="nav-label" style="margin-top:20px">AGENTES</div>
    <a class="nav-item" data-view="marketing" onclick="showView('marketing')">
      <span class="nav-icon">📢</span> Marketing
    </a>
    <a class="nav-item" data-view="finance" onclick="showView('finance')">
      <span class="nav-icon">💰</span> Finanças
    </a>
    <a class="nav-item locked" title="Faça upgrade para desbloquear" onclick="showView('hr')">
      <span class="nav-icon">👥</span> RH
      <span class="lock-badge">🔒</span>
    </a>

    <div class="nav-label" style="margin-top:20px">CONTA</div>
    <a class="nav-item" data-view="profile" onclick="showView('profile')">
      <span class="nav-icon">👤</span> Perfil
    </a>
  </nav>
</div>
```

- [ ] **Step 2: Add sidebar CSS inside the `<style>` block (after `.view.active` rule)**

```css
.sidebar-logo {
  display: flex;
  align-items: center;
  gap: 8px;
  margin-bottom: 28px;
}
.logo-mark {
  width: 28px;
  height: 28px;
  background: var(--blue);
  color: white;
  border-radius: 7px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: 700;
  font-size: 14px;
}
.logo-name { font-weight: 700; font-size: 15px; }
.sidebar-nav { display: flex; flex-direction: column; }
.nav-label {
  font-size: 10px;
  font-weight: 700;
  color: var(--text-muted);
  letter-spacing: 0.08em;
  margin-bottom: 6px;
}
.nav-item {
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 7px 10px;
  border-radius: 6px;
  cursor: pointer;
  color: var(--text-muted);
  font-size: 13px;
  font-weight: 500;
  text-decoration: none;
  margin-bottom: 2px;
  transition: background 0.15s;
  position: relative;
}
.nav-item:hover { background: var(--blue-light); color: var(--blue); }
.nav-item.active { background: var(--blue-light); color: var(--blue); }
.nav-item.locked { opacity: 0.5; cursor: default; }
.nav-item.locked:hover { background: none; color: var(--text-muted); }
.nav-icon { font-size: 13px; }
.lock-badge { margin-left: auto; font-size: 10px; }
```

- [ ] **Step 3: Replace `// Task 2+` in the `<script>` tag with the navigation function**

```javascript
function showView(name) {
  // update views
  document.querySelectorAll('.view').forEach(v => v.classList.remove('active'));
  document.getElementById('view-' + name).classList.add('active');
  // update sidebar active state
  document.querySelectorAll('.nav-item[data-view]').forEach(a => a.classList.remove('active'));
  const link = document.querySelector('.nav-item[data-view="' + name + '"]');
  if (link) link.classList.add('active');
  // scroll main to top
  document.getElementById('main').scrollTop = 0;
}
```

- [ ] **Step 4: Open in browser and verify navigation**

Open the file. You should see the sidebar with logo "Cleo", sections INÍCIO / AGENTES / CONTA, and nav items. Clicking items should switch the active highlight (views are empty for now — that's fine).

- [ ] **Step 5: Commit**

```bash
git add cleo-ai-prototype.html
git commit -m "feat: add sidebar navigation with JS view switching"
```

---

## Task 3: Home Dashboard

**Files:**
- Modify: `cleo-ai-prototype.html` — home view HTML + CSS

- [ ] **Step 1: Replace `<!-- Task 3 -->` inside `#view-home` with the dashboard HTML**

```html
<div class="view-header">
  <div>
    <h1 class="greeting">Bom dia, Maria 👋</h1>
    <p class="greeting-sub">Aqui está um resumo do que está acontecendo na Eufloria.</p>
  </div>
</div>

<div class="dashboard-body">
  <!-- Agent cards -->
  <div class="section-label">Seus agentes</div>
  <div class="agent-cards">
    <div class="agent-card">
      <div class="agent-card-header">
        <span class="agent-icon">📢</span>
        <span class="agent-name">Marketing</span>
      </div>
      <p class="agent-nudge">Você tem um rascunho de campanha pronto para revisar.</p>
      <button class="go-btn" onclick="showView('marketing')">Ir para o agente →</button>
    </div>
    <div class="agent-card">
      <div class="agent-card-header">
        <span class="agent-icon">💰</span>
        <span class="agent-name">Finanças</span>
      </div>
      <p class="agent-nudge">3 boletos estão vencidos — quer que eu ajude a acompanhar?</p>
      <button class="go-btn" onclick="showView('finance')">Ir para o agente →</button>
    </div>
    <div class="agent-card locked-card">
      <div class="agent-card-header">
        <span class="agent-icon">👥</span>
        <span class="agent-name">RH</span>
        <span class="badge-locked">Bloqueado</span>
      </div>
      <p class="agent-nudge" style="color:var(--text-muted)">Desbloqueie para automatizar descrições de cargo, onboarding e mais.</p>
      <button class="go-btn upgrade-btn">Fazer upgrade →</button>
    </div>
  </div>

  <!-- Recent artifacts -->
  <div class="section-label" style="margin-top:28px">Últimos resultados</div>
  <div class="artifacts-strip">
    <div class="artifact-chip">
      <span class="artifact-chip-icon">📄</span>
      <div>
        <div class="artifact-chip-name">Campanha_Verao_Eufloria.docx</div>
        <div class="artifact-chip-meta">Marketing · há 2h</div>
      </div>
    </div>
    <div class="artifact-chip">
      <span class="artifact-chip-icon">✉️</span>
      <div>
        <div class="artifact-chip-name">Email_Lancamento_Colecao.txt</div>
        <div class="artifact-chip-meta">Marketing · há 3h</div>
      </div>
    </div>
    <div class="artifact-chip">
      <span class="artifact-chip-icon">📊</span>
      <div>
        <div class="artifact-chip-name">Resumo_Fluxo_Caixa_Abril.pdf</div>
        <div class="artifact-chip-meta">Finanças · ontem</div>
      </div>
    </div>
    <div class="artifact-chip">
      <span class="artifact-chip-icon">📄</span>
      <div>
        <div class="artifact-chip-name">Fatura_Cliente_003.pdf</div>
        <div class="artifact-chip-meta">Finanças · ontem</div>
      </div>
    </div>
  </div>

  <!-- Profile completeness -->
  <div class="profile-bar-block">
    <div class="profile-bar-text">
      <span>Seu perfil está <strong>70% completo</strong></span>
      <a class="profile-bar-link" onclick="showView('profile')">Completar perfil →</a>
    </div>
    <div class="profile-bar-track">
      <div class="profile-bar-fill" style="width:70%"></div>
    </div>
    <p class="profile-bar-hint">Adicione precificação e tamanho do time para melhorar os resultados dos agentes.</p>
  </div>
</div>
```

- [ ] **Step 2: Add home dashboard CSS inside `<style>` (append after existing rules)**

```css
/* ── SHARED VIEW HEADER ── */
.view-header {
  padding: 28px 32px 0;
  border-bottom: 1px solid var(--border);
  background: var(--white);
  padding-bottom: 20px;
}
.greeting { font-size: 22px; font-weight: 700; margin-bottom: 4px; }
.greeting-sub { color: var(--text-muted); font-size: 13px; }

/* ── DASHBOARD ── */
.dashboard-body { padding: 28px 32px; }
.section-label {
  font-size: 11px;
  font-weight: 700;
  color: var(--text-muted);
  letter-spacing: 0.07em;
  margin-bottom: 12px;
}
.agent-cards { display: grid; grid-template-columns: repeat(3, 1fr); gap: 16px; }
.agent-card {
  background: var(--white);
  border: 1px solid var(--border);
  border-radius: var(--radius);
  padding: 18px;
  display: flex;
  flex-direction: column;
  gap: 10px;
}
.locked-card { opacity: 0.7; }
.agent-card-header { display: flex; align-items: center; gap: 8px; }
.agent-icon { font-size: 16px; }
.agent-name { font-weight: 600; font-size: 14px; }
.badge-locked {
  margin-left: auto;
  font-size: 10px;
  background: var(--bg);
  border: 1px solid var(--border);
  color: var(--text-muted);
  padding: 2px 7px;
  border-radius: 20px;
}
.agent-nudge { font-size: 12px; color: var(--text); line-height: 1.5; flex: 1; }
.go-btn {
  background: var(--blue);
  color: white;
  border: none;
  border-radius: 6px;
  padding: 8px 14px;
  font-size: 12px;
  font-weight: 600;
  cursor: pointer;
  align-self: flex-start;
  font-family: inherit;
}
.go-btn:hover { background: #2d5ce0; }
.upgrade-btn { background: var(--text-muted); }
.upgrade-btn:hover { background: #666; }

/* ── ARTIFACTS STRIP ── */
.artifacts-strip { display: flex; gap: 12px; flex-wrap: wrap; }
.artifact-chip {
  background: var(--white);
  border: 1px solid var(--border);
  border-radius: var(--radius);
  padding: 10px 14px;
  display: flex;
  align-items: center;
  gap: 10px;
  cursor: pointer;
}
.artifact-chip:hover { border-color: var(--blue-mid); background: var(--blue-light); }
.artifact-chip-icon { font-size: 18px; }
.artifact-chip-name { font-size: 12px; font-weight: 500; }
.artifact-chip-meta { font-size: 11px; color: var(--text-muted); margin-top: 2px; }

/* ── PROFILE BAR ── */
.profile-bar-block {
  margin-top: 28px;
  background: var(--white);
  border: 1px solid var(--border);
  border-radius: var(--radius);
  padding: 16px 20px;
}
.profile-bar-text {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 10px;
  font-size: 13px;
}
.profile-bar-link { color: var(--blue); cursor: pointer; font-weight: 500; text-decoration: none; font-size: 13px; }
.profile-bar-track {
  height: 6px;
  background: var(--bg);
  border-radius: 3px;
  overflow: hidden;
  margin-bottom: 8px;
}
.profile-bar-fill { height: 100%; background: var(--blue); border-radius: 3px; }
.profile-bar-hint { font-size: 11px; color: var(--text-muted); }
```

- [ ] **Step 3: Open in browser, click "Dashboard" in the sidebar**

You should see: greeting "Bom dia, Maria 👋", 3 agent cards (Marketing, Finanças, RH-locked), 4 artifact chips, and the profile completeness bar. Clicking "Ir para o agente →" buttons should navigate to empty views (not yet built).

- [ ] **Step 4: Commit**

```bash
git add cleo-ai-prototype.html
git commit -m "feat: add home dashboard with agent cards, artifacts strip, and profile bar"
```

---

## Task 4: Marketing Agent Workspace

**Files:**
- Modify: `cleo-ai-prototype.html` — marketing view HTML, workspace CSS, pill + send JS

- [ ] **Step 1: Replace `<!-- Task 4 -->` inside `#view-marketing` with workspace HTML**

```html
<div class="workspace-header">
  <div>
    <h2 class="workspace-title">📢 Marketing</h2>
    <p class="workspace-sub">Sua especialista em marketing — campanhas, e-mails e conteúdo.</p>
  </div>
</div>

<div class="workspace-body" id="ws-marketing">
  <div class="chat-thread" id="thread-marketing">
    <!-- Agent message -->
    <div class="msg agent-msg">
      <div class="msg-bubble agent-bubble">
        Bem-vinda de volta! Da última vez, estávamos trabalhando na campanha de verão da Eufloria. Já criei dois posts — quer revisar?
      </div>
    </div>
    <!-- Artifact card -->
    <div class="msg agent-msg">
      <div class="artifact-card">
        <div class="artifact-card-icon">📄</div>
        <div class="artifact-card-info">
          <div class="artifact-card-name">Campanha_Verao_Eufloria.docx</div>
          <div class="artifact-card-preview">2 posts para Instagram e TikTok — coleção de verão Eufloria...</div>
          <div class="artifact-card-actions">
            <a class="artifact-action">Ver</a>
            <a class="artifact-action">Baixar</a>
          </div>
        </div>
      </div>
    </div>
    <!-- User message -->
    <div class="msg user-msg">
      <div class="msg-bubble user-bubble">Ficou ótimo! Pode redigir o e-mail de lançamento também?</div>
    </div>
    <!-- Agent response -->
    <div class="msg agent-msg">
      <div class="msg-bubble agent-bubble">Claro! Aqui está um rascunho do e-mail de lançamento para a sua lista:</div>
    </div>
    <!-- Artifact card -->
    <div class="msg agent-msg">
      <div class="artifact-card">
        <div class="artifact-card-icon">✉️</div>
        <div class="artifact-card-info">
          <div class="artifact-card-name">Email_Lancamento_Colecao.txt</div>
          <div class="artifact-card-preview">Assunto: A nova coleção chegou — e foi feita para você ☀️...</div>
          <div class="artifact-card-actions">
            <a class="artifact-action">Ver</a>
            <a class="artifact-action">Baixar</a>
          </div>
        </div>
      </div>
    </div>
  </div>

  <div class="input-area">
    <div class="skill-pills">
      <button class="pill" onclick="fillInput('marketing', 'Criar uma campanha nas redes sociais para ')">Campanha nas redes sociais</button>
      <button class="pill" onclick="fillInput('marketing', 'Criar uma sequência de e-mails sobre ')">Sequência de e-mails</button>
      <button class="pill" onclick="fillInput('marketing', 'Redigir um texto de anúncio para ')">Texto de anúncio</button>
      <button class="pill" onclick="fillInput('marketing', 'Auditar a comunicação atual da Eufloria e ')">Auditar comunicação</button>
      <button class="pill" onclick="fillInput('marketing', 'Criar um brief de conteúdo para ')">Brief de conteúdo</button>
    </div>
    <div class="input-row">
      <input class="chat-input" id="input-marketing" type="text" placeholder="Rode uma skill ou pergunte qualquer coisa..." />
      <button class="send-btn" onclick="sendMessage('marketing')">Enviar</button>
    </div>
  </div>
</div>
```

- [ ] **Step 2: Add workspace CSS inside `<style>` (append after dashboard rules)**

```css
/* ── WORKSPACE ── */
.workspace-header {
  padding: 24px 32px 16px;
  background: var(--white);
  border-bottom: 1px solid var(--border);
}
.workspace-title { font-size: 18px; font-weight: 700; margin-bottom: 4px; }
.workspace-sub { font-size: 12px; color: var(--text-muted); }
.workspace-body {
  display: flex;
  flex-direction: column;
  flex: 1;
  height: 0; /* forces flex child to not overflow */
  min-height: 0;
}
.chat-thread {
  flex: 1;
  overflow-y: auto;
  padding: 24px 32px;
  display: flex;
  flex-direction: column;
  gap: 12px;
}
.msg { display: flex; }
.agent-msg { justify-content: flex-start; }
.user-msg { justify-content: flex-end; }
.msg-bubble {
  max-width: 60%;
  padding: 10px 14px;
  border-radius: 10px;
  font-size: 13px;
  line-height: 1.55;
}
.agent-bubble { background: var(--blue-light); color: var(--blue); border-bottom-left-radius: 2px; }
.user-bubble { background: var(--white); border: 1px solid var(--border); color: var(--text); border-bottom-right-radius: 2px; }

/* artifact card in thread */
.artifact-card {
  display: flex;
  align-items: flex-start;
  gap: 12px;
  background: var(--white);
  border: 1px solid var(--border);
  border-radius: var(--radius);
  padding: 12px 16px;
  max-width: 380px;
}
.artifact-card-icon { font-size: 22px; flex-shrink: 0; }
.artifact-card-name { font-size: 13px; font-weight: 600; margin-bottom: 4px; }
.artifact-card-preview { font-size: 11px; color: var(--text-muted); line-height: 1.4; margin-bottom: 8px; }
.artifact-card-actions { display: flex; gap: 12px; }
.artifact-action { font-size: 12px; color: var(--blue); cursor: pointer; font-weight: 500; }
.artifact-action:hover { text-decoration: underline; }

/* input area */
.input-area {
  border-top: 1px solid var(--border);
  background: var(--white);
  padding: 12px 32px 16px;
}
.skill-pills {
  display: flex;
  gap: 8px;
  flex-wrap: wrap;
  margin-bottom: 10px;
}
.pill {
  background: var(--blue-light);
  color: var(--blue);
  border: none;
  border-radius: 20px;
  padding: 5px 13px;
  font-size: 12px;
  font-weight: 500;
  cursor: pointer;
  font-family: inherit;
}
.pill:hover { background: var(--blue-mid); }
.input-row { display: flex; gap: 8px; }
.chat-input {
  flex: 1;
  border: 1px solid var(--border);
  border-radius: 6px;
  padding: 9px 14px;
  font-size: 13px;
  font-family: inherit;
  outline: none;
  background: var(--bg);
}
.chat-input:focus { border-color: var(--blue); background: var(--white); }
.send-btn {
  background: var(--blue);
  color: white;
  border: none;
  border-radius: 6px;
  padding: 9px 18px;
  font-size: 13px;
  font-weight: 600;
  cursor: pointer;
  font-family: inherit;
}
.send-btn:hover { background: #2d5ce0; }
```

- [ ] **Step 3: Add `fillInput` and `sendMessage` JS functions inside `<script>` (after `showView`)**

```javascript
function fillInput(workspace, text) {
  const input = document.getElementById('input-' + workspace);
  input.value = text;
  input.focus();
}

function sendMessage(workspace) {
  const input = document.getElementById('input-' + workspace);
  const text = input.value.trim();
  if (!text) return;

  const thread = document.getElementById('thread-' + workspace);

  // append user message
  const userMsg = document.createElement('div');
  userMsg.className = 'msg user-msg';
  userMsg.innerHTML = '<div class="msg-bubble user-bubble">' + escapeHtml(text) + '</div>';
  thread.appendChild(userMsg);

  // append agent reply
  const agentMsg = document.createElement('div');
  agentMsg.className = 'msg agent-msg';
  agentMsg.innerHTML = '<div class="msg-bubble agent-bubble">Entendido! Estou preparando isso para a Eufloria agora. Um momento...</div>';
  thread.appendChild(agentMsg);

  input.value = '';
  thread.scrollTop = thread.scrollHeight;
}

function escapeHtml(text) {
  return text.replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;');
}
```

- [ ] **Step 4: Open in browser, click "Marketing" in the sidebar**

You should see: workspace header, pre-populated conversation with two artifact cards, skill pills above the input bar. Clicking a pill should pre-fill the input. Typing a message and clicking "Enviar" should append user and agent bubbles.

- [ ] **Step 5: Commit**

```bash
git add cleo-ai-prototype.html
git commit -m "feat: add marketing agent workspace with chat, skill pills, and artifact cards"
```

---

## Task 5: Finance Agent Workspace

**Files:**
- Modify: `cleo-ai-prototype.html` — finance view HTML (reuses workspace CSS from Task 4)

- [ ] **Step 1: Replace `<!-- Task 5 -->` inside `#view-finance` with workspace HTML**

```html
<div class="workspace-header">
  <div>
    <h2 class="workspace-title">💰 Finanças</h2>
    <p class="workspace-sub">Sua especialista financeira — receitas, faturas e fluxo de caixa.</p>
  </div>
</div>

<div class="workspace-body" id="ws-finance">
  <div class="chat-thread" id="thread-finance">
    <div class="msg agent-msg">
      <div class="msg-bubble agent-bubble">
        Olá! Sou sua especialista financeira. Posso ajudar a acompanhar receitas, redigir faturas e identificar riscos no fluxo de caixa. Por onde quer começar?
      </div>
    </div>
  </div>

  <div class="input-area">
    <div class="skill-pills">
      <button class="pill" onclick="fillInput('finance', 'Resumir receitas e despesas de ')">Resumo de receitas e despesas</button>
      <button class="pill" onclick="fillInput('finance', 'Redigir uma fatura para ')">Redigir fatura</button>
      <button class="pill" onclick="fillInput('finance', 'Identificar gaps no fluxo de caixa de ')">Gaps no fluxo de caixa</button>
      <button class="pill" onclick="fillInput('finance', 'Criar um snapshot de orçamento para ')">Snapshot de orçamento</button>
    </div>
    <div class="input-row">
      <input class="chat-input" id="input-finance" type="text" placeholder="Rode uma skill ou pergunte qualquer coisa..." />
      <button class="send-btn" onclick="sendMessage('finance')">Enviar</button>
    </div>
  </div>
</div>
```

- [ ] **Step 2: Open in browser, click "Finanças" in the sidebar**

You should see: workspace header, a single agent greeting bubble (empty state), skill pills, and input bar. Sending a message should work the same as Marketing.

- [ ] **Step 3: Commit**

```bash
git add cleo-ai-prototype.html
git commit -m "feat: add finance agent workspace (empty state)"
```

---

## Task 6: Profile View

**Files:**
- Modify: `cleo-ai-prototype.html` — profile view HTML, profile CSS, collapsible + edit JS

- [ ] **Step 1: Replace `<!-- Task 6 -->` inside `#view-profile` with profile HTML**

```html
<div class="view-header">
  <div style="display:flex;justify-content:space-between;align-items:flex-start;">
    <div>
      <h1 class="greeting">Eufloria</h1>
      <p class="greeting-sub">Moda feminina · E-commerce · Brasil</p>
    </div>
    <button class="go-btn" style="margin-top:4px">Editar perfil</button>
  </div>
  <div class="profile-bar-block" style="margin-top:16px;border:none;padding:0">
    <div class="profile-bar-text">
      <span style="font-size:12px">Perfil <strong>70% completo</strong> — adicione precificação e tamanho do time</span>
    </div>
    <div class="profile-bar-track">
      <div class="profile-bar-fill" style="width:70%"></div>
    </div>
  </div>
</div>

<div class="profile-body">

  <div class="profile-section">
    <div class="profile-section-header" onclick="toggleSection(this)">
      <span class="profile-section-title">Identidade</span>
      <span class="profile-chevron">▾</span>
    </div>
    <div class="profile-section-body">
      <div class="profile-field">
        <div class="profile-field-label">Nome da empresa</div>
        <div class="profile-field-value" contenteditable="true">Eufloria</div>
      </div>
      <div class="profile-field">
        <div class="profile-field-label">Setor</div>
        <div class="profile-field-value" contenteditable="true">Moda feminina — e-commerce</div>
      </div>
      <div class="profile-field">
        <div class="profile-field-label">Descrição</div>
        <div class="profile-field-value" contenteditable="true">E-commerce brasileiro de roupas femininas com identidade própria, focado em peças exclusivas e produção sustentável.</div>
      </div>
      <div class="profile-field">
        <div class="profile-field-label">Tom de voz</div>
        <div class="profile-field-value" contenteditable="true">Sofisticado, próximo e feminino</div>
      </div>
      <button class="rerun-btn">Refazer entrevista com IA</button>
    </div>
  </div>

  <div class="profile-section">
    <div class="profile-section-header" onclick="toggleSection(this)">
      <span class="profile-section-title">Produtos & Serviços</span>
      <span class="profile-chevron">▾</span>
    </div>
    <div class="profile-section-body">
      <div class="profile-field">
        <div class="profile-field-label">Produtos principais</div>
        <div class="profile-field-value" contenteditable="true">Roupas femininas exclusivas: vestidos, conjuntos, blusas e acessórios. Coleções sazonais com edições limitadas.</div>
      </div>
      <div class="profile-field">
        <div class="profile-field-label">Precificação</div>
        <div class="profile-field-value empty" contenteditable="true">Não informado — clique para adicionar</div>
      </div>
      <button class="rerun-btn">Refazer entrevista com IA</button>
    </div>
  </div>

  <div class="profile-section">
    <div class="profile-section-header" onclick="toggleSection(this)">
      <span class="profile-section-title">Público-alvo</span>
      <span class="profile-chevron">▾</span>
    </div>
    <div class="profile-section-body">
      <div class="profile-field">
        <div class="profile-field-label">Cliente ideal</div>
        <div class="profile-field-value" contenteditable="true">Mulheres entre 25–40 anos, Brasil, interessadas em moda consciente e estilo autoral. Valorizam exclusividade e sustentabilidade.</div>
      </div>
      <div class="profile-field">
        <div class="profile-field-label">Tamanho do time</div>
        <div class="profile-field-value empty" contenteditable="true">Não informado — clique para adicionar</div>
      </div>
      <button class="rerun-btn">Refazer entrevista com IA</button>
    </div>
  </div>

  <div class="profile-section">
    <div class="profile-section-header" onclick="toggleSection(this)">
      <span class="profile-section-title">Desafios & Objetivos</span>
      <span class="profile-chevron">▾</span>
    </div>
    <div class="profile-section-body">
      <div class="profile-field">
        <div class="profile-field-label">Desafios atuais</div>
        <div class="profile-field-value" contenteditable="true">Produzir conteúdo para redes sociais com consistência sem aumentar o time. Entender melhor o retorno de cada campanha.</div>
      </div>
      <div class="profile-field">
        <div class="profile-field-label">Objetivos</div>
        <div class="profile-field-value" contenteditable="true">Lançar coleção de inverno com campanha integrada. Aumentar recorrência de compra da base de clientes.</div>
      </div>
      <button class="rerun-btn">Refazer entrevista com IA</button>
    </div>
  </div>

  <div class="profile-section">
    <div class="profile-section-header" onclick="toggleSection(this)">
      <span class="profile-section-title">Agentes</span>
      <span class="profile-chevron">▾</span>
    </div>
    <div class="profile-section-body">
      <div class="profile-field">
        <div class="profile-field-label">Marketing</div>
        <div class="profile-field-value">✅ Ativo</div>
      </div>
      <div class="profile-field">
        <div class="profile-field-label">Finanças</div>
        <div class="profile-field-value">✅ Ativo</div>
      </div>
      <div class="profile-field">
        <div class="profile-field-label">RH</div>
        <div class="profile-field-value" style="color:var(--text-muted)">🔒 Bloqueado — disponível no plano Pro</div>
      </div>
    </div>
  </div>

</div>
```

- [ ] **Step 2: Add profile CSS inside `<style>` (append)**

```css
/* ── PROFILE ── */
.profile-body { padding: 24px 32px; display: flex; flex-direction: column; gap: 12px; }
.profile-section {
  background: var(--white);
  border: 1px solid var(--border);
  border-radius: var(--radius);
  overflow: hidden;
}
.profile-section-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 14px 18px;
  cursor: pointer;
  user-select: none;
}
.profile-section-header:hover { background: var(--bg); }
.profile-section-title { font-weight: 600; font-size: 13px; }
.profile-chevron { color: var(--text-muted); font-size: 12px; transition: transform 0.2s; }
.profile-section.collapsed .profile-section-body { display: none; }
.profile-section.collapsed .profile-chevron { transform: rotate(-90deg); }
.profile-section-body { padding: 0 18px 16px; border-top: 1px solid var(--border); }
.profile-field { padding: 12px 0; border-bottom: 1px solid var(--bg); }
.profile-field:last-of-type { border-bottom: none; }
.profile-field-label { font-size: 10px; font-weight: 700; color: var(--text-muted); letter-spacing: 0.07em; margin-bottom: 4px; }
.profile-field-value {
  font-size: 13px;
  color: var(--text);
  line-height: 1.5;
  outline: none;
  border-radius: 4px;
  padding: 2px 4px;
  margin: -2px -4px;
}
.profile-field-value:focus { background: var(--blue-light); }
.profile-field-value.empty { color: var(--text-muted); font-style: italic; }
.rerun-btn {
  margin-top: 12px;
  background: none;
  border: 1px solid var(--border);
  color: var(--text-muted);
  border-radius: 6px;
  padding: 6px 12px;
  font-size: 12px;
  cursor: pointer;
  font-family: inherit;
}
.rerun-btn:hover { border-color: var(--blue); color: var(--blue); }
```

- [ ] **Step 3: Add `toggleSection` JS function inside `<script>` (append)**

```javascript
function toggleSection(header) {
  header.parentElement.classList.toggle('collapsed');
}
```

- [ ] **Step 4: Open in browser, click "Perfil" in sidebar**

You should see: Eufloria header, 70% progress bar, and 5 collapsible sections. Clicking a section header collapses/expands it. Clicking a field value should make it editable (blue highlight). "Não informado" fields in Produtos and Público-alvo should appear in italic muted grey.

- [ ] **Step 5: Commit**

```bash
git add cleo-ai-prototype.html
git commit -m "feat: add profile view with Eufloria data, collapsible sections, inline editing"
```

---

## Task 7: HR Locked State + Final Polish

**Files:**
- Modify: `cleo-ai-prototype.html` — HR view HTML + locked state CSS

- [ ] **Step 1: Replace `<!-- Task 7 -->` inside `#view-hr` with locked state HTML**

```html
<div class="view-header">
  <h2 class="workspace-title">👥 RH</h2>
  <p class="workspace-sub">Automatize descrições de cargo, onboarding e comunicações internas.</p>
</div>
<div class="locked-view">
  <div class="locked-icon">🔒</div>
  <h3 class="locked-title">Agente de RH bloqueado</h3>
  <p class="locked-desc">Faça upgrade para o plano Pro para desbloquear o agente de RH e automatizar descrições de cargo, onboarding, políticas internas e muito mais.</p>
  <button class="go-btn">Fazer upgrade para Pro →</button>
</div>
```

- [ ] **Step 2: Add locked view CSS inside `<style>` (append)**

```css
/* ── LOCKED VIEW ── */
.locked-view {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 14px;
  text-align: center;
  padding: 40px;
}
.locked-icon { font-size: 40px; opacity: 0.4; }
.locked-title { font-size: 18px; font-weight: 700; }
.locked-desc { font-size: 13px; color: var(--text-muted); max-width: 360px; line-height: 1.6; }
```

- [ ] **Step 3: Open in browser and do a full walkthrough**

Check each view in order:
1. **Dashboard** — greeting, 3 agent cards, artifact chips, profile bar, "Ir para o agente" buttons work
2. **Marketing** — header, pills, pre-populated conversation, artifact cards, pill click pre-fills input, send appends messages
3. **Finanças** — header, empty state greeting, pills, send works
4. **RH** — locked state with upgrade message
5. **Perfil** — Eufloria data, collapsible sections, inline editing, "Não informado" fields, profile bar

Fix any visual misalignments you notice during this walkthrough.

- [ ] **Step 4: Final commit**

```bash
git add cleo-ai-prototype.html
git commit -m "feat: add HR locked state — Cleo AI prototype complete"
```

---

## Self-Review Notes

- All spec requirements covered: Home Dashboard ✓, Marketing workspace ✓, Finance workspace ✓, Profile view ✓, HR locked state ✓, labeled sidebar ✓, Portuguese content ✓, Eufloria sample data ✓, skill pills ✓, inline artifacts ✓, profile completeness bar ✓, collapsible sections ✓, inline editing ✓
- `fillInput` and `sendMessage` use workspace ID consistently (`'marketing'`, `'finance'`) — thread and input IDs match (`thread-marketing`, `input-marketing`, etc.)
- `escapeHtml` is defined before `sendMessage` uses it
- No TBD or placeholder content — all copy is in Portuguese with real Eufloria data
