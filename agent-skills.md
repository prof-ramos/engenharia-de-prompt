# Agent Skills

Use agent skills para estender o Codex com capacidades específicas para tarefas. Uma skill empacota instruções, recursos e scripts opcionais para que o Codex possa seguir um fluxo de trabalho de forma confiável. Você pode compartilhar skills entre equipes ou com a comunidade. Skills são baseadas no [open agent skills standard](https://agentskills.io).

Skills estão disponíveis no Codex CLI, extensão IDE e app Codex.

Skills usam **divulgação progressiva** para gerenciar contexto de forma eficiente: o Codex começa com os metadados de cada skill (`name`, `description`, caminho do arquivo e metadados opcionais de `agents/openai.yaml`). O Codex carrega as instruções completas do `SKILL.md` apenas quando decide usar uma skill.

## Estrutura de uma Skill

Uma skill é um diretório com um arquivo `SKILL.md` mais scripts e recursos opcionais:

```
skill-name/
├── SKILL.md                    # Obrigatório: instruções da skill
├── scripts/                    # Opcional: scripts de automação
│   └── run.sh
├── templates/                  # Opcional: templates, recursos
└── agents/
    └── openai.yaml             # Opcional: aparência e dependências
```

## Como o Codex usa Skills

O Codex pode ativar skills de duas formas:

1. **Invocação explícita:** Inclua a skill diretamente no seu prompt. No CLI/IDE, execute `/skills` ou digite `$` para mencionar uma skill.
2. **Invocação implícita:** O Codex pode escolher uma skill quando sua tarefa corresponde à `description` da skill.

Como o matching implícito depende da `description`, escreva descrições com escopo e limites claros.

## Criar uma Skill

Use o criador integrado primeiro:

```text
$skill-creator
```

O criador pergunta o que a skill faz, quando deve ser acionada e se deve ser apenas instruções ou incluir scripts. Apenas instruções é o padrão.

Você também pode criar uma skill manualmente criando uma pasta com um arquivo `SKILL.md`:

```md
---
name: nome-da-skill
description: Explique exatamente quando esta skill deve e não deve ser acionada.
---

Instruções da skill para o Codex seguir.
```

O Codex detecta mudanças nas skills automaticamente. Se uma atualização não aparecer, reinicie o Codex.

## Onde salvar Skills

O Codex lê skills de locais de repositório, usuário, admin e sistema. Para repositórios, o Codex escaneia `.agents/skills` em cada diretório do seu diretório de trabalho atual até a raiz do repositório. Se duas skills compartilham o mesmo `name`, o Codex não as mescla; ambas podem aparecer nos seletores de skill.

| Escopo da Skill | Localização | Uso sugerido |
| :---------- | :--- | :--- |
| `REPO` | `$CWD/.agents/skills` <br /> Diretório de trabalho atual: onde você inicia o Codex. | Se você está em um repositório ou ambiente de código, equipes podem commitar skills relevantes para uma pasta de trabalho. Por exemplo, skills relevantes apenas para um microsserviço ou módulo. |
| `REPO` | `$CWD/../.agents/skills` <br /> Uma pasta acima do CWD quando você inicia o Codex dentro de um repositório Git. | Se você está em um repositório com pastas aninhadas, organizações podem commitar skills relevantes. |
| `USER` | `~/.codex/skills` <br /> Skills que se aplicam a qualquer repositório em que o usuário possa trabalhar. | Skills pessoais e templates que se aplicam a qualquer repositório. |
| `ADMIN` | `/etc/codex/skills` <br /> Qualquer skill commitada na máquina ou container em um local compartilhado do sistema. | Use para scripts SDK, automação e para commitar skills admin padrão disponíveis para cada usuário na máquina. |
| `SYSTEM` | Empacotadas com o Codex pela OpenAI. | Skills úteis relevantes para um público amplo, como skill-creator e plan skills. Disponíveis para todos ao iniciar o Codex. |

O Codex suporta pastas de skill com symlink e segue o destino do symlink ao escanear esses locais.

## Instalar Skills

Para instalar skills além das integradas, use `$skill-installer`:

```bash
$skill-installer install the linear skill from the .experimental folder
```

Você também pode pedir ao instalador para baixar skills de outros repositórios. O Codex detecta skills recém-instaladas automaticamente; se uma não aparecer, reinicie o Codex.

## Habilitar ou Desabilitar Skills

Use entradas `[[skills.config]]` em `~/.codex/config.toml` para desabilitar uma skill sem deletá-la:

```toml
[[skills.config]]
path = "/caminho/para/skill/SKILL.md"
enabled = false
```

Reinicie o Codex após alterar `~/.codex/config.toml`.

## Metadados Opcionais

Adicione `agents/openai.yaml` para configurar metadados de UI no [Codex app](https://developers.openai.com/codex/app), para definir política de invocação e declarar dependências de ferramentas para uma experiência mais fluida ao usar a skill.

```yaml
interface:
  display_name: "Nome de exibição opcional"
  short_description: "Descrição de exibição opcional"
  icon_small: "./assets/small-logo.svg"
  icon_large: "./assets/large-logo.png"
  brand_color: "#3B82F6"
  default_prompt: "Prompt opcional para usar a skill com"

policy:
  allow_implicit_invocation: false

dependencies:
  tools:
    - type: "mcp"
      value: "openaiDeveloperDocs"
      description: "OpenAI Docs MCP server"
      transport: "streamable_http"
      url: "https://developers.openai.com/mcp"
```

`allow_implicit_invocation` (padrão: `true`): Quando `false`, o Codex não invocará implicitamente a skill baseado no prompt do usuário; invocação explícita `$skill` ainda funciona.

## Melhores Práticas

- Mantenha cada skill focada em um único trabalho
- Prefira instruções em vez de scripts, a menos que precise de comportamento determinístico ou ferramentas externas
- Escreva passos imperativos com inputs e outputs explícitos
- Teste prompts contra a descrição da skill para confirmar o comportamento de acionamento correto

## Estrutura Completa de Arquivos

```
skill-name/
├── SKILL.md                    # Obrigatório: instruções principais
├── scripts/                    # Opcional: scripts de automação
│   ├── run.sh                  # Script principal
│   └── utils.sh                # Utilitários
├── templates/                  # Opcional: templates e recursos
│   └── example.md
├── assets/                     # Opcional: ícones e imagens
│   ├── small-logo.svg
│   └── large-logo.png
└── agents/
    └── openai.yaml             # Opcional: metadados e configurações
```

## Exemplos de SKILL.md

### Skill Simples (Apenas Instruções)

```md
---
name: commit-helper
description: Ajuda a criar mensagens de commit semânticas e organizadas. Use quando o usuário pedir para commitar código ou criar mensagens de commit.
---

# Commit Helper

Você é um especialista em conventional commits. Sua tarefa é ajudar o usuário a criar mensagens de commit claras e semânticas.

## Formato

Use o padrão Conventional Commits:
- `feat:` para novas funcionalidades
- `fix:` para correções de bugs
- `docs:` para mudanças na documentação
- `style:` para formatação
- `refactor:` para refatoração
- `test:` para testes
- `chore:` para tarefas de manutenção

## Processo

1. Analise as mudanças no código (git diff)
2. Identifique o tipo de mudança
3. Crie uma mensagem clara e concisa
4. Sugira um corpo de mensagem se necessário
```

### Skill com Scripts

```md
---
name: deploy-checker
description: Verifica se o código está pronto para deploy. Use quando o usuário pedir para verificar readiness de deploy ou pré-deploy check.
---

# Deploy Checker

Verifica se o código está pronto para deploy.

## Processo

1. Execute os testes
2. Verifique lint
3. Confirme build
4. Valide variáveis de ambiente

## Script

Execute o script de verificação:

\`\`\`bash
./scripts/check-deploy.sh
\`\`\`

Analise os resultados e forneça feedback sobre prontidão para deploy.
```

---

## Recursos

- [Especificação Agent Skills](https://agentskills.io/specification)
- [Repositório de Skills OpenAI](https://github.com/openai/skills)
- [ClawHub - Marketplace de Skills](https://clawhub.com)

---

*Adaptado da documentação do Codex - Fevereiro 2026*
