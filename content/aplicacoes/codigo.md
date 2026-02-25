---
title: "Prompting para Código"
weight: 1
description: "Escrever, explicar, traduzir e debugar código"
---

# Prompting para Código

## Escrever Código

```
Escreva uma função em {linguagem} que {descrição clara}.

Requisitos:
- {Requisito 1}
- {Requisito 2}
- Incluir docstring
- Type hints
- Tratamento de erros
```

## Explicar Código

```
Explique o código abaixo para um desenvolvedor {nível}:

[CÓDIGO AQUI]

Cubra:
1. O que o código faz (visão geral)
2. Como funciona (passo a passo)
3. Conceitos importantes
4. Possíveis melhorias
```

## Traduzir Código

```
Traduza este código de {linguagem A} para {linguagem B}:

[CÓDIGO ORIGINAL]

Mantenha:
- A mesma lógica
- Boas práticas da linguagem destino
- Comentários relevantes
```

## Debugar Código

```
O código abaixo apresenta erro:

[ERRO/STACK TRACE]

Código:
[CÓDIGO COM BUG]

Por favor:
1. Identifique a causa
2. Explique por que acontece
3. Forneça código corrigido
4. Sugira evitar erros similares
```

## Revisar Código

```
Revise o código abaixo como engenheiro sênior:

[CÓDIGO]

Avalie:
- Legibilidade
- Performance
- Segurança
- Manutenibilidade
- Padrões e boas práticas

Para cada ponto: nota (1-10) + sugestão
```

## Configurações por Tarefa

| Tarefa | Temperatura |
|--------|-------------|
| Escrever código | 0 |
| Explicar | 0.3 |
| Debugar | 0 |
| Revisar | 0.2 |
