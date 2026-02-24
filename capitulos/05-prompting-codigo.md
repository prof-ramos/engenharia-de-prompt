# 05 - Prompting para Código

[← Voltar ao Sumário](00-sumario.md)

---

## Escrever Código

```
Escreva uma função em {linguagem} que {descrição clara}.

REQUISITOS:
- {requisito 1}
- {requisito 2}
- Incluir docstring
- Incluir type hints
- Tratamento de erros

EXEMPLO DE USO:
{exemplo}

CÓDIGO:
```

### Exemplo

```
Escreva uma função Python que renomeie todos os arquivos de uma pasta 
adicionando um prefixo ao nome.

REQUISITOS:
- Aceitar nome da pasta e prefixo como parâmetros
- Validar se a pasta existe
- Tratar erros de permissão
- Retornar lista de arquivos renomeados

CÓDIGO:
```

---

## Explicar Código

```
Explique o código abaixo para um desenvolvedor {nível}:

```{linguagem}
{código}
```

Cubra:
1. O que o código faz (visão geral)
2. Como funciona (passo a passo)
3. Conceitos importantes utilizados
4. Possíveis melhorias
```

---

## Traduzir Código

```
Traduza este código de {linguagem A} para {linguagem B}:

```{linguagem A}
{código original}
```

MANTENHA:
- A mesma lógica
- Boas práticas da linguagem destino
- Comentários relevantes
```

---

## Debugar Código

```
O código abaixo está apresentando o seguinte erro:

```
{erro/stack trace}
```

Código:
```{linguagem}
{código com bug}
```

Por favor:
1. Identifique a causa do erro
2. Explique por que acontece
3. Forneça o código corrigido
4. Sugira como evitar erros similares
```

### Exemplo

```
Erro: NameError: name 'toUpperCase' is not defined

Código:
```python
text = toUpperCase(prefix)
```

Solução: Python usa prefix.upper() em vez de toUpperCase()
```

---

## Revisar Código

```
Revise o código abaixo como um engenheiro sênior:

```{linguagem}
{código}
```

AVALIE (nota 1-10 para cada):
- Legibilidade
- Performance
- Segurança
- Manutenibilidade
- Padrões e boas práticas

Para cada ponto, dê sugestão de melhoria.
```

---

## Dicas Gerais

| Tarefa | Configuração |
|--------|--------------|
| Escrever código | temp=0, max_tokens alto |
| Explicar | temp=0.3 |
| Debugar | temp=0 + incluir erro completo |
| Revisar | temp=0.2 |

---

[Próximo: Engenharia Automática →](06-ape.md)
