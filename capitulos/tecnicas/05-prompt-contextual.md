# 04.05 - Prompt Contextual

[← Prompt de Papel](04-prompt-papel.md) | [Próximo: Step-back →](06-step-back.md)

---

Fornece **informações específicas** relevantes para a tarefa atual.

## Tipos de Contexto

| Tipo | Exemplo |
|------|---------|
| **Público-alvo** | "Este texto é para CEOs de startups" |
| **Restrições** | "Máximo 280 caracteres" |
| **Preferências** | "Prefira bullet points a parágrafos" |
| **Antecedentes** | "O usuário já tentou X e Y" |
| **Tom desejado** | "Tom profissional mas amigável" |
| **Domínio** | "Contexto: aplicativo de saúde" |

## Exemplo Completo

```
CONTEXTO:
- Público: Gerentes de projeto iniciantes
- Objetivo: Explicar metodologias ágeis
- Restrição: Máximo 300 palavras
- Tom: Educativo e encorajador
- Formato: Comparação em tabela

TAREFA:
Compare Scrum e Kanban para iniciantes.
```

## Benefícios

- Respostas mais **relevantes**
- Menos **alucinações**
- Melhor **personalização**
- Maior **controle** sobre a saída

## Quando Usar

| ✅ Use quando | ❌ Evite quando |
|--------------|-----------------|
| Público específico | Tarefa genérica |
| Restrições claras | Contexto não afeta resultado |
| Personalização necessária | Simplicidade é prioritária |

## Exemplos por Situação

### Com Restrições
```
Contexto: Texto para Twitter (máx. 280 caracteres)

Tarefa: Resuma o artigo sobre mudanças climáticas.
```

### Com Antecedentes
```
Contexto: O usuário já tentou reiniciar o computador e 
verificar a conexão de internet, mas o problema persiste.

Tarefa: Sugira próximos passos para diagnóstico.
```

### Com Público
```
Contexto: Explicação para uma criança de 8 anos

Tarefa: O que é gravidade?
```

### Com Domínio
```
Contexto: Sistema bancário brasileiro

Tarefa: Explique o que é PIX.
```

## Diferença de Prompt de Sistema

| Sistema | Contextual |
|---------|------------|
| Aplica-se a toda conversa | Aplica-se à tarefa atual |
| Define comportamento | Fornece informações |
| Ex: "Você é um assistente" | Ex: "Este texto é para médicos" |

---

[Próximo: Step-back →](06-step-back.md)
