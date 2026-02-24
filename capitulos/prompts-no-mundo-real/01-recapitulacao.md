# 01 - Recapitulação de Prompting

[← Introdução](00-introducao.md) | [Próximo: Prompt Médico →](02-prompt-medico.md)

---

Antes de mergulhar em exemplos do mundo real, vamos revisar as técnicas essenciais de prompting.

## Princípios Fundamentais

### 1. Seja Claro e Direto

O modelo faz o que você pede, literalmente. Quanto mais claro, melhor.

```
❌ "Analise isso"
✅ "Analise o texto abaixo e identifique os 3 principais argumentos do autor"
```

### 2. Forneça Contexto

O modelo não tem contexto além do que você fornece.

```
❌ "Traduza para inglês"
✅ "Traduza para inglês técnico de TI, mantendo terminologia específica de cloud computing"
```

### 3. Use Exemplos (Few-shot)

Exemplos mostram o padrão esperado.

```
Analise o sentimento das frases:

EXEMPLOS:
"Adorei o produto!" → POSITIVO
"Que porcaria!" → NEGATIVO
"É ok, nada especial" → NEUTRO

FRASE:
"Gostei, mas poderia ser melhor"
```

### 4. Especifique o Formato de Saída

```
Retorne a resposta em JSON com a estrutura:
{
  "sentimento": "POSITIVO|NEGATIVO|NEUTRO",
  "confianca": 0.0-1.0,
  "argumentos": ["...", "..."]
}
```

### 5. Divida Tarefas Complexas

```
Em vez de um prompt gigante:
1. Primeiro, extraia as entidades
2. Depois, classifique cada uma
3. Por fim, formate o resultado
```

## Estrutura de um Prompt Robusto

```
┌─────────────────────────────────────┐
│ 1. CONTEXTO / PAPEL                 │
│   "Você é um especialista em..."    │
├─────────────────────────────────────┤
│ 2. TAREFA                           │
│   "Analise o texto e..."            │
├─────────────────────────────────────┤
│ 3. FORMATO DE SAÍDA                 │
│   "Retorne em JSON com..."          │
├─────────────────────────────────────┤
│ 4. EXEMPLOS (opcional)              │
│   "Exemplo de entrada/saída..."     │
├─────────────────────────────────────┤
│ 5. RESTRIÇÕES                       │
│   "Não invente informações..."      │
├─────────────────────────────────────┤
│ 6. DADOS DE ENTRADA                 │
│   "Texto: ..."                      │
└─────────────────────────────────────┘
```

## Técnicas Avançadas

### Cadeia de Pensamento (CoT)

```
[Problema complexo]

Vamos pensar passo a passo:
1. Primeiro, ...
2. Então, ...
3. Portanto, ...
```

### Prompt de Sistema

```
SYSTEM: Você é um assistente médico especializado em cardiologia.
Sempre cite fontes e recomende consultar um médico.
Não faça diagnósticos definitivos.
```

### Delimitadores

```
Analise o texto entre aspas triplas:

"""[texto aqui]"""
```

## Checklist Rápido

Antes de enviar um prompt, verifique:

- [ ] A tarefa está clara?
- [ ] Há contexto suficiente?
- [ ] O formato de saída está definido?
- [ ] Há exemplos (se necessário)?
- [ ] As restrições estão explícitas?
- [ ] O prompt está bem estruturado?

---

[Próximo: Prompt Médico →](02-prompt-medico.md)
