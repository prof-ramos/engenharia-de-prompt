---
title: "Prompt Sistema"
weight: 03
---

---

Define o **comportamento global** do modelo. Ideal para instruções que se aplicam a toda a conversa.

## Estrutura

```
[Identidade/Papel]
[Regras de comportamento]
[Formato de saída]
[Restrições]
```

## Exemplo - Assistente Jurídico

```
Você é um assistente especializado em análise de contratos jurídicos.

REGRAS:
- Identifique cláusulas de risco
- Destaque termos ambíguos
- Sugira melhorias de redação
- Use linguagem técnica mas acessível

FORMATO DE SAÍDA:
Para cada ponto identificado:
1. **Cláusula**: [citação]
2. **Risco**: [baixo/médio/alto]
3. **Explicação**: [análise]
4. **Sugestão**: [recomendação]

RESTRIÇÕES:
- Não dê conselhos legais definitivos
- Sempre sugira consultar um advogado
```

## Exemplo - Classificador com JSON

```
Você é um classificador de avaliações de produtos.

REGRAS:
- Classifique como POSITIVO, NEGATIVO ou NEUTRO
- Identifique o aspecto principal mencionado
- Retorne SEMPRE em JSON

FORMATO:
{
  "sentimento": "POSITIVO|NEGATIVO|NEUTRO",
  "aspecto": "qualidade|preço|entrega|atendimento|outro",
  "confianca": 0.0-1.0
}
```

## Benefícios

| Benefício | Descrição |
|-----------|-----------|
| **Consistência** | Mantém comportamento em conversas longas |
| **Reutilização** | Define "regras do jogo" uma vez |
| **Controle** | Limita comportamentos indesejados |
| **Integração** | Fácil de usar em APIs e chatbots |

## Quando Usar

- ✅ Chatbots e assistentes
- ✅ APIs que processam múltiplas requisições
- ✅ Conversas multi-turno
- ✅ Quando precisa de formato consistente

## Diferença de Outros Prompts

| Tipo | Escopo | Exemplo |
|------|--------|---------|
| **Sistema** | Toda a conversa | "Você é um assistente técnico..." |
| **Contextual** | Tarefa específica | "Este texto é sobre finanças..." |
| **Papel** | Identidade | "Aja como um advogado..." |

## Dica: Combine com Outros Prompts

```
[SYSTEM]
Você é um especialista em marketing digital.

[USER - Contextual]
Este texto é para um público de pequenos empreendedores.

[USER - Tarefa]
Crie 5 headlines para um ebook sobre SEO.
```

---

[Próximo: Prompt de Papel →](04-prompt-papel.md)
