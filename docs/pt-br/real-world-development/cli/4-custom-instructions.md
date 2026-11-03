---
title: "Lição 4 - Orientar o Copilot com instruções personalizadas"
description: "Explore as instruções do repositório, adicione um padrão de documentação e aplique-o ao código de filtragem."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

O contexto é essencial ao trabalhar com IA generativa. Se uma tarefa precisa ser feita de uma maneira específica, disponibilize essas orientações ao Copilot. Os [arquivos de instruções][instruction-files] descrevem não apenas *o que* você quer, mas também *como* o código deve ser estruturado. Agora que você criou a filtragem, explore as instruções usadas pelo Copilot, adicione um padrão de documentação e aplique-o ao código.

Nesta lição, você vai:

- explorar como as instruções do repositório e os arquivos com escopo de caminho chegam ao agente;
- atualizar o arquivo de instruções para que os padrões de código sejam seguidos;
- observar o efeito dos arquivos de instruções no código.

## Cenário

A Tailspin Toys tem diretrizes e requisitos para as práticas de desenvolvimento:

- Comentários devem explicar a intenção e decisões não óbvias, não repetir o código.
- Funções exportadas em `db/` e `src/lib/` devem documentar sua finalidade, parâmetros e valores retornados com TSDoc/JSDoc, incluindo um argumento `db` injetável quando houver.
- Componentes Astro reutilizáveis devem documentar seus contratos `Props`, e os comentários devem continuar atualizados quando o código relacionado mudar.
- As orientações existentes de formatação e lint devem ser preservadas.

Com arquivos de instruções, você fornecerá ao Copilot o contexto necessário para seguir essas práticas.

## Arquivos de instruções

As instruções personalizadas fornecem contexto e preferências para que o Copilot entenda melhor o estilo e os requisitos do projeto. Você pode especificar convenções de código, bibliotecas e comentários desejados, tanto para todo o repositório quanto para tipos específicos de arquivo.

Há dois tipos de arquivos de instruções:

- `.github/copilot-instructions.md`: um arquivo enviado ao Copilot em **todas** as solicitações do repositório. Inclua nele informações gerais relevantes para a maioria das solicitações.
- `.github/instructions/*.instructions.md`: arquivos com orientações para linguagens, tipos de arquivo ou tarefas específicas.

> [!NOTE]
> O suporte a outros formatos de instrução varia conforme o ambiente. Consulte a [referência de suporte a instruções personalizadas][custom-instructions-support] antes de depender de um formato específico.

## Explorar os arquivos de instruções personalizadas deste projeto

O projeto inicial já inclui arquivos de instruções. Explore-os antes de fazer alterações para observar seu efeito:

1. Volte ao Codespace.
2. No editor Codespaces (não no terminal), abra `.github/copilot-instructions.md`.
3. Examine a descrição do projeto e as orientações de código, que se aplicam a todas as interações com o Copilot.
4. Explore a pasta `.github/instructions`. Observe as instruções para arquivos Astro, a camada de dados Drizzle, testes e outros tópicos.
5. Abra `.github/instructions/unit-tests.instructions.md` e observe o campo `applyTo`, que define um glob para determinar os arquivos abrangidos.
6. Abra `.github/instructions/drizzle.instructions.md` e observe os links para outros arquivos de instruções e arquivos do projeto. Isso permite dividir conjuntos grandes em arquivos menores e reutilizáveis e apontar o Copilot para exemplos.

## Atualizar os arquivos de instruções conforme os padrões da equipe

Atualize o arquivo `copilot-instructions.md` para solicitar comentários TSDoc em novos arquivos TypeScript:

1. Em `.github/copilot-instructions.md`, localize a seção **Code formatting guidance**, perto da linha 35.
2. Adicione este item ao final da seção:

   ```markdown
   - All new TypeScript should contain TSDocs comments for documentation purposes.
   ```

O arquivo será salvo automaticamente.

## Aplicar as instruções atualizadas

O Copilot CLI carrega as instruções do repositório no início de uma conversa. Depois de salvar as instruções, feche e retome a conversa de filtragem para que o Copilot receba a orientação atualizada sem perder o contexto do recurso.

1. Se a conversa de filtragem ainda estiver aberta, digite `/exit` para fechá-la. O Copilot CLI salva as conversas automaticamente.
2. Na raiz do repositório e na branch `game-filters-cli`, retome a conversa salva:

   ```bash
   copilot --resume
   ```

   Se solicitado, selecione a conversa de filtragem e confirme que a branch `game-filters-cli` está selecionada.
3. Peça ao Copilot que aplique as instruções atualizadas:

   ```plaintext
   We just updated our instructions and code guidance. Can you please update the code you generated to match that guidance?
   ```

4. Digite `/diff` e revise os arquivos TypeScript alterados. Observe os comentários TSDoc e confirme que explicam o código corretamente.

## Resumo e próximos passos

Você explorou como o Copilot CLI usa as instruções do repositório e aplicou um novo padrão ao recurso. Nesta lição, você:

- explorou as instruções do repositório e os arquivos com escopo de caminho;
- atualizou o arquivo de instruções para definir padrões de código;
- observou o efeito das instruções no código.

Em seguida, [personalize e execute a skill reutilizável `quality-checks`][next-lesson] para executar as verificações de forma consistente.

## Recursos

- [Adicionar instruções personalizadas ao Copilot CLI][instruction-files]
- [Suporte a instruções personalizadas][custom-instructions-support]
- [Práticas recomendadas para criar instruções personalizadas][instructions-best-practices]
- [Awesome Copilot — arquivos de instruções e outros recursos][awesome-copilot]

[instruction-files]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-custom-instructions
[instructions-best-practices]: https://docs.github.com/copilot/concepts/prompting/response-customization#writing-effective-custom-instructions
[awesome-copilot]: https://awesome-copilot.github.com/
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support
[previous-lesson]: ../3-agent-modes/
[next-lesson]: ../5-agent-skills/
