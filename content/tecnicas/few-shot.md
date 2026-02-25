---
title: "Few-shot"
weight: 2
description: "Com exemplos para guiar o modelo"
---

# One-shot e Few-shot

Fornece **exemplos** para o modelo imitar o padrão.

- **One-shot** = 1 exemplo
- **Few-shot** = 3-5 exemplos (recomendado)

## Por Que Funciona

Modelos aprendem por padrão. Exemplos mostram:
- O formato esperado
- O estilo de resposta
- Como tratar casos específicos

## Estrutura

```
[Instrução]

EXEMPLO 1:
Entrada: [exemplo de entrada]
Saída: [exemplo de saída]

EXEMPLO 2:
Entrada: [exemplo de entrada]
Saída: [exemplo de saída]

Agora faça:
Entrada: [entrada real]
Saída:
```

## Quantos Exemplos?

| Cenário | Recomendação |
|---------|--------------|
| Tarefa simples | 1-2 exemplos |
| Tarefa média | 3-5 exemplos |
| Tarefa complexa | 5-8 exemplos |

> 💡 Mais que 5-8 exemplos raramente melhora resultados.

## Dicas Essenciais

### ✅ Misture as Classes

**❌ Desbalanceado:**
```
Positivo: "Ótimo!"
Positivo: "Adorei!"
Positivo: "Excelente!"
Negativo: "Horrível."
```

**✅ Balanceado:**
```
Positivo: "Ótimo!"
Negativo: "Horrível."
Positivo: "Adorei!"
Negativo: "Não recomendo."
```

### ✅ Inclua Casos Extremos

### ✅ Mantenha Consistência

### ✅ Use Exemplos de Qualidade

O modelo copiará padrões dos exemplos — incluindo erros.

---

[Próximo: Prompt de Sistema →](/tecnicas/prompt-sistema/)
