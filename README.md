# 🎯 Engenharia de Prompt - Guia Completo

[![License](https://img.shields.io/badge/license-Educational-blue.svg)](LICENSE)
[![Language](https://img.shields.io/badge/language-Portugu%C3%AAs-green.svg)]()

Documentação completa sobre engenharia de prompt para LLMs, baseada no whitepaper do Google/Gemini e expandida com práticas adicionais.

## 📚 Conteúdo

### Fundamentos
- Como LLMs funcionam
- Configurações de saída (Temperatura, Top-K, Top-P)
- Guia rápido de configurações por tipo de tarefa

### Técnicas de Prompting
1. **Zero-shot** - Prompts simples sem exemplos
2. **Few-shot** - Aprendizado com exemplos
3. **Prompt de Sistema** - Comportamento global
4. **Prompt de Papel (Role)** - Identidade especializada
5. **Prompt Contextual** - Informações específicas
6. **Step-back** - Raciocínio por abstração
7. **Cadeia de Pensamento (CoT)** - Raciocínio explícito
8. **Auto-consistência** - Votação majoritária
9. **Árvore de Pensamentos (ToT)** - Exploração ramificada
10. **ReAct** - Raciocínio + ferramentas externas

### Recursos Adicionais
- ✅ Prompting para código (escrever, explicar, traduzir, debugar)
- ✅ Engenharia Automática de Prompts (APE)
- ✅ 15 melhores práticas detalhadas
- ⚠️ Anti-padrões e como evitá-los
- ✅ Checklist de revisão de prompts
- 📋 Templates prontos para usar
- 🔧 Troubleshooting comum
- 📖 Referência rápida

## 📂 Arquivos

| Arquivo | Descrição |
|---------|-----------|
| [`engenharia-de-prompt.md`](engenharia-de-prompt.md) | Documentação completa (~28KB) |

## 🚀 Uso Rápido

### Configurações Recomendadas

| Cenário | Temperatura | Top-P |
|---------|-------------|-------|
| Código/Fatos | 0 | 0.9 |
| Classificação | 0.1 | 0.9 |
| Conversação | 0.5 | 0.95 |
| Criatividade | 0.8 | 0.99 |

### Técnicas por Tarefa

| Tarefa | Técnica |
|--------|---------|
| Classificação | Zero-shot / Few-shot |
| Raciocínio | CoT / Step-back |
| Criatividade | Role + Temperatura alta |
| Código | Sistema + CoT |

### Frases Mágicas

```
"Vamos pensar passo a passo."           → Ativa Chain-of-Thought
"Responda apenas com o JSON."           → Formato estrito
"Se não souber, diga 'Não disponível'." → Evita alucinação
```

## 📖 Fonte

Baseado no whitepaper **"Prompt Engineering"** de Lee Boontra, Google, Fevereiro de 2025.

Versão expandida com:
- Mais exemplos práticos
- Seção de anti-padrões
- Templates prontos
- Troubleshooting
- Referência rápida

## 📄 Licença

Documentação para fins educacionais.
