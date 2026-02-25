---
title: "Troubleshooting"
weight: 5
description: "Problemas comuns e soluções"
---

# Troubleshooting

## Respostas Muito Longas

**Causas:**
- Sem limite de tokens
- Prompt vago
- Temperatura alta

**Soluções:**
```
✅ "Seja conciso (máx. 100 palavras)"
✅ Reduza max_tokens
✅ Peça bullet points
```

---

## Respostas Muito Curtas

**Soluções:**
```
✅ "Responda em detalhes"
✅ Aumente max_tokens
✅ "Explique seu raciocínio"
```

---

## Formato Inconsistente

**Soluções:**
```
✅ Adicione exemplos few-shot
✅ Use delimitadores no formato
✅ "Retorne APENAS o JSON"
```

---

## Alucinações

**Soluções:**
```
✅ "Responda apenas com informações do texto"
✅ "Se não souber, diga 'Não disponível'"
✅ Reduza temperatura (0-0.3)
✅ Peça citações
```

---

## Loop de Repetição

**Soluções:**
```
✅ Ajuste temperatura para 0.3-0.7
✅ Aumente top-K
✅ Limite max_tokens
```

---

## Ignora Instruções

**Soluções:**
```
✅ Coloque instruções no início
✅ Use prompt de sistema
✅ Seja mais explícito
✅ Use delimitadores
```

---

## Tabela Resumo

| Problema | Causa | Solução |
|----------|-------|---------|
| Muito longo | Sem limite | max_tokens + "seja conciso" |
| Muito curto | Limite baixo | Aumentar max_tokens |
| Formato ruim | Sem exemplos | Few-shot |
| Alucinação | Sem restrição | "Apenas do texto" |
| Loop | Temp extrema | Ajustar para 0.3-0.7 |
| Ignora | Posição | Instruções no início |
