# Configuração do Hugo

## Informações Gerais

- **Framework**: Hugo Extended v0.146.0+
- **Tema**: PaperMod (submodule)
- **Idioma**: Português (Brasil)
- **Deploy**: GitHub Pages

## Configurações Principais

### [params] - Configurações do Tema

| Configuração | Valor | Motivo |
|--------------|-------|--------|
| `defaultTheme` | auto | Respeita preferência do sistema do usuário |
| `ShowReadingTime` | true | Ajuda a estimar tempo de leitura |
| `ShowCodeCopyButtons` | true | Facilita copiar exemplos de código |
| `ShowBreadCrumbs` | true | Melhora navegação em conteúdo profundo |
| `ShowShareButtons` | false | Documentação técnica, não precisa compartilhar |
| `ShowRssButtonInSectionTermList` | false | Sem RSS por enquanto |

### [markup] - Renderização

| Configuração | Valor | Motivo |
|--------------|-------|--------|
| `highlight.style` | monokai | Bom contraste para código |
| `highlight.lineNos` | false | Exemplos são curtos, não precisa |
| `tableOfContents.startLevel` | 2 | Ignora h1 (título da página) |
| `tableOfContents.endLevel` | 3 | Até h3, evita sobrecarga |

## Menu Principal

```
Fundamentos → Técnicas → Aplicações → Mundo Real → Referência
```

Ordem lógica de aprendizado: do básico ao avançado.

## URLs

- **Produção**: https://prof-ramos.github.io/engenharia-de-prompt/
- **Local**: http://localhost:1313/engenharia-de-prompt/
