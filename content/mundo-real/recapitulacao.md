---
title: "Recapitulação de Prompting"
weight: 1
description: "Revisão das técnicas essenciais"
---

# Recapitulação de Prompting

Antes de mergulhar em exemplos do mundo real, vamos revisar as técnicas essenciais.

## Princípios Fundamentais

### 1. Seja Claro e Direto

```
❌ "Analise isso"
✅ "Analise o texto e identifique os 3 principais argumentos"
```

### 2. Forneça Contexto

```
❌ "Traduza para inglês"
✅ "Traduza para inglês técnico de TI"
```

### 3. Use Exemplos (Few-shot)

```
EXEMPLOS:
"Adorei!" → POSITIVO
"Que porcaria!" → NEGATIVO

FRASE: "Gostei, mas poderia ser melhor"
```

### 4. Especifique o Formato

```
Retorne em JSON:
{
  "sentimento": "POSITIVO|NEGATIVO|NEUTRO",
  "confianca": 0.0-1.0
}
```

### 5. Divida Tarefas Complexas

```
1. Extraia as entidades
2. Classifique cada uma
3. Formate o resultado
```

## Estrutura de um Prompt Robusto

```
1. CONTEXTO / PAPEL
   "Você é um especialista em..."

2. TAREFA
   "Analise o texto e..."

3. FORMATO DE SAÍDA
   "Retorne em JSON com..."

4. EXEMPLOS (opcional)

5. RESTRIÇÕES
   "Não invente informações..."

6. DADOS DE ENTRADA
   "Texto: ..."
```

## Checklist Rápido

- [ ] A tarefa está clara?
- [ ] Há contexto suficiente?
- [ ] O formato está definido?
- [ ] Há exemplos (se necessário)?
- [ ] As restrições estão explícitas?
