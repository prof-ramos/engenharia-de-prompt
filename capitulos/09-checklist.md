# 09 - Checklist de Revisão

[← Anti-Padrões](08-anti-padroes.md) | [Próximo: Templates →](10-templates.md)

---

Antes de usar um prompt em produção, verifique:

## ✅ Clareza

- [ ] A tarefa está claramente definida?
- [ ] Não há ambiguidades?
- [ ] O formato de saída está especificado?
- [ ] Há exemplos (se necessário)?

## ✅ Contexto

- [ ] Há contexto suficiente?
- [ ] O contexto é relevante (sem ruído)?
- [ ] Informações críticas estão no início?
- [ ] Delimitadores separam seções?

## ✅ Restrições

- [ ] Há limite de tamanho?
- [ ] O formato está definido?
- [ ] Há restrições de tom/estilo?
- [ ] Restrições são realistas?

## ✅ Testes

- [ ] Testei com entradas típicas?
- [ ] Testei com edge cases?
- [ ] Testei múltiplas vezes (consistência)?
- [ ] Testei com diferentes tamanhos de entrada?

## ✅ Técnico

- [ ] A temperatura está apropriada?
- [ ] O limite de tokens está adequado?
- [ ] O modelo escolhido é adequado?
- [ ] Há tratamento de erros?

## ✅ Qualidade

- [ ] Não há instruções conflitantes?
- [ ] Exemplos são consistentes?
- [ ] Classes estão balanceadas?
- [ ] Não assume conhecimento implícito?

## ✅ Custo

- [ ] Tokens de entrada estão otimizados?
- [ ] Prompt é o mais curto possível?
- [ ] Uso de exemplos é justificado?
- [ ] Custo-benefício está claro?

---

## Quick Check

```
✅ Clara? Específica? Contexto? Exemplos? Testada?
```

Se não passou em todos, revise antes de usar em produção.

---

[Próximo: Templates →](10-templates.md)
