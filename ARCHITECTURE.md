# Arquitetura do Projeto

## Estrutura de Diretórios

```
engenharia-de-prompt/
├── .github/
│   └── workflows/
│       └── hugo.yaml              # CI/CD para GitHub Pages
├── content/                       # Conteúdo do site Hugo (FONTE ÚNICA)
│   ├── fundamentos/               # Conceitos básicos
│   │   ├── _index.md
│   │   ├── como-llms-funcionam.md
│   │   └── configuracoes.md
│   ├── tecnicas/                  # 10 técnicas de prompting
│   │   ├── _index.md
│   │   ├── zero-shot.md
│   │   ├── few-shot.md
│   │   ├── prompt-sistema.md
│   │   ├── prompt-papel.md
│   │   ├── prompt-contextual.md
│   │   ├── step-back.md
│   │   ├── cot.md
│   │   ├── auto-consistencia.md
│   │   ├── tot.md
│   │   └── react.md
│   ├── aplicacoes/                # Casos de uso práticos
│   │   ├── _index.md
│   │   ├── codigo.md
│   │   └── ape.md
│   ├── mundo-real/                # Exemplos da Anthropic
│   │   ├── _index.md
│   │   ├── recapitulacao.md
│   │   ├── prompt-medico.md
│   │   ├── processo.md
│   │   ├── resumidor-chamadas.md
│   │   └── bot-suporte.md
│   └── referencia/                # Referência rápida
│       ├── _index.md
│       ├── melhores-praticas.md
│       ├── anti-padroes.md
│       ├── checklist.md
│       ├── templates.md
│       ├── troubleshooting.md
│       └── resumo.md
├── themes/
│   └── PaperMod/                  # Tema Hugo (submodule)
├── docs/
│   └── hugo-config.md             # Documentação de configuração
├── .gitignore
├── .gitmodules
├── .markdownlint.json
├── hugo.toml
├── ARCHITECTURE.md
└── README.md
```

## Fluxo de Build

```
content/*.md → Hugo → public/ (HTML) → GitHub Pages
     ↓
  Themes/PaperMod
```

## Pipeline CI/CD

```
Push → Lint (markdownlint) → Build (Hugo) → Deploy (GitHub Pages)
```

## Dependências

| Dependência | Versão | Propósito |
|-------------|--------|-----------|
| Hugo Extended | 0.146.0 | Build do site |
| PaperMod | latest | Tema visual |
| markdownlint-cli | latest | Lint de markdown |

## Comandos Úteis

```bash
# Desenvolvimento local
hugo server -D

# Build para produção
hugo --gc --minify

# Atualizar tema
git submodule update --remote --merge

# Lint markdown
npx markdownlint-cli "content/**/*.md"

# Verificar estrutura
tree -I '.git|themes|public' --dirsfirst
```

## Fontes de Conteúdo

- Whitepaper "Prompt Engineering" - Google/Lee Boontra
- Curso "Real World Prompting" - Anthropic

## URLs

- **Produção**: https://prof-ramos.github.io/engenharia-de-prompt/
- **Repositório**: https://github.com/prof-ramos/engenharia-de-prompt
