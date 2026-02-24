# 🎯 Engenharia de Prompt - Guia Completo

> **Licença:** Educacional | **Idioma:** Português (Brasil)

Documentação completa sobre engenharia de prompt para LLMs, baseada no whitepaper do Google/Gemini e expandida com práticas adicionais.

## 📚 Estrutura

```
capitulos/
├── 00-sumario.md           # Índice geral
├── 01-introducao.md        # O que é engenharia de prompt
├── 02-como-llms-funcionam.md
├── 03-configuracoes.md     # Temperatura, Top-K, Top-P
├── 05-prompting-codigo.md  # Código: escrever, explicar, debugar
├── 06-ape.md               # Engenharia automática
├── 07-melhores-praticas.md # 15 práticas essenciais
├── 08-anti-padroes.md      # O que evitar
├── 09-checklist.md         # Validação
├── 10-templates.md         # Prontos para usar
├── 11-troubleshooting.md   # Problemas comuns
├── 12-referencia-rapida.md # Tabelas e resumos
│
├── prompts-no-mundo-real/  # Casos práticos (Anthropic)
│   ├── 00-introducao.md
│   ├── 01-recapitulacao.md
│   ├── 02-prompt-medico.md
│   ├── 03-processo.md
│   ├── 04-resumidor-chamadas.md
│   └── 05-bot-suporte.md
│
└── tecnicas/               # 10 técnicas de prompting
    ├── 01-zero-shot.md
    ├── 02-few-shot.md
    ├── 03-prompt-sistema.md
    ├── 04-prompt-papel.md
    ├── 05-prompt-contextual.md
    ├── 06-step-back.md
    ├── 07-cot.md           # Cadeia de Pensamento
    ├── 08-auto-consistencia.md
    ├── 09-tot.md           # Árvore de Pensamentos
    └── 10-react.md         # Raciocinar e Agir
```

## 🚀 Uso Rápido

### Configurações por Tarefa

| Cenário | Temperatura | Top-P |
|---------|-------------|-------|
| Código/Fatos | 0 | 0.9 |
| Classificação | 0.1 | 0.9 |
| Conversação | 0.5 | 0.95 |
| Criatividade | 0.8 | 0.99 |

### Frases Mágicas

```
"Vamos pensar passo a passo."     → Ativa CoT
"Responda apenas com o JSON."    → Formato estrito
"Se não souber, diga 'Não disponível'." → Evita alucinação
```

### Navegação Rápida

| Quero... | Ir para |
|----------|---------|
| Entender o básico | [Introdução](capitulos/01-introducao.md) |
| Ajustar temperatura | [Configurações](capitulos/03-configuracoes.md) |
| Aprender técnicas | [Técnicas](capitulos/tecnicas/) |
| Ver casos práticos | [Prompts no Mundo Real](capitulos/prompts-no-mundo-real/) |
| Copiar templates | [Templates](capitulos/10-templates.md) |
| Resolver problemas | [Troubleshooting](capitulos/11-troubleshooting.md) |
| Consulta rápida | [Referência](capitulos/12-referencia-rapida.md) |

## 📖 Fontes

- Whitepaper **"Prompt Engineering"** de Lee Boontra, Google, Fevereiro 2025
- Curso **"Real World Prompting"** da Anthropic (traduzido e adaptado)

## 📄 Licença

Documentação para fins educacionais.
