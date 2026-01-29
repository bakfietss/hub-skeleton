# Workflow Overzicht - Versnel Digitaal

Dit document beschrijft PRECIES wat je doet, stap voor stap.

---

## De Kern: Git-Based Deployment

```
JOUW WERK-PC                      GITHUB                    KLANT SERVER
┌─────────────────┐              ┌───────┐               ┌─────────────────┐
│ solutions/      │              │       │               │ C:\Projects\    │
│  └─klant-x/     │ ── push ──▶  │ repo  │  ◀── pull ── │  └─klant-x\     │
│                 │              │       │               │                 │
│ • Code aanpassen│              │       │               │ • git pull      │
│ • Workflows     │              │       │               │ • docker up     │
│ • Claude agents │              │       │               │                 │
└─────────────────┘              └───────┘               └─────────────────┘
```

**Jij beheert ALTIJD de broncode. Server draait ALTIJD laatste versie.**

---

## Jouw Setup (Werk-PC)

```
C:\Users\ricks\VersnelDigitaal\     ← ALTIJD HIER STARTEN
│
├── .claude/agents/                  ← AI agents (IP beschermd)
├── .planning/                       ← Hub-level GSD planning
├── deploy/
│   ├── scripts/                     ← Deployment scripts
│   └── templates/                   ← Project templates
├── docs/                            ← Documentatie
├── solutions/                       ← SOLUTIONS (twee patterns!)
│   ├── agile-assistant/             ← Pattern A: GEEN eigen .git
│   ├── RAG-automation/              ← Pattern B: EIGEN .git
│   └── Flow-mapper/                 ← Pattern B: EIGEN .git
└── CHANGELOG.md                     ← Hub wijzigingen
```

### BELANGRIJK: Twee Solution Patterns

| Pattern | Voorbeeld | Git | Wanneer |
|---------|-----------|-----|---------|
| **A: Hub-Centric** | agile-assistant | Hub repo | Development, intern |
| **B: Solution-Centric** | RAG-automation | Eigen repo | Verkoopbaar product |

**Zie `docs/SOLUTION-WORKFLOW.md` voor volledige uitleg!**

---

## Git Commit Workflow (Automatisch)

### Commit Convention

Gebruik tags in je commit messages:

```
[FEAT] nieuwe feature toegevoegd     → Added sectie
[FIX] bug opgelost                   → Fixed sectie
[DOCS] documentatie bijgewerkt       → Documentation sectie
[REFACTOR] code opgeschoond          → Refactored sectie
[CHORE] maintenance taken            → Changed sectie
[WIP] work in progress               → NIET in changelog
[TASK-001] agile task                → Changed + task ID
```

### Wat Gebeurt Automatisch

```
1. JIJ COMMIT
   git commit -m "[FEAT] nieuwe zoekfunctie"
                    │
                    ▼
2. POST-COMMIT HOOK draait
   → Voegt "TODO:" entry toe aan CHANGELOG.md
   → Je ziet: "📝 CHANGELOG.md updated"
                    │
                    ▼
3. JIJ EDIT CHANGELOG
   → Vervang "TODO:" met echte beschrijving
   → Commit de CHANGELOG update
                    │
                    ▼
4. JIJ PUSHT
   git push
                    │
                    ▼
5. PRE-PUSH HOOK CHECKT
   ✅ CHANGELOG.md is modified?
   ✅ Geen "TODO:" markers meer?
   → Als OK: push gaat door
   → Als NIET OK: push geblokkeerd
```

### Git Hooks Installeren (per repo)

```bash
# Vanuit repo root:
../../deploy/scripts/install-hooks.sh

# Of handmatig:
cp deploy/templates/hooks/* .git/hooks/
chmod +x .git/hooks/*
```

---

## Dagelijkse Workflow

### Scenario 1: Werken aan een Solution

```
1. Open terminal in: C:\Users\ricks\VersnelDigitaal

2. Werk aan je solution:
   - Code aanpassen in solutions/RAG-automation/
   - Workflows maken/testen in lokale N8N
   - Export workflows naar solutions/RAG-automation/workflows/

3. Commit je werk (dagelijks of per feature):
   git add .
   git commit -m "Beschrijving van wat je deed"
   git push

4. Klaar voor deploy? Zie "Deployment" hieronder
```

### Scenario 2: Nieuwe Solution Maken

```
1. Maak nieuwe solution folder:
   mkdir solutions/nieuwe-solution

2. Kopieer basis structuur:
   - docker-compose.yml (van templates)
   - deploy/docker-compose.prod.yml
   - workflows/
   - docs/

3. Ontwikkel de solution lokaal

4. Als klaar: deploy naar server
```

### Scenario 3: Deployment naar Server

```
EERSTE KEER (nieuwe server/klant):
─────────────────────────────────
1. Run setup script:
   ./deploy/scripts/setup-client.sh user@server-ip

2. SSH naar server en configureer:
   ssh user@server-ip
   nano /opt/infrastructure/.env      ← Credentials invullen
   nano /opt/infrastructure/Caddyfile ← Domeinen invullen
   cd /opt/infrastructure
   docker compose up -d

3. Test of N8N werkt:
   Open https://n8n.domein.com in browser

DAARNA (solution deployen):
───────────────────────────
1. Deploy solution:
   ./deploy/scripts/deploy-solution.sh user@server-ip rag-automation

2. Import workflows in N8N UI

3. Test of alles werkt
```

---

## Wat Heb Je Nodig?

### Op Jouw Werk-PC

| Tool | Waarom | Check |
|------|--------|-------|
| Git | Code beheer | `git --version` |
| SSH | Server toegang | `ssh -V` |
| rsync | Files syncen | `rsync --version` |
| Docker Desktop | Lokaal testen | `docker --version` |
| VS Code / Editor | Code schrijven | - |
| Terminal / Git Bash | Commands uitvoeren | - |

### Op De Server

| Tool | Waarom | Wie installeert |
|------|--------|-----------------|
| Docker | Containers draaien | Setup script |
| Open poorten (80, 443) | Web toegang | Klant/hosting |
| SSH toegang | Jij kunt erbij | Klant/hosting |
| Domein + DNS | HTTPS werkt | Klant |

---

## Lokaal Testen (Voordat Je Deployed)

### Optie A: Test met Docker Desktop

```bash
# In solutions/RAG-automation/
docker compose up -d

# Check of het werkt
docker compose ps
docker compose logs -f

# Stop als klaar
docker compose down
```

### Optie B: Test op Eigen Server

Je hebt al een server met Qdrant. Gebruik die als test-omgeving:

```bash
# Eerste keer: setup infrastructure
./deploy/scripts/setup-client.sh ricks@jouw-server-ip

# Deploy RAG solution
./deploy/scripts/deploy-solution.sh ricks@jouw-server-ip rag-automation
```

---

## Git Workflow (Simpel)

```bash
# Dagelijks of na elke feature:

# 1. Zie wat je veranderd hebt
git status

# 2. Voeg alles toe
git add .

# 3. Commit met beschrijving
git commit -m "feat: nieuwe RAG workflow toegevoegd"

# 4. Push naar GitHub
git push
```

### Commit Message Conventies

```
feat: nieuwe feature
fix: bug fix
docs: documentatie update
refactor: code opschonen
```

---

## Checklist: Wat Mis Je Misschien?

### Lokale Ontwikkeling
- [ ] Docker Desktop geïnstalleerd?
- [ ] Kun je lokaal `docker compose up` draaien?
- [ ] Heb je een lokale N8N om workflows te ontwikkelen?

### Server Toegang
- [ ] SSH key aangemaakt? (`ssh-keygen` als niet)
- [ ] SSH key toegevoegd aan server?
- [ ] Kun je `ssh user@server` doen zonder wachtwoord?

### Git/GitHub
- [ ] Git geconfigureerd? (`git config --global user.name "Naam"`)
- [ ] GitHub account gekoppeld?
- [ ] Kun je pushen naar de repo?

### Domeinen (voor productie)
- [ ] Heb je een domein?
- [ ] Kun je DNS records aanmaken?
- [ ] Of test je eerst met IP + poort?

### API Keys (voor RAG)
- [ ] Anthropic API key?
- [ ] Andere API keys die je workflows nodig hebben?

---

## Veelgestelde Vragen

### "Waar bewaar ik klant credentials?"

NIET in git! Gebruik:
- Password manager (1Password, Bitwarden)
- Encrypted notes
- `deploy/templates/client-config.template.md` als format

### "Wat als ik iets kapot maak?"

```bash
# Laatste commit ongedaan maken (lokaal)
git reset --soft HEAD~1

# Of: terug naar laatste werkende versie
git checkout -- .
```

### "Hoe update ik een solution die al draait?"

```bash
# Sync nieuwe versie
./deploy/scripts/deploy-solution.sh user@server solution-name

# Of handmatig:
rsync -avz solutions/RAG-automation/ user@server:/opt/solutions/rag-automation/
ssh user@server "cd /opt/solutions/rag-automation && docker compose up -d"
```

### "Hoe backup ik data op de server?"

```bash
ssh user@server

# Backup Qdrant data
docker run --rm -v rag-automation_qdrant_data:/data -v ~/backups:/backup \
  alpine tar czf /backup/qdrant-$(date +%Y%m%d).tar.gz /data

# Backup N8N data
docker run --rm -v infrastructure_n8n_data:/data -v ~/backups:/backup \
  alpine tar czf /backup/n8n-$(date +%Y%m%d).tar.gz /data
```

---

## Samenvatting: Jouw Dagelijkse Routine

```
OCHTEND:
1. Open terminal in VersnelDigitaal folder
2. git pull (haal laatste versie op)

WERKEN:
3. Werk aan solutions, test lokaal
4. Commit regelmatig: git add . && git commit -m "..."

EINDE DAG:
5. git push (alles naar GitHub)

DEPLOYMENT (wanneer klaar):
6. ./deploy/scripts/deploy-solution.sh user@server solution-name
7. Test op server
8. Informeer klant
```

---

## Hulp Nodig?

- **Technische issues:** Vraag Claude (mij)
- **Git problemen:** `git status` en `git log` tonen wat er aan de hand is
- **Docker problemen:** `docker compose logs -f` toont errors
- **Server problemen:** `ssh user@server` en dan `docker compose ps`

---

## Windows Server Deployment

De meeste klanten hebben Windows servers. Hier is de specifieke workflow.

### Eerste Keer Setup (op Windows Server)

Via Remote Desktop inloggen op de server, dan PowerShell openen:

```powershell
# 1. Maak project folder
mkdir C:\Projects
cd C:\Projects

# 2. Clone het project
git clone https://github.com/VersnelDigitaal/RAG-automation.git
cd RAG-automation

# 3. Kopieer env template en vul in
copy deploy\.env.example .env
notepad .env

# 4. Start met production config
docker compose -f deploy/docker-compose.prod.yml up -d

# 5. Check of het draait
docker ps
```

### Updates Deployen (op Windows Server)

```powershell
cd C:\Projects\RAG-automation
git pull
docker compose -f deploy/docker-compose.prod.yml up -d
```

### Toegang op Afstand (zonder RDP)

Zodra de server draait, kun je via je browser:

| Service | URL | Wat kun je doen |
|---------|-----|-----------------|
| N8N | `http://server-ip:5678` | Workflows beheren |
| Qdrant | `http://server-ip:6333/dashboard` | Vector data bekijken |

**Je hoeft alleen RDP te gebruiken voor:**
- Eerste installatie
- Git pull + docker restart
- .env credentials wijzigen
- Troubleshooting

---

## Samenvatting per Server Type

| Server Type | Eerste Setup | Updates | Dagelijks Beheer |
|-------------|--------------|---------|------------------|
| **Windows** | RDP → git clone → docker up | RDP → git pull → docker up | Browser (N8N/Qdrant UI) |
| **Linux** | SSH script of handmatig | SSH → git pull → docker up | Browser (N8N/Qdrant UI) |
