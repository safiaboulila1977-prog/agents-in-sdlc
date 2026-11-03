---
title: "Lição 1 - Instalar o aplicativo GitHub Copilot"
description: "Instale o aplicativo GitHub Copilot, conecte o repositório criado a partir do modelo, conheça o espaço de trabalho e experimente um chat rápido."
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

O **[aplicativo GitHub Copilot][about-copilot-app]** é um aplicativo para desktop voltado ao desenvolvimento orientado por agentes. Ele é baseado no GitHub Copilot CLI e se integra nativamente ao GitHub, para que seus repositórios, branches e pipelines de CI funcionem sem configuração adicional. O aplicativo foi projetado para fluxos de trabalho nos quais você orienta vários agentes em paralelo, cada um em seu próprio espaço de trabalho isolado, em vez de fazer tudo sozinho, além de automatizar tarefas repetitivas. Com o Node.js instalado e sua cópia do projeto pronta, o próximo passo é instalar o aplicativo e conectar esse repositório.

Nesta lição, você vai:

- instalar o aplicativo GitHub Copilot e entrar na sua conta;
- adicionar seu projeto ao aplicativo pelo repositório do GitHub;
- conhecer o espaço de trabalho, incluindo o backlog criado pelo modelo;
- experimentar um chat rápido para saber mais sobre o próprio aplicativo.

## Cenário

Sua equipe está adotando agentes de IA para trabalhar em um backlog crescente. O aplicativo Copilot oferece um único lugar para orientar esse trabalho: selecionar issues, executar agentes, revisar alterações e fazer merge de pull requests. Nesta lição, você instalará e conectará o aplicativo e aprenderá a iniciar uma conversa sobre o projeto.

> [!NOTE]
> É necessário ter um plano elegível do Copilot: Copilot Free, Copilot Student ou um plano pago (Pro, Pro+, Business ou Enterprise). Se você usa o Copilot Business ou o Copilot Enterprise, o administrador precisa manter habilitada a política **GitHub Copilot app**.

## Instalar e configurar o aplicativo GitHub Copilot

O primeiro passo para usar o aplicativo GitHub Copilot é instalá-lo. Há versões para Windows, macOS e Linux. Vamos instalar o aplicativo, autenticar a conta e adicionar o repositório Tailspin Toys.

1. Em um navegador, abra a [página inicial do aplicativo GitHub Copilot][download-app].
2. Baixe o aplicativo para sua plataforma e instale-o seguindo as instruções da página.
3. Abra o aplicativo depois da instalação.
4. Selecione **Sign in to GitHub** e siga as instruções para autenticar-se. Se você usa o GitHub Enterprise Cloud com residência de dados, selecione **Use GitHub Enterprise** e informe seu host `*.ghe.com` quando solicitado. O GitHub Enterprise Server não é compatível.
5. Se o processo inicial oferecer a seleção de repositórios, selecione o repositório Tailspin Toys criado a partir do modelo. Você também pode ignorar essa etapa e adicionar o projeto depois.
6. Selecione um tema quando solicitado e conclua a configuração inicial.
7. Procure seu repositório em **Sessions**, na barra lateral. Se ele já estiver listado, não é necessário adicioná-lo novamente.
8. Se o repositório ainda não estiver conectado, selecione **+** ao lado de **Sessions** para criar uma nova sessão e, em seguida, selecione **Add GitHub repository**. Use o proprietário e o nome do repositório anotados na lição de pré-requisitos.
9. Confirme se o repositório aparece na barra lateral. No layout usado aqui, pastas de repositório, como `tailspin-toys`, ficam agrupadas em **Sessions**, com as sessões individuais abaixo de cada repositório.

## Conhecer o espaço de trabalho

Com o projeto conectado, conheça as áreas da barra lateral:

- **New**: inicie uma nova sessão de chat com o Copilot.
- **Pull requests**: seus pull requests, exibidos pela integração nativa com o GitHub. Procure e filtre PRs, confira o status da CI e revise-os sem sair do aplicativo.
- **Issues**: suas issues, também exibidas pela integração. Procure e filtre issues e inicie uma sessão a partir de uma issue.
- **Automations**: tarefas de agente salvas, executadas conforme uma agenda ou sob demanda. Elas ajudam a gerenciar listas de tarefas, manutenção regular do projeto e outras atividades repetitivas. O resumo do workshop apresenta automações como um próximo passo, não como outro exercício.
- **Customize**: adicione recursos ao aplicativo Copilot por meio de servidores MCP, plugins, skills e outros componentes. Você usará esta área para configurar o MCP do Playwright.
- **Chats**: conversas leves para perguntas e brainstorming que não precisam de uma branch nem de um espaço de trabalho próprio. Esta seção aparece depois que você inicia seu primeiro chat. Se ela não estiver visível, selecione **+** ao lado de **Sessions** para iniciar um chat.
- **Sessions**: agrupa as pastas dos repositórios e as sessões de agente. Selecione um repositório, como `tailspin-toys`, para abrir a visualização dele ou selecione uma sessão abaixo do repositório para voltar à conversa. Cada sessão é executada em um espaço de trabalho isolado, para que você possa executar várias sessões sem conflitos. Você iniciará sua primeira sessão ao adicionar avaliações por estrelas.

Ao longo do workshop, você explorará o espaço de trabalho.

> [!TIP]
> Na dúvida, pergunte ao Copilot. Se não souber como fazer algo ou se algo é possível, pergunte ao Copilot para receber orientações.

### Localizar o backlog criado pelo modelo

Quase todo projeto tem um backlog, e a Tailspin Toys não é diferente. Vamos explorar as issues criadas quando você criou sua cópia a partir do modelo.

1. Em **Sessions**, na barra lateral, selecione a pasta do repositório Tailspin Toys, não uma sessão individual abaixo dela. Em seguida, selecione **Issues** na navegação superior do repositório.
2. Encontre estas issues pelo título, sem presumir seus números:

   - Allow users to filter games by category and publisher
   - Update our repository coding standards

3. Selecione uma issue para ler os detalhes. Cada issue também pode iniciar uma sessão de agente. Você começará pela issue de filtragem depois de concluir uma alteração rápida.

> [!NOTE]
> As listas de **Issues** e **Pull requests** são filtradas automaticamente para exibir somente itens dos repositórios adicionados ao aplicativo Copilot. Para ver itens de outros repositórios, adicione-os ao aplicativo.

## Experimentar um chat rápido

Uma ótima maneira de conhecer o aplicativo é perguntar sobre o *próprio aplicativo*. Um **chat rápido** é ideal para isso. Você pode fazer uma pergunta ou trocar ideias sem criar uma branch nem um worktree; não é necessário iniciar uma sessão.

1. Na barra lateral, selecione **+** ao lado de **Chats** para abrir um novo chat. Se **Chats** ainda não estiver visível, selecione **+** ao lado de **Sessions** para iniciar seu primeiro chat. Depois disso, **Chats** aparecerá.
2. Pergunte ao aplicativo como as sessões funcionam:

   ```plaintext
   How does the GitHub Copilot app use worktrees?
   ```

3. Leia a resposta na visualização da conversa. Cada sessão é executada em seu próprio git worktree isolado, o que permite executar vários agentes em paralelo sem que suas alterações entrem em conflito. Você pode continuar a conversa ou iniciar outro chat a qualquer momento.

## Resumo e próximos passos

Você instalou o aplicativo GitHub Copilot, conectou o projeto e explorou o espaço de trabalho. Você aprendeu a:

- instalar o aplicativo e entrar no GitHub;
- adicionar um projeto pelo repositório do GitHub;
- conhecer o espaço de trabalho e localizar o backlog criado em **Issues**;
- usar um chat rápido para fazer uma pergunta.

Em seguida, [inicie sua primeira sessão de agente][next-lesson] e use-a para exibir uma avaliação por estrelas nos cartões de jogos.

## Recursos

- [Sobre o aplicativo GitHub Copilot][about-copilot-app]
- [Introdução ao aplicativo GitHub Copilot][getting-started]
- [Trabalhar com sessões de agente no aplicativo GitHub Copilot][agent-sessions]

[next-lesson]: ../2-add-star-rating/
[about-copilot-app]: https://docs.github.com/copilot/concepts/agents/github-copilot-app
[getting-started]: https://docs.github.com/copilot/how-tos/github-copilot-app/getting-started
[agent-sessions]: https://docs.github.com/copilot/how-tos/github-copilot-app/agent-sessions
[download-app]: https://gh.io/app
