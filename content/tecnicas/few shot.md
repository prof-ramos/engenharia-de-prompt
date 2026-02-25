---
title: "Few Shot"
weight: 02
---

---

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

EXEMPLO 3:
Entrada: [exemplo de entrada]
Saída: [exemplo de saída]

Agora faça:
Entrada: [entrada real]
Saída:
```

## Exemplo - Extração de Entidades

```
Extraia nomes de pessoas e locais do texto.

EXEMPLO 1:
Texto: "Maria foi a Paris visitar o Louvre."
Saída: {"pessoas": ["Maria"], "locais": ["Paris", "Louvre"]}

EXEMPLO 2:
Texto: "João e Ana se encontraram no café central de São Paulo."
Saída: {"pessoas": ["João", "Ana"], "locais": ["São Paulo", "café central"]}

Texto: "Carlos viajou de Brasília para Rio de Janeiro com sua esposa."
Saída:
```

**Saída:**
```json
{"pessoas": ["Carlos"], "locais": ["Brasília", "Rio de Janeiro"]}
```

## Quantos Exemplos?

| Cenário | Recomendação |
|---------|--------------|
| Tarefa simples | 1-2 exemplos |
| Tarefa média | 3-5 exemplos |
| Tarefa complexa | 5-8 exemplos |
| Limite de tokens apertado | 1-2 exemplos |

> 💡 Mais que 5-8 exemplos raramente melhora resultados, apenas consome tokens.

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

```
EXEMPLO (caso normal):
Texto: "O produto é bom."
Sentimento: POSITIVO

EXEMPLO (caso extremo - vazio):
Texto: ""
Sentimento: INDEFINIDO

EXEMPLO (caso extremo - ambíguo):
Texto: "Interessante..."
Sentimento: NEUTRO
```

### ✅ Mantenha Consistência

**❌ Inconsistente:**
```
EXEMPLO 1: Saída = "Positivo"
EXEMPLO 2: A resposta é: Negativo
EXEMPLO 3: POSITIVO
```

**✅ Consistente:**
```
EXEMPLO 1: "Positivo"
EXEMPLO 2: "Negativo"
EXEMPLO 3: "Positivo"
```

### ✅ Use Exemplos de Qualidade

O modelo copiará padrões dos exemplos — incluindo erros.

---

[Próximo: Prompt de Sistema →](03-prompt-sistema.md)
