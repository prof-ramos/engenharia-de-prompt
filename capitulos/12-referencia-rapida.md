# 11 - Troubleshooting

[← Templates](10-templates.md) | [Próximo: Referência Rápida →](12-referencia-rapida.md)

---

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
✅ Temperatura mais baixa
```

---

## Respostas Muito Curtas

**Causas:**
- max_tokens muito baixo
- Sem solicitação de detalhes

**Soluções:**
```
✅ "Responda em detalhes"
✅ Aumente max_tokens
✅ "Explique seu raciocínio"
✅ Use CoT
```

---

## Formato Inconsistente

**Causas:**
- Sem exemplos
- Formato mal especificado

**Soluções:**
```
✅ Adicione exemplos few-shot
✅ Use delimitadores no formato
✅ "Retorne APENAS o JSON"
✅ Seja mais específico
```

---

## Alucinações

**Causas:**
- Sem restrições
- Temperatura alta
- Modelo inventa

**Soluções:**
```
✅ "Responda apenas com informações do texto"
✅ "Se não souber, diga 'Não disponível'"
✅ Reduza temperatura (0-0.3)
✅ Peça citações/fontes
```

---

## Loop de Repetição

**Causas:**
- Temperatura muito baixa OU muito alta
- Top-K muito baixo

**Soluções:**
```
✅ Ajuste temperatura para 0.3-0.7
✅ Aumente top-K
✅ Limite max_tokens
✅ Reformule o prompt
```

---

## Ignora Instruções

**Causas:**
- Instruções no lugar errado
- Prompt muito longo
- Instruções conflitantes

**Soluções:**
```
✅ Coloque instruções no início
✅ Use prompt de sistema
✅ Seja mais explícito
✅ Use delimitadores
✅ Reduza tamanho do prompt
```

---

## Tabela Resumo

| Problema | Causa Provável | Solução |
|----------|----------------|---------|
| Muito longo | Sem limite | max_tokens + "seja conciso" |
| Muito curto | Limite baixo | Aumentar max_tokens |
| Formato ruim | Sem exemplos | Few-shot |
| Alucinação | Sem restrição | "Apenas do texto" + temp baixa |
| Loop | Temp extrema | Ajustar para 0.3-0.7 |
| Ignora | Posição | Instruções no início |

---

[Próximo: Referência Rápida →](12-referencia-rapida.md)
