# 06 - Engenharia Automática de Prompts (APE)

[← Prompting para Código](05-prompting-codigo.md) | [Próximo: Melhores Práticas →](07-melhores-praticas.md)

---

Usa o próprio LLM para **gerar e otimizar prompts**.

## Processo

```
1. GERAÇÃO: LLM cria N variantes do prompt
2. AVALIAÇÃO: Testa cada variante com métricas
3. SELEÇÃO: Escolhe a melhor variante
4. REFINAMENTO: Itera sobre a melhor
```

## Exemplo - Gerar Variantes

```
Tarefa: Criar prompts para um chatbot de e-commerce 
que ajuda clientes a encontrar produtos.

Prompt base: "Quero uma camisa azul"

Gere 10 variantes de como clientes podem formular esse pedido:
```

**Saída:**
1. "Estou procurando uma camisa na cor azul"
2. "Vocês têm camisas azuis?"
3. "Me mostra as opções de camisa azul"
4. "Quero ver camisas masculinas azuis"
5. "Tem camisa azul disponível?"
6. "Buscando camisa azul tamanho M"
7. "Quais camisas azuis vocês têm?"
8. "Camisa azul, por favor"
9. "Estou atrás de uma camisa azul"
10. "Preciso de uma camisa azul"

## Métricas de Avaliação

| Métrica | Uso |
|---------|-----|
| **BLEU** | Comparação com referência |
| **ROUGE** | Cobertura de termos |
| **Accuracy** | Classificação correta |
| **Human eval** | Qualidade subjetiva |

## Aplicações

| Uso | Descrição |
|-----|-----------|
| **Treinamento** | Gerar dados sintéticos |
| **Teste** | Avaliar robustez |
| **Otimização** | Encontrar melhor prompt |
| **Variação** | Aumentar diversidade |

## Fluxo Completo

```
┌─────────────────┐
│  Prompt Inicial │
└────────┬────────┘
         ↓
┌─────────────────┐
│ Gerar Variantes │
└────────┬────────┘
         ↓
┌─────────────────┐
│   Avaliar com   │
│    Métricas     │
└────────┬────────┘
         ↓
┌─────────────────┐
│  Selecionar     │
│  Melhor         │
└────────┬────────┘
         ↓
┌─────────────────┐
│  Refinar e      │
│  Repetir?       │
└─────────────────┘
```

---

[Próximo: Melhores Práticas →](07-melhores-praticas.md)
