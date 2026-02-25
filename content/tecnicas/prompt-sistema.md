---
title: "Prompt de Sistema"
weight: 3
description: "Define comportamento global"
---

# Prompt de Sistema

Define o **comportamento global** do modelo. Ideal para instruções que se aplicam a toda a conversa.

## Estrutura

```
[Identidade/Papel]
[Regras de comportamento]
[Formato de saída]
[Restrições]
```

## Benefícios

| Benefício | Descrição |
|-----------|-----------|
| **Consistência** | Mantém comportamento em conversas longas |
| **Reutilização** | Define "regras do jogo" uma vez |
| **Controle** | Limita comportamentos indesejados |
| **Integração** | Fácil de usar em APIs e chatbots |

## Quando Usar

- ✅ Chatbots e assistentes
- ✅ APIs que processam múltiplas requisições
- ✅ Conversas multi-turno
- ✅ Quando precisa de formato consistente

## Diferença de Outros Prompts

| Tipo | Escopo |
|------|--------|
| **Sistema** | Toda a conversa |
| **Contextual** | Tarefa específica |
| **Papel** | Identidade |

## Dica: Combine com Outros Prompts

```
[SYSTEM]
Você é um especialista em marketing digital.

[USER - Contextual]
Este texto é para um público de pequenos empreendedores.

[USER - Tarefa]
Crie 5 headlines para um ebook sobre SEO.
```

---

[Próximo: Prompt de Papel →](/tecnicas/prompt-papel/)
