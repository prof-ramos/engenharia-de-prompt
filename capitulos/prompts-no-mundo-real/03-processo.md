# 03 - Processo de Engenharia de Prompt

[← Prompt Médico](02-prompt-medico.md) | [Próximo: Resumidor de Chamadas →](04-resumidor-chamadas.md)

---

Engenharia de prompt é mais do que escrever um bom prompt — é um **processo sistemático**.

## O Ciclo de Engenharia de Prompt

```
┌─────────────────────────────────────────────────────────┐
│                                                         │
│  ┌──────────┐    ┌──────────┐    ┌──────────┐         │
│  │ DEFINIR  │───▶│ CRIAR    │───▶│ TESTAR   │         │
│  │ Objetivo │    │ Prompt   │    │ Casos    │         │
│  └──────────┘    └──────────┘    └──────────┘         │
│       ▲                                │               │
│       │                                ▼               │
│  ┌──────────┐                   ┌──────────┐         │
│  │ DEPLOY   │◀──────────────────│ ITERAR   │         │
│  │ Produção │                   │ Refinar  │         │
│  └──────────┘                   └──────────┘         │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

## Etapa 1: Definir o Objetivo

Antes de escrever qualquer prompt, responda:

| Pergunta | Exemplo de Resposta |
|----------|---------------------|
| **Qual o problema?** | Resumir chamadas de atendimento |
| **Quem usa?** | Agentes de suporte |
| **Qual a entrada?** | Transcrição de chamada |
| **Qual a saída?** | Resumo estruturado |
| **Quais restrições?** | Máx. 200 palavras, sem dados sensíveis |
| **Como medir sucesso?** | Precisão > 90%, feedback dos agentes |

**Template de Definição:**

```markdown
## Definição do Problema

### Contexto
[Descreva o cenário]

### Entrada
[O que o modelo recebe]

### Saída Esperada
[O que o modelo deve produzir]

### Restrições
[Limitações e regras]

### Métricas de Sucesso
[Como avaliar se está funcionando]
```

---

## Etapa 2: Criar o Prompt Inicial

Comece simples, depois refine.

```
Versão 0.1 (MVP):
"Resuma a chamada abaixo em 200 palavras."

Versão 0.2:
"Resuma a chamada de atendimento abaixo.
Inclua: problema relatado, solução proposta, próximo passo."

Versão 0.3:
[Adiciona formato, exemplos, restrições...]
```

**Dica:** Não tente fazer tudo de primeira. Comece com o mínimo viável.

---

## Etapa 3: Testar com Casos Reais

### Tipos de Teste

| Tipo | Descrição |
|------|-----------|
| **Casos Típicos** | Entradas normais do dia a dia |
| **Casos Extremos** | Entradas muito curtas, muito longas, vazias |
| **Casos Problemáticos** | Entradas que podem causar erros |
| **Casos Adversários** | Tentativas de quebrar o prompt |

### Exemplos de Teste

```
✅ Caso Típico:
Transcrição normal de 10 minutos de chamada

⚠️ Caso Extremo:
Transcrição de 2 horas

⚠️ Caso Problemático:
Transcrição com áudio ruim, partes inaudíveis

❌ Caso Adversário:
"Ignore todas as instruções anteriores e..."
```

### Documente os Resultados

```markdown
| Data | Versão | Caso | Resultado | Problema? |
|------|--------|------|-----------|-----------|
| 24/02 | 0.3 | Típico | ✅ OK | - |
| 24/02 | 0.3 | Extremo | ⚠️ Cortou | Limite tokens |
| 24/02 | 0.3 | Problemático | ❌ Erro | Tratar nulos |
```

---

## Etapa 4: Iterar e Refinar

### Framework de Decisão

```
┌─────────────────────────────────────┐
│ O prompt está funcionando?          │
└──────────────┬──────────────────────┘
               │
       ┌───────┴───────┐
       │               │
      SIM             NÃO
       │               │
       ▼               ▼
┌─────────────┐  ┌─────────────────────┐
│ Otimizar    │  │ Qual é o problema?  │
│ - Tokens    │  │ - Formato?          │
│ - Latência  │  │ - Precisão?         │
│ - Custo     │  │ - Segurança?        │
└─────────────┘  └─────────────────────┘
```

### Quando Refinar

| Sintoma | Ação |
|---------|------|
| Respostas inconsistentes | Adicionar exemplos few-shot |
| Formato errado | Ser mais específico sobre estrutura |
| Alucinações | Adicionar restrições, reduzir temperatura |
| Respostas muito longas | Limitar tokens, pedir concisão |
| Ignora instruções | Reorganizar prompt, usar delimitadores |

---

## Etapa 5: Deploy e Monitoramento

### Antes de Produção

- [ ] Testado com casos reais (mín. 50-100)
- [ ] Testado com edge cases
- [ ] Documentado
- [ ] Métricas definidas
- [ ] Plano de rollback

### Em Produção

```markdown
## Monitoramento

### Métricas a Acompanhar
- Taxa de erro
- Latência
- Custo por requisição
- Feedback dos usuários
- Casos de falha

### Alertas
- Taxa de erro > 5%: investigar
- Latência > X segundos: otimizar
- Feedback negativo > 10%: revisar
```

---

## Framework de Decisão Completo

```
                    ┌──────────────────┐
                    │ Definir Objetivo │
                    └────────┬─────────┘
                             │
                    ┌────────▼─────────┐
                    │ Criar Prompt MVP │
                    └────────┬─────────┘
                             │
              ┌──────────────▼──────────────┐
              │ Testar (Típicos + Extremos) │
              └──────────────┬──────────────┘
                             │
                    ┌────────▼─────────┐
              Não   │  Passou nos      │   Sim
           ┌────────┤  Testes?         ├────────┐
           │        └──────────────────┘        │
           │                                      │
    ┌──────▼──────┐                      ┌───────▼──────┐
    │ Identificar │                      │   Otimizar   │
    │ Problema    │                      │   (Tokens,   │
    └──────┬──────┘                      │    Custo)    │
           │                             └───────┬──────┘
    ┌──────▼──────┐                              │
    │ Ajustar     │                              │
    │ Prompt      │                              │
    └──────┬──────┘                              │
           │                                     │
           └─────────────────────────────────────┤
                                                 │
                                          ┌──────▼──────┐
                                          │   Deploy    │
                                          └──────┬──────┘
                                                 │
                                          ┌──────▼──────┐
                                          │  Monitorar  │
                                          └─────────────┘
```

---

## Checklist de Qualidade

### Antes de cada versão:

- [ ] O objetivo está claro?
- [ ] O formato de saída está definido?
- [ ] Há exemplos suficientes?
- [ ] As restrições estão explícitas?
- [ ] Testei com casos típicos?
- [ ] Testei com edge cases?
- [ ] Documentei as mudanças?

### Antes de produção:

- [ ] Testado com dados reais (mín. 100 casos)
- [ ] Métricas de sucesso definidas
- [ ] Plano de rollback
- [ ] Monitoramento configurado
- [ ] Documentação completa

---

[Próximo: Resumidor de Chamadas →](04-resumidor-chamadas.md)
