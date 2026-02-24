# 📑 Sumário

**Versão:** 2.0 | **Atualização:** Fevereiro 2025  
**Idioma:** Português (Brasil)

---

## Capítulos

### Fundamentos

| Capítulo | Descrição |
|----------|-----------|
| [01 - Introdução](01-introducao.md) | O que é engenharia de prompt e por que importa |
| [02 - Como LLMs Funcionam](02-como-llms-funcionam.md) | Entendendo o funcionamento interno |
| [03 - Configurações de Saída](03-configuracoes.md) | Temperatura, Top-K, Top-P e limites |

### Técnicas de Prompting

| Capítulo | Técnica | Quando Usar |
|----------|---------|-------------|
| [04.01 - Zero-shot](tecnicas/01-zero-shot.md) | Sem exemplos | Tarefas simples |
| [04.02 - Few-shot](tecnicas/02-few-shot.md) | Com exemplos | Formato específico |
| [04.03 - Prompt de Sistema](tecnicas/03-prompt-sistema.md) | Comportamento global | Chatbots, agentes |
| [04.04 - Prompt de Papel](tecnicas/04-prompt-papel.md) | Identidade | Expertise específica |
| [04.05 - Prompt Contextual](tecnicas/05-prompt-contextual.md) | Informações específicas | Personalização |
| [04.06 - Step-back](tecnicas/06-step-back.md) | Recuo abstrato | Problemas complexos |
| [04.07 - Cadeia de Pensamento](tecnicas/07-cot.md) | Raciocínio explícito | Lógica, matemática |
| [04.08 - Auto-consistência](tecnicas/08-auto-consistencia.md) | Votação | Maior precisão |
| [04.09 - Árvore de Pensamentos](tecnicas/09-tot.md) | Exploração ramificada | Otimização |
| [04.10 - ReAct](tecnicas/10-react.md) | Raciocinar + Agir | Ferramentas externas |

### Aplicações

| Capítulo | Descrição |
|----------|-----------|
| [05 - Prompting para Código](05-prompting-codigo.md) | Escrever, explicar, traduzir, debugar |
| [06 - Engenharia Automática](06-ape.md) | Gerar prompts automaticamente |

### Prompts no Mundo Real

| Capítulo | Descrição |
|----------|-----------|
| [Introdução](prompts-no-mundo-real/00-introducao.md) | Visão geral do curso prático |
| [01 - Recapitulação](prompts-no-mundo-real/01-recapitulacao.md) | Fundamentos essenciais |
| [02 - Prompt Médico](prompts-no-mundo-real/02-prompt-medico.md) | Exemplo: assistente médico |
| [03 - Processo](prompts-no-mundo-real/03-processo.md) | Framework de engenharia |
| [04 - Resumidor](prompts-no-mundo-real/04-resumidor-chamadas.md) | Exemplo: resumo de chamadas |
| [05 - Bot de Suporte](prompts-no-mundo-real/05-bot-suporte.md) | Exemplo: atendimento ao cliente |

### Referência

| Capítulo | Descrição |
|----------|-----------|
| [07 - Melhores Práticas](07-melhores-praticas.md) | 15 práticas essenciais |
| [08 - Anti-Padrões](08-anti-padroes.md) | O que evitar |
| [09 - Checklist](09-checklist.md) | Validação antes de usar |
| [10 - Templates](10-templates.md) | Prontos para copiar |
| [11 - Troubleshooting](11-troubleshooting.md) | Problemas comuns |
| [12 - Referência Rápida](12-referencia-rapida.md) | Tabelas e resumos |

---

## Navegação Rápida

### Por Tipo de Tarefa

```
Classificação     → Zero-shot, Few-shot
Extração          → Few-shot, JSON
Resumo            → Sistema, Contexto
Raciocínio        → CoT, Step-back
Criatividade      → Papel, Temperatura alta
Código            → Sistema, CoT, Few-shot
Análise           → Papel, CoT, Step-back
Conversação       → Sistema, Papel, Contexto
```

### Por Problema

```
Respostas longas    → 11-troubleshooting.md
Alucinações         → 11-troubleshooting.md
Formato inconsistente → 08-anti-padroes.md
Ignora instruções   → 11-troubleshooting.md
```

---

*Documento baseado no whitepaper "Prompt Engineering" de Lee Boonstra, Google*
