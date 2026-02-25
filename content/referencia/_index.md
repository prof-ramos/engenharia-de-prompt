---
title: "Referência Rápida"
weight: 50
description: "Tabelas, checklists e resumos"
---

# Referência Rápida

Consulte rapidamente configurações, técnicas e melhores práticas.

## Tópicos

- [Melhores Práticas](/referencia/melhores-praticas/) - 15 práticas essenciais
- [Anti-Padrões](/referencia/anti-padroes/) - O que evitar
- [Checklist](/referencia/checklist/) - Validação de prompts
- [Templates](/referencia/templates/) - Prontos para usar
- [Troubleshooting](/referencia/troubleshooting/) - Problemas comuns
- [Referência Rápida](/referencia/resumo/) - Tabelas e resumos

## Técnicas por Tarefa

| Tarefa | Técnicas |
|--------|----------|
| Classificação | Zero-shot, Few-shot |
| Extração | Few-shot, JSON |
| Resumo | Sistema, Contexto |
| Raciocínio | CoT, Step-back |
| Criatividade | Papel, Temperatura alta |
| Código | Sistema, CoT |
| Análise | Papel, CoT, Step-back |
| Conversação | Sistema, Papel, Contexto |

## Configurações por Tarefa

| Tarefa | Temperatura | Top-P | Top-K |
|--------|-------------|-------|-------|
| Fatos/Código | 0 | 0.9 | 20 |
| Classificação | 0.1 | 0.9 | 20 |
| Resumo | 0.2 | 0.95 | 30 |
| Conversação | 0.5 | 0.95 | 40 |
| Criatividade | 0.8 | 0.99 | 50 |

## Frases Mágicas

| Objetivo | Frase |
|----------|-------|
| Ativar CoT | `"Vamos pensar passo a passo."` |
| Evitar alucinação | `"Se não estiver no texto, responda 'Não disponível'."` |
| Garantir formato | `"Retorne APENAS o JSON, sem texto adicional."` |
| Melhor raciocínio | `"Pense cuidadosamente antes de responder."` |
