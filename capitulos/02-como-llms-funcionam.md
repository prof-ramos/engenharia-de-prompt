# 02 - Como LLMs Funcionam

[← Voltar ao Sumário](00-sumario.md)

---

LLMs são **mecanismos de previsão de tokens**.

## O Processo

```
1. Recebem texto sequencial como entrada
2. Preveem qual deve ser o próximo token (baseado em treinamento)
3. Adicionam o token previsto ao final do texto
4. Repetem o processo
```

A previsão é baseada na relação entre tokens anteriores e o que o LLM viu durante treinamento.

## O Que Isso Significa na Prática?

| Conceito | Implicação |
|----------|------------|
| **Previsão probabilística** | O modelo não "pensa" — prevê o mais provável |
| **Contexto importa** | Tokens anteriores influenciam os próximos |
| **Treinamento define limites** | O modelo só sabe o que viu no treinamento |
| **Sem memória entre sessões** | Cada conversa começa do zero |

## Implicações para Engenharia de Prompt

### 1. Contexto é Rei
Quanto mais contexto relevante você fornecer, melhor a previsão.

```
❌ "Analise isso"
✅ "Analise o texto abaixo considerando o público-alvo de executivos de TI"
```

### 2. Ordem Importa
Tokens no início têm mais influência.

```
❌ [texto longo] + [instrução]
✅ [instrução] + [texto longo]
```

### 3. Exemplos Guiam o Padrão
O modelo tende a seguir o padrão dos exemplos fornecidos.

```
EXEMPLO:
Entrada: "Olá"
Saída: {"saudacao": "Olá"}

Agora:
Entrada: "Oi"
Saída:
```

### 4. Fim do Contexto é Esquecido
Tokens muito distantes do ponto atual têm menos influência.

```
Solução: Coloque informações críticas perto de onde serão usadas
```

## Próximo Passo

- [Configurações de Saída](03-configuracoes.md) - Controle a previsão
