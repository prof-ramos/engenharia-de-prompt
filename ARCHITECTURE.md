# Arquitetura do Projeto

## Estrutura de Diretórios

```
engenharia-de-prompt/
├── .github/
│   └── workflows/
│       └── hugo.yaml          # CI/CD para GitHub Pages
├── content/                   # Conteúdo do site Hugo (FONTE PRINCIPAL)
│   ├── fundamentos/           # Conceitos básicos
│   ├── tecnicas/              # 10 técnicas de prompting
│   ├── aplicacoes/            # Casos de uso práticos
│   ├── mundo-real/            # Exemplos da Anthropic
│   └── referencia/            # Referência rápida
├── themes/
│   └── PaperMod/              # Tema Hugo (submodule)
├── .gitignore
├── .gitmodules
├── .markdownlint.json         # Configuração de lint
├── hugo.toml                  # Configuração do Hugo
└── README.md
```

## Fluxo de Build

```
content/*.md → Hugo → public/ (HTML) → GitHub Pages
```

## Dependências

| Dependência | Versão | Propósito |
|-------------|--------|-----------|
| Hugo Extended | 0.146.0 | Build do site |
| PaperMod | latest | Tema visual |

## Comandos Úteis

```bash
# Desenvolvimento local
hugo server -D

# Build para produção
hugo --gc --minify

# Atualizar tema
git submodule update --remote --merge

# Lint markdown
npx markdownlint-cli "**/*.md"
```

## Fontes de Conteúdo

- Whitepaper "Prompt Engineering" - Google/Lee Boontra
- Curso "Real World Prompting" - Anthropic
