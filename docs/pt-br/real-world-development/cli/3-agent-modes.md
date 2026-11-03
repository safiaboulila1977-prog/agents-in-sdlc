---
title: "Lição 3 - Modos de agente: Plan e Autopilot"
description: "Use Plan para definir uma abordagem, Autopilot para criar a filtragem a partir de uma issue e Interactive para revisar o resultado."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Você começou adicionando um pequeno recurso ao projeto. Alterações maiores exigem um processo mais robusto. O GitHub Copilot CLI pode seguir o fluxo de trabalho da organização para ajudar a criar o que é necessário da maneira adequada. Nesta lição, você seguirá um processo comum de desenvolvimento com agentes: partir de uma issue, definir os requisitos, validar o código e o comportamento e, por fim, fazer merge.

> [!NOTE]
> Você usará a mesma conversa e a mesma branch durante o fluxo de trabalho deste recurso. Normalmente, haveria branches ou PRs diferentes para cada tipo de arquivo, mas aqui usaremos um atalho para manter o foco nos conceitos principais.

Nesta lição, você vai:

- iniciar uma conversa do Copilot a partir de uma issue do GitHub;
- definir requisitos no modo Plan;
- implementar o recurso no modo Autopilot;
- revisar o código;
- validar manualmente o recurso em um navegador encaminhado.

Ao continuar o trabalho, você atualizará as instruções do repositório, personalizará a skill `quality-checks`, adicionará validação MCP, criará um agente de QA e abrirá o PR do recurso.

## Cenário

O catálogo da Tailspin Toys está crescendo, e os visitantes precisam filtrar os jogos por categoria e editora. A issue do backlog descreve o recurso, mas detalhes como combinar categorias precisam ser definidos antes de programar. Use o modo Plan para decidir esses detalhes e autorize uma implementação com escopo definido pelo Autopilot.

## Contexto

Adicionar agentes de programação de IA ao fluxo de desenvolvimento não muda seus fundamentos. A maioria das pessoas desenvolvedoras segue um processo semelhante a este:

1. Começar com uma issue que descreve o trabalho.
2. Planejar o que será criado.
3. Criar e revisar o código.
4. Executar testes para validá-lo.
5. Validar manualmente a nova funcionalidade.
6. Criar um pull request (PR).
7. Depois da revisão e da aprovação da integração contínua, fazer o merge.

> [!NOTE]
> Os detalhes variam de acordo com a equipe e a organização, mas o fluxo normalmente é uma variação dessas etapas.

Seguir esse processo ajuda a confirmar que o código gerado por IA atende aos requisitos e passa pelas mesmas revisões do código escrito manualmente.

## Modos de conversa

O **modo de conversa** controla o nível de autonomia do agente. Pressione <kbd>Shift</kbd>+<kbd>Tab</kbd> para alternar:

- **Interactive**: você e o agente trabalham em conjunto. O agente sugere alterações e aguarda sua orientação.
- **Plan**: o agente cria primeiro um plano e não pode editar os arquivos do projeto.
- **Autopilot**: o agente trabalha de forma autônoma, escrevendo código, executando testes e iterando até concluir a tarefa.

Comece no modo Plan, revise o plano e depois use o Autopilot para implementá-lo.

## Começar pela issue

Volte ao Codespace e prepare o repositório e o terminal:

1. Volte ao Codespace. Se estiver parado, reinicie-o.
2. Confirme que o PR de avaliação por estrelas foi mesclado.
3. Se o terminal não estiver aberto, pressione <kbd>Control</kbd>+<kbd>`</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux).
4. Atualize `main` e crie uma branch para a filtragem:

   ```bash
   git checkout main
   git pull --ff-only
   git checkout -b game-filters-cli
   ```

5. Inicie o Copilot CLI:

   ```bash
   copilot --yolo
   ```

6. Pressione <kbd>Tab</kbd> duas vezes para abrir a guia **Issues**.
7. Pressione <kbd>A</kbd> para mostrar todas as issues.
8. Use as setas para selecionar a issue **Allow users to filter games by category and publisher**.
9. Pressione <kbd>C</kbd> para adicionar a issue ao prompt e voltar à guia **Session**.

Observe que o prompt começa com `#7` (ou um número semelhante). O caractere `#` adiciona o contexto de uma issue ou de um pull request do GitHub.

## Planejar o recurso de filtragem

Planejar permite definir a abordagem antes de implementar um recurso ou executar uma tarefa. É especialmente útil para trabalhos complexos.

1. Pressione <kbd>Shift</kbd>+<kbd>Tab</kbd> para alternar para Plan. Confirme que o indicador de modo abaixo do prompt mostra **Plan**.
2. Depois da referência à issue, envie este prompt:

   ```plaintext
   Create a plan for implementing this feature.
   ```

O Copilot explorará o projeto e definirá uma abordagem.

3. Se o Copilot fizer perguntas sobre o comportamento da filtragem, responda de acordo com suas preferências.
4. Quando o plano estiver pronto, pressione <kbd>Control</kbd>+<kbd>E</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>E</kbd> (Windows/Linux) para expandi-lo.
5. Percorra e revise o plano.
6. Peça ao Copilot para revisar qualquer parte que não corresponda às suas decisões.

## Aprovar o Autopilot

Com o plano revisado, implemente-o usando o Autopilot:

1. Selecione **Accept plan and build on autopilot (recommended)** ou a opção equivalente na sua versão.
2. Confirme que o indicador abaixo do prompt mostra **Autopilot**.
3. Acompanhe o Copilot executar o plano, gerar código e executar testes.

> [!NOTE]
> A aprovação pode iniciar a implementação imediatamente; revise o plano antes. Se o Copilot informar que faltam dependências ou que há conflito de porta, resolva o problema de configuração antes de considerar as verificações concluídas.

## Revisar e verificar a implementação

Como qualquer código, o código gerado precisa ser revisado antes do merge:

1. Pressione <kbd>Shift</kbd>+<kbd>Tab</kbd> para voltar ao modo Interactive. Confirme que o indicador não mostra **Plan** nem **Autopilot**.
2. Digite `/diff` e examine a implementação e os testes de filtragem.
3. Compare o resultado com a issue e com as decisões de planejamento.
4. Depois da revisão, pressione <kbd>Esc</kbd> para sair da visualização do diff.
5. Revise o resultado das verificações e peça ao Copilot para corrigir eventuais falhas.

## Explorar a nova funcionalidade

Inicie o aplicativo e abra o site pela porta encaminhada do Codespaces:

1. Peça ao Copilot para iniciar o aplicativo:

   ```plaintext
   Start the app so I can try the filtering feature in my browser. Tell me the URL and leave the server running.
   ```

2. Quando o Codespaces informar que a porta `4321` está disponível, selecione **Open in Browser**.
3. Teste os filtros de categoria e editora, inclusive as combinações definidas no plano.
4. Confirme se a redefinição dos filtros e os resultados vazios correspondem à issue e às suas decisões.
5. Volte ao Codespace e peça ao Copilot que pare o servidor de desenvolvimento.

## Resumo e próximos passos

Você usou vários modos de conversa para criar e revisar um recurso. Nesta lição, você:

- iniciou uma conversa do Copilot a partir de uma issue do GitHub;
- definiu requisitos no modo Plan;
- implementou o recurso no modo Autopilot;
- revisou o código;
- validou manualmente a funcionalidade no navegador encaminhado.

Em seguida, aprofunde-se na geração de código e nas práticas documentadas usando [instruções personalizadas][next-lesson].

## Recursos

- [Autopilot no GitHub Copilot CLI][autopilot]
- [Referência de comandos do Copilot CLI][cli-reference]

[autopilot]: https://docs.github.com/copilot/concepts/agents/copilot-cli/autopilot
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[previous-lesson]: ../2-add-star-rating/
[next-lesson]: ../4-custom-instructions/
