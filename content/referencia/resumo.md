---
title: "Referência Rápida"
weight: 6
description: "Tabelas e resumos"
---

# Referência Rápida

## Técnicas por Tarefa

| Tarefa | Técnicas |
|--------|----------|
| Classificação | Zero-shot, Few-shot |
| Extração | Few-shot, JSON |
| Resumo | Sistema, Contexto |
| Raciocínio | CoT, Step-back |
| Criatividade | Papel, Temperatura alta |
| Código | Sistema, CoT |
| Análise | Papel, CoT |
| Conversação | Sistema, Papel |

---

## Configurações por Tarefa

| Tarefa | Temperatura | Top-P | Top-K |
|--------|-------------|-------|-------|
| Fatos/Código | 0 | 0.9 | 20 |
| Classificação | 0.1 | 0.9 | 20 |
| Resumo | 0.2 | 0.95 | 30 |
| Conversação | 0.5 | 0.95 | 40 |
| Criatividade | 0.8 | 0.99 | 50 |

---

## Frases Mágicas

| Objetivo | Frase |
|----------|-------|
| Ativar CoT | `"Vamos pensar passo a passo."` |
| Evitar alucinação | `"Se não estiver no texto, responda 'Não disponível'."` |
| Garantir formato | `"Retorne APENAS o JSON."` |
| Melhor raciocínio | `"Pense cuidadosamente antes de responder."` |
| Ser conciso | `"Seja conciso. Máximo 100 palavras."` |

---

## Estrutura de Prompt

```
1. CONTEXTO/PAPEL
2. TAREFA
3. FORMATO
4. EXEMPLOS
5. RESTRIÇÕES
6. DADOS
```

---

## Delimitadores

| Tipo | Uso |
|------|-----|
| `---` | Separar seções |
| `"""` | Texto longo |
| ``` ``` | Código |
| `<tag>` | Estrutura XML |

---

## Checklist

```
✅ Clara? Específica? Contexto? Exemplos? Testada?
```
