# 11 - Troubleshooting

[← Templates](10-templates.md) | [Próximo: Referência Rápida →](12-referencia-rapida.md)

---

Problemas comuns e como resolver.

---

## Problema: Respostas muito longas

### Sintomas
- Modelo ignora pedidos de brevidade
- Texto excessivamente verboso

### Soluções

1. **Seja explícito sobre o limite**
```
Responda em EXATAMENTE 50 palavras. Não ultrapasse.
```

2. **Use formato estruturado**
```
Responda em 3 bullet points de no máximo 15 palavras cada.
```

3. **Reduza max_tokens**
```
max_tokens = 100
```

4. **Adicione consequência**
```
Se ultrapassar 100 palavras, a resposta será rejeitada.
```

---

## Problema: Respostas muito curtas

### Sintomas
- Respostas incompletas
- Falta de detalhes

### Soluções

1. **Peça explicitamente**
```
Responda em detalhes, com no mínimo 200 palavras.
```

2. **Aumente max_tokens**
```
max_tokens = 1000
```

3. **Use CoT**
```
Explique seu raciocínio passo a passo antes de responder.
```

---

## Problema: Formato inconsistente

### Sintomas
- JSON malformado
- Estrutura varia entre execuções

### Soluções

1. **Use few-shot com exemplos perfeitos**
```
EXEMPLO:
Input: "texto"
Output: {"campo": "valor"}
```

2. **Seja explícito sobre o formato**
```
Retorne APENAS JSON válido, sem markdown, sem explicações.
```

3. **Use temperatura baixa**
```
temperature = 0
```

4. **Adicione validação no prompt**
```
Antes de responder, verifique se o JSON é válido.
```

---

## Problema: Alucinações

### Sintomas
- Informações inventadas
- Fatos incorretos apresentados como verdade

### Soluções

1. **Limite ao texto fornecido**
```
Responda APENAS com informações explicitamente presentes no texto.
Se a informação não estiver no texto, responda "NÃO DISPONÍVEL".
```

2. **Peça citações**
```
Para cada afirmação, cite a frase exata do texto que a embasa.
```

3. **Reduza temperatura**
```
temperature = 0 - 0.2
```

4. **Peça para admitir ignorância**
```
Se não tiver certeza, diga "Não tenho informação suficiente".
```

---

## Problema: Loop de repetição

### Sintomas
- Modelo repete a mesma palavra/frase
- Texto entra em loop infinito

### Soluções

1. **Ajuste temperatura**
```
Evite extremos (0 ou >1). Use 0.3-0.7.
```

2. **Reduza top-K**
```
top_k = 20-40
```

3. **Limite max_tokens**
```
max_tokens = valor razoável para a tarefa
```

4. **Reformule o prompt**
```
Adicione instrução explícita para variar o texto.
```

---

## Problema: Ignora instruções

### Sintomas
- Modelo não segue formato solicitado
- Instruções são parcialmente seguidas

### Soluções

1. **Coloque instruções no início**
```
IMPORTANTE: [instrução crítica]

[resto do prompt]
```

2. **Use prompt de sistema**
```
System: Você SEMPRE responde em JSON.
User: [pergunta]
```

3. **Repita a instrução**
```
No início: Responda em JSON.
No final: Lembre-se: responda APENAS em JSON.
```

4. **Use delimitadores**
```
INSTRUÇÃO:
---
[instrução]
---

CONTEÚDO:
---
[conteúdo]
---
```

---

## Resumo

| Problema | Causa Provável | Solução Principal |
|----------|----------------|-------------------|
| Respostas longas | Sem limite explícito | Defina max_tokens e peça no prompt |
| Respostas curtas | max_tokens baixo | Aumente limite, peça detalhes |
| Formato inconsistente | Temperatura alta | Use temp=0, few-shot |
| Alucinações | Modelo "criativo" | Limite ao texto, temp baixa |
| Loop de repetição | Temperatura extrema | Ajuste para 0.3-0.7 |
| Ignora instruções | Instruções bury | Coloque no início, sistema prompt |

---

[Próximo: Referência Rápida →](12-referencia-rapida.md)
