---
title: "Step-back (Recuo)"
weight: 6
description: "Recuo para abstração"
---

# Step-back (Recuo)

Faz uma **pergunta geral primeiro**, depois usa a resposta para a tarefa específica.

## Por Que Funciona

O "recuo" permite que o LLM:
- Ative conhecimento mais amplo
- Considere princípios gerais antes de detalhes
- Reduza viés de informações específicas

## Processo

```
1. Pergunta geral/abstrata → ativa conhecimento amplo
2. Resposta como contexto → guia raciocínio específico
3. Tarefa específica → usa conhecimento ativado
```

## Quando Usar

| ✅ Ideal para | ❌ Evitar quando |
|--------------|------------------|
| Problemas complexos | Tarefas simples |
| Criatividade | Classificação simples |
| Planejamento | Extração de dados |

## Implementação

```
Antes de responder, considere: 
[pergunta geral sobre o tema]

Agora, responda: [pergunta específica]
```

---

[Próximo: Cadeia de Pensamento →](/tecnicas/cot/)
