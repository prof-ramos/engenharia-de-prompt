---
title: "Zero Shot"
weight: 01
---

---

O prompt mais simples: **sem exemplos**, apenas a instrução.

## Estrutura

```
[Instrução clara]
[Contexto/dados de entrada]
[Formato esperado da saída]
```

## Exemplo - Classificação

```
Classifique a avaliação abaixo como POSITIVO, NEGATIVO ou NEUTRO.

Avaliação: "O produto chegou antes do prazo, mas a qualidade deixou a desejar."

Classificação:
```

**Saída:** `NEUTRO`

## Exemplo - Extração

```
Extraia o nome do produto, preço e categoria do texto abaixo.
Retorne em formato JSON.

Texto: "iPhone 15 Pro Max - A partir de R$ 9.999 em Smartphones"

JSON:
```

**Saída:**
```json
{
  "produto": "iPhone 15 Pro Max",
  "preco": "R$ 9.999",
  "categoria": "Smartphones"
}
```

## Quando Usar

| ✅ Bom para | ❌ Evitar quando |
|------------|------------------|
| Tarefas simples e bem definidas | Tarefas complexas ou ambíguas |
| Modelo já treinado para o tipo de tarefa | Formato de saída muito específico |
| Poucos tokens disponíveis | Modelo menos capaz |

## Dicas

- Seja **específico** sobre o formato de saída
- Inclua **contexto suficiente**
- Defina **restrições claras**
- Use **delimitadores** para separar seções

## Variação: Instrução + Formato

```
Traduza o texto abaixo para inglês.

TEXTO:
---
Olá, como você está?
---

Responda apenas com a tradução, sem comentários adicionais.
```

---

[Próximo: Few-shot →](02-few-shot.md)
