# 🎯 Engenharia de Prompt - Guia Completo

> **Licença:** Educacional | **Idioma:** Português (Brasil)

Documentação completa sobre engenharia de prompt para LLMs, baseada no whitepaper do Google/Gemini e no curso "Real World Prompting" da Anthropic.

## 🌐 Site

**https://prof-ramos.github.io/engenharia-de-prompt/**

## 📚 Estrutura

```
engenharia-de-prompt/
├── content/                    # Conteúdo do site Hugo
│   ├── fundamentos/            # Introdução, LLMs, configurações
│   ├── tecnicas/               # 10 técnicas de prompting
│   ├── aplicacoes/             # Código, engenharia automática
│   ├── mundo-real/             # Casos práticos (Anthropic)
│   └── referencia/             # Melhores práticas, templates
├── themes/PaperMod/            # Tema Hugo (submodule)
├── .github/workflows/          # CI/CD
├── hugo.toml                   # Configuração Hugo
├── ARCHITECTURE.md             # Documentação de arquitetura
└── docs/                       # Documentação adicional
```

## 🚀 Desenvolvimento Local

```bash
# Clonar com submodules
git clone --recursive https://github.com/prof-ramos/engenharia-de-prompt

# Servidor local
hugo server -D

# Build para produção
hugo --gc --minify
```

## 📖 Fontes

- Whitepaper **"Prompt Engineering"** de Lee Boontra, Google, Fevereiro 2025
- Curso **"Real World Prompting"** da Anthropic (traduzido e adaptado)

## 📄 Licença

Documentação para fins educacionais.
