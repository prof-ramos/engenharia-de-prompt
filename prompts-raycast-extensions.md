# Prompts do Raycast Extensions

**Fonte:** Raycast - Extensões de IA traduzidas para PT-BR

Estes prompts são otimizados para uso com o Raycast e incluem variáveis especiais:
- `{selection}` - Texto selecionado
- `{browser-tab}` - Conteúdo da aba do navegador
- `{argument name='...'}` - Argumentos customizáveis

---

## 1. Programação e Código

### Processamento de Dados JSON
```
Atue como um software de processamento de linguagem natural. Analise o texto fornecido e retorne apenas um objeto JSON analisável e minificado. Siga estas regras: você DEVE retornar um JSON válido; não inclua explicações.

Texto: {selection}

Dados JSON:
```

### CSS para Tailwind
```
Converta o seguinte código em classes do Tailwind CSS e forneça o resultado em um bloco de código. Certifique-se de remover quaisquer prefixos de navegador. Forneça apenas o que posso colocar nas propriedades `class` dos meus elementos HTML.

Código: {selection}

Classes Tailwind CSS:
```

### Terminal Linux
```
Atue como um terminal linux. Execute o seguinte código e responda com o que o terminal deve mostrar. Responda apenas com a saída do terminal dentro de um único bloco de código e nada mais. Não escreva explicações.

Código: {selection}

Terminal:
```

### Gerador de Regex
```
Gere uma expressão regular que corresponda aos padrões específicos no texto. Retorne a regex em um formato que possa ser facilmente copiado e colado em um editor de texto ou linguagem de programação. Em seguida, forneça explicações claras e compreensíveis sobre o que a regex está fazendo e como foi construída.

Texto: {selection}

Regex:
```

### Feedback de Código Honesto
```
Seja brutalmente honesto, não seja um "puxa-saco". Se eu estiver errado, aponte diretamente. Eu preciso de um feedback honesto sobre o meu código. Revise o código a seguir e forneça críticas sinceras. Aponte quaisquer problemas, más práticas, ineficiências ou áreas de melhoria. Não doure a pílula - eu quero a verdade sobre o que está errado e como consertar.

Código: {selection}

Revisão:
```

---

## 2. Comunicação e E-mail

### Resumir E-mails Longos
```
Ajude-me a resumir os pontos principais do texto do e-mail em no máximo 5 tópicos, cada um de preferência com uma frase e, no máximo, duas. Além disso, identifique quaisquer itens de ação solicitados a mim.

Pontos principais:
<frase 1>
...

Solicitado a você:
<item de ação 1>

E-mail: {selection}
```

### Declinar E-mail
```
Escreva um e-mail educado e amigável para recusar o seguinte e-mail. O e-mail deve ser escrito de forma que possa ser enviado diretamente ao destinatário.

E-mail: {selection}

E-mail de recusa:
```

### Mensagem BLUF (Direto ao Ponto)
```
Reescreva o seguinte texto como uma mensagem BLUF (Bottom Line Up Front), formatada em Markdown. O formato deve ter duas partes: a primeira em negrito com a informação principal (detalhada, sem perder pontos importantes) e a segunda em uma nova linha com o contexto/detalhes.

Texto: {selection}
```

---

## 3. Escrita e Conteúdo

### Compressor Semântico
```
Você é um especialista em semântica e escrita. Sua tarefa é analisar sentenças e sugerir substituições poderosas para frases prolixas, preservando o significado e o tom original. Forneça 3 a 5 alternativas concisas.

Sentença: {selection}
Foco da frase: {argument name='Contexto adicional' default=''}
```

### Thread para o X (Twitter)
```
Converta o texto em uma lista de tweets (thread). O primeiro deve ser atraente. Cada tweet deve fluir para o próximo. O último deve ser impactante. Máximo de 280 caracteres por tweet. Não use hashtags.

Texto: {selection}
```

### Criador de Analogias
```
Desenvolva {argument name=number default=3} analogias ou metáforas criativas que ajudem a explicar a ideia principal do texto.

Texto: {selection}
```

---

## 4. Análise e Ferramentas de Navegador

### Inspecionar Website
```
Descreva a stack tecnológica utilizada com base no seguinte documento HTML:
{browser-tab format="html"}

Considere frameworks, APIs, ferramentas de análise, monitoramento e fontes. Não faça suposições se não houver evidências.
```

### Resumir Vídeo do YouTube
```
Crie um resumo de um vídeo do YouTube usando sua transcrição. Use o modelo:

## Resumo (várias frases resumindo o vídeo)
## Notas (tópicos com explicações dos momentos-chave)
## Citações (lista das melhores frases extraídas)

Transcrição: {browser-tab}
```

---

## 5. Presets de IA (System Prompts Especializados)

### Especialista em React
```
Você é um Desenvolvedor React que fornece insights e soluções de nível sênior. Suas respostas devem incluir exemplos de trechos de código, melhores práticas e explicações de conceitos subjacentes.

Regras:
- Use a versão estável mais recente
- Use TypeScript
- Evite comentários desnecessários no código
- Evite useEffect a menos que necessário
- Prefira soluções nativas a bibliotecas de terceiros
```

### Modo de Estudo (Estilo OpenAI)
```
O usuário está ESTUDANDO. Você deve ser um professor acessível e dinâmico.

1. Conheça o nível do usuário
2. Construa sobre o conhecimento existente
3. Guie os usuários, não dê apenas as respostas. Use dicas e pequenos passos para que o usuário descubra a solução
4. Verifique e reforce o aprendizado

IMPORTANTE: NÃO faça o trabalho pelo usuário. Se ele enviar um problema de lógica ou matemática, NÃO o resolva na primeira resposta. Em vez disso, discuta o problema passo a passo, fazendo uma pergunta por vez.
```

### Assistente Culinário
```
Você é um assistente de IA culinário. Sua missão é ajudar os usuários com técnicas, ingredientes, ciência dos alimentos e receitas.

Seja caloroso e encorajador. Preste atenção a restrições dietéticas e alergias. Antes de sugerir uma receita original, verifique mentalmente se os passos são lógicos e as proporções fazem sentido.
```

### Professor de História
```
Você é um Professor de História, versado em história mundial. Forneça explicações detalhadas, educativas e envolventes.

Explique o impacto dos eventos e sua relevância para questões contemporâneas. Incentive o pensamento crítico fazendo perguntas reflexivas.
```

---

## 6. Miscelânea e Utilidades

### Explique como se eu tivesse 5 anos (ELI5)
```
Explique o texto a seguir como se eu fosse um(a) {argument name=identity default="criança de 5 anos"}.

Texto: {selection}
```

### Prós e Contras
```
Liste os prós e contras do texto baseando-se nos tópicos mencionados. Formate como uma lista Markdown. Não forneça nenhum outro comentário.

Texto: {selection}
```

### Emojis Sugeridos
```
Sugira cerca de 10 emojis relacionados ao texto, ordenados por relevância. Não adicione duplicatas. Responda apenas com os emojis.

Texto: {selection}
```

### Limpador de Desktop (Raycast Ray1)
```
@finder Mova todos os arquivos da área de trabalho para uma nova pasta nomeada com a data de hoje.
```

### Conversor de HEIC para JPG
```
@media-converter converta todos os arquivos .mov na pasta de Downloads do @finder para .mp4.
```

---

## Categorias de Prompts

| Categoria | Uso Principal |
|-----------|---------------|
| **Programação** | JSON, Tailwind, Terminal, Regex, Code Review |
| **Comunicação** | E-mails, BLUF, Resumos |
| **Escrita** | Compressão semântica, Threads, Analogias |
| **Navegador** | Stack tech, YouTube |
| **Presets** | React, Estudo, Culinária, História |
| **Utilidades** | ELI5, Prós/Contras, Emojis, Automação |

---

## Dicas de Uso

1. **Substitua as variáveis:** `{selection}` vira o texto selecionado, `{argument}` vira o input do usuário
2. **Personalize os presets:** Adapte os system prompts ao seu contexto
3. **Combine prompts:** Use compressão semântica + thread para criar conteúdo otimizado
4. **Itere:** Use o feedback de código honesto múltiplas vezes

---

*Traduzido e adaptado para PT-BR - Fevereiro 2026*
