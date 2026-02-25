---
title: "Engenharia Automática de Prompts (APE)"
weight: 2
description: "Gerar prompts automaticamente"
---

# Engenharia Automática de Prompts (APE)

Usa o próprio LLM para **gerar e otimizar prompts**.

## Processo

```
1. GERAÇÃO: LLM cria N variantes do prompt
2. AVALIAÇÃO: Testa cada variante com métricas
3. SELEÇÃO: Escolhe a melhor variante
4. REFINAMENTO: Itera sobre a melhor
```

## Exemplo - Gerar Variantes

```
Tarefa: Criar prompts para chatbot de e-commerce.

Prompt base: "Quero uma camisa azul"

Gere 10 variantes de como clientes podem formular esse pedido:
```

**Saída:**
1. "Estou procurando uma camisa na cor azul"
2. "Vocês têm camisas azuis?"
3. "Me mostra as opções de camisa azul"
4. "Quero ver camisas masculinas azuis"
5. ...

## Métricas de Avaliação

| Métrica | Uso |
|---------|-----|
| **BLEU** | Comparação com referência |
| **ROUGE** | Cobertura de termos |
| **Accuracy** | Classificação correta |
| **Human eval** | Qualidade subjetiva |

## Aplicações

- Treinamento de modelos
- Teste de robustez
- Otimização de prompts
- Aumento de diversidade

## Fluxo Completo

```
Prompt Inicial → Gerar Variantes → Avaliar → Selecionar → Refinar → Repetir?
```
