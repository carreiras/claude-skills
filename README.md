# 🧠 claude-skills

**Biblioteca pessoal de Claude Skills** — segurança, conformidade regulatória brasileira e governança de produto para projetos SaaS.

Desenvolvida por **Ewerton Carreira** para uso com [Claude Code](https://docs.claude.ai/code) e [Cowork](https://claude.ai/cowork).

---

## O que são Skills?

Skills são pacotes de conhecimento estruturado que o Claude carrega sob demanda. Em vez de repetir contexto em cada conversa, a skill é acionada automaticamente quando o tema é reconhecido — e o Claude passa a operar com a profundidade e a persona definidas nela.

Cada `.skill` contém:
- Um `SKILL.md` com `description` (gatilhos de acionamento), `persona` e metadados
- Arquivos de referência em `references/` com o conhecimento técnico detalhado

---

## Skills disponíveis

### 🔒 Segurança

| Skill | Arquivo | O que faz |
|---|---|---|
| **security-backend** | [`security-backend.skill`](./security-backend.skill) | Desenvolvimento seguro de APIs e backends — autenticação, injeções, criptografia, rate limiting, secrets, deploy |
| **security-frontend** | [`security-frontend.skill`](./security-frontend.skill) | Segurança em aplicações web — XSS, CSRF, CSP, armazenamento no browser, OAuth no cliente, dependências npm |
| **security-mcp-review** | [`security-mcp-review.skill`](./security-mcp-review.skill) | Análise de risco de MCPs de terceiros — superfície de ataque, publisher, fluxo de dados, CVEs, parecer técnico |

### ⚖️ Conformidade Regulatória Brasileira

| Skill | Arquivo | O que faz |
|---|---|---|
| **security-lgpd** | [`security-lgpd.skill`](./security-lgpd.skill) | LGPD (Lei 13.709/2018) — bases legais, direitos do titular, ROPA, DPIA, consentimento, incidentes, DPO |
| **security-marco-civil** | [`security-marco-civil.skill`](./security-marco-civil.skill) | Marco Civil da Internet (Lei 12.965/2014) — retenção de logs, requisição judicial, responsabilidade de provedores |
| **security-pci-dss** | [`security-pci-dss.skill`](./security-pci-dss.skill) | PCI-DSS v4.0 — escopo CDE, tokenização, proteção de PAN/SAD, controles de rede, SAQs, checklist de conformidade |

### 📋 Governança de Produto

| Skill | Arquivo | O que faz |
|---|---|---|
| **prd-reference** | [`prd-reference.skill`](./prd-reference.skill) | Quando e como atualizar o PRD — critérios de decisão estrutural, aprovação, anatomia de uma edição saudável |
| **feature-spec** | [`feature-spec.skill`](./feature-spec.skill) | Planejamento e documentação de features — spec compacto, ciclo de vida (rascunho → dev → homolog → arquivado) |

---

## Como instalar

### No Cowork (Claude Desktop)

1. Abra o Cowork
2. Vá em **Skills → Instalar skill**
3. Arraste o arquivo `.skill` desejado ou selecione via navegador de arquivos

### No Claude Code

```bash
# Copiar o .skill para o diretório de skills do projeto
cp security-lgpd.skill /caminho/do/projeto/.claude/skills/

# Ou instalar globalmente
cp security-lgpd.skill ~/.claude/skills/
```

### Clonar o repositório

```bash
git clone https://github.com/carreiras/claude-skills.git
cd claude-skills
```

---

## Como as skills são acionadas

Cada skill tem gatilhos definidos na `description` do frontmatter. Exemplos:

| Você digita... | Skill acionada |
|---|---|
| *"esse endpoint está seguro?"* | `security-backend` |
| *"preciso de consentimento para isso?"* | `security-lgpd` |
| *"posso liberar esse MCP para o cliente?"* | `security-mcp-review` |
| *"por quanto tempo guardar os logs?"* | `security-marco-civil` |
| *"posso armazenar o CVV?"* | `security-pci-dss` |
| *"devo atualizar o PRD?"* | `prd-reference` |
| *"vamos criar um feature spec"* | `feature-spec` |

---

## Estrutura do repositório

```
claude-skills/
├── feature-spec/               # Fontes da skill (SKILL.md + references/)
├── prd-reference/
├── security-backend/
├── security-frontend/
├── security-lgpd/
├── security-marco-civil/
├── security-mcp-review/
├── security-pci-dss/
│
├── feature-spec.skill          # Pacote instalável
├── prd-reference.skill
├── security-backend.skill
├── security-frontend.skill
├── security-lgpd.skill
├── security-marco-civil.skill
├── security-mcp-review.skill
└── security-pci-dss.skill
```

Cada pasta de fonte contém:
```
security-lgpd/
├── SKILL.md                    # Frontmatter + persona + mapa de referências
└── references/
    ├── 01-fundamentos-lgpd.md
    ├── 02-direitos-titular.md
    └── ...
```

---

## Personas

Cada skill opera com uma persona distinta, calibrada para o domínio:

| Skill | Persona |
|---|---|
| `security-backend` | Engenheiro sênior de segurança — direto, aponta vulnerabilidades com evidência, propõe mitigações concretas |
| `security-frontend` | Especialista em segurança web — foca no impacto real ao usuário, desconfia de "isso nunca vai acontecer" |
| `security-lgpd` | Consultor de privacidade — cita artigos, recomenda interpretação conservadora, trata conformidade como processo |
| `security-marco-civil` | Especialista em direito digital — traduz lei em requisito de engenharia, preciso sobre prazos |
| `security-pci-dss` | QSA experiente — primeira pergunta é sempre "o que está no escopo?", firme no que é proibido |
| `security-mcp-review` | Analista de risco cético — todo MCP é suspeito até prova em contrário, produz pareceres inequívocos |
| `prd-reference` | Guardião do PRD — protege contra inflação e desatualização, não confirma o que o usuário quer ouvir |
| `feature-spec` | Redator de Specs Enxuto — escreve o mínimo necessário, referencia em vez de copiar, cobra escopo negativo |

---

## Roadmap

Skills planejadas para próximas versões:

- [ ] `security-healthcare` — CFM, dados de saúde, prontuário eletrônico, telemedicina
- [ ] `security-marco-civil-criancas` — Proteção de menores na internet, interseção com ECA e LGPD
- [ ] `security-pci-brasil` — Contexto brasileiro: PIX, Open Finance, Elo, ABECS
- [ ] `security-lgpd-frontend` — Banners de consentimento, cookies, opt-in/opt-out
- [ ] `security-lgpd-marco-civil` — Skill combinada para sistemas que precisam dos dois frameworks

---

## Metadados

```yaml
author: Ewerton Carreira
version: v1
language: pt-BR
target: Claude Code / Cowork
```

---

> **Aviso:** As skills de conformidade regulatória (LGPD, Marco Civil, PCI-DSS) têm fins informativos e educacionais para times de tecnologia. Para decisões jurídicas definitivas, consulte um advogado especializado.
