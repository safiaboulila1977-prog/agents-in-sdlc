---
title: "Exercício 5: Iterar no trabalho do GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lição anterior: Gerenciar agentes][previous-lesson] |
|:--|

## Revisar o trabalho

Ao longo deste laboratório, você trabalhou com o GitHub Copilot em tarefas para melhorar a experiência do usuário e adicionar funcionalidades: pediu documentação para o código, um recurso de jogos relacionados para a equipe de design e recursos de acessibilidade com modos de alto contraste e claro. Agora, revise as alterações e, se necessário, dê feedback ao Copilot para aprimorar o trabalho.

### Cenário

Os fundamentos do design de software e do DevOps não mudam com a chegada da IA generativa. Sempre revise o código gerado e siga o processo normal de DevOps. Vamos revisar as sugestões do GitHub Copilot para a documentação, os jogos relacionados e os recursos de acessibilidade antes de habilitar a revisão para o restante da equipe.

## Segurança e agente de nuvem do GitHub Copilot

Como o agente de nuvem executa tarefas de forma assíncrona e sem supervisão, há restrições de segurança:

- O Copilot tem acesso de leitura ao repositório e acesso de gravação **somente** à branch que usará para o código.
- O agente de nuvem é executado no GitHub Actions, em um ambiente separado e temporário.
- Os fluxos de trabalho do GitHub Actions precisam de aprovação humana antes de serem executados.
- [O acesso a recursos externos é limitado por padrão](https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall), incluindo servidores MCP.

## Revisar a documentação gerada

Comece pelo primeiro pull request (PR) criado pelo agente de nuvem: o que adiciona documentação ao código.

> [!NOTE]
> Ao abrir o PR, você talvez veja um aviso informando que o Copilot foi bloqueado por um firewall. Isso é **esperado**, pois o acesso a recursos externos, inclusive servidores MCP, é limitado por padrão. Se quiser, você pode [personalizar ou desabilitar o firewall do agente de nuvem][agent-firewall].

1. Acesse seu repositório no github.com.
2. Selecione **Pull Requests** para abrir a lista de pull requests.
3. Abra o PR intitulado algo como **Add missing documentation**.

> [!NOTE]
> Se o Copilot ainda estiver trabalhando, o pull request terá a marca **[WIP]**. Aguarde até que ele termine; isso pode levar alguns minutos.

4. Quando o PR estiver pronto, selecione a guia **Files changed** e revise as alterações.

    ![Guia Files changed](../../../_images/shared-pr-files-changed.png)

5. Examine o código atualizado, que inclui comentários TSDoc e outra documentação. O conteúdo exato varia. Procure comentários TSDoc, convenções de TypeScript e cabeçalhos de comentários, orientações provenientes dos arquivos de instruções personalizados vistos no início do Exercício 2.
6. Depois da revisão, volte à guia **Conversation** e role a página para baixo.
7. Verifique se há um indicador de fluxos de trabalho aguardando aprovação.
8. Se houver fluxos de trabalho aguardando aprovação, selecione **Approve and run workflows**.

   ![Aprovar e executar fluxos de trabalho](../../../_images/shared-approve-workflows.png)

9. Os fluxos de trabalho deverão entrar na fila de verificações do pull request. As verificações do projeto para o aplicativo Astro deverão passar; isso pode levar alguns minutos.

## Solicitar alterações ao GitHub Copilot

Você também pode mencionar o Copilot em comentários do pull request ou comentários em linha no código. Ele verá o comentário e iniciará outra sessão para tratar das solicitações. Como os resultados não são determinísticos, não há um texto único a usar. Por exemplo, você pode pedir que o Copilot:

- adicione um cabeçalho breve no início de cada arquivo de código;
- adicione comentários TSDoc a arquivos TypeScript e Astro;
- crie um README que descreva a estrutura do aplicativo Astro.

1. Adicione um comentário solicitando uma alteração na documentação gerada e mencione **@copilot**, como faria com qualquer pessoa da equipe. Use uma das ideias acima ou outra solicitação de documentação.
2. Selecione **View Session** para acompanhar o trabalho. O Copilot iniciará uma nova sessão para fazer as atualizações.
3. Selecione **Back to pull request** para voltar ao pull request.

    ![Voltar ao pull request](../../../_images/ex7-back-to-pr.png)

4. Depois que o Copilot terminar, uma nova confirmação deverá aparecer no PR.
5. Selecione **Files changed** para revisar as alterações.

Continue iterando até ficar satisfeito. Depois, marque o PR de rascunho como pronto para revisão e faça o merge.

![Marcar o PR como pronto para revisão](../../../_images/ex7-ready-for-review.png)

## Revisar o recurso de jogos relacionados

Agora, revise o PR criado pelo Copilot para exibir jogos relacionados na página de detalhes de um jogo.

1. Volte ao repositório no GitHub.com.
2. Selecione a guia **Pull Requests**.
3. Abra o PR com um título semelhante a **Show related games on the game details page**.
4. Selecione **Files changed** e revise o código.
5. Depois da revisão, volte à guia **Conversation** e role a página para baixo.
6. Verifique se há fluxos de trabalho aguardando aprovação.
7. Se houver, selecione **Approve and run workflows**.

   ![Aprovar e executar fluxos de trabalho](../../../_images/shared-approve-workflows.png)

8. Confirme se as verificações do projeto para o aplicativo Astro passam.
9. **Opcional:** teste manualmente o recurso no codespace. No terminal, execute os comandos a seguir, substituindo `<branch-name>` pelo nome da branch criada pelo Copilot, por exemplo, `copilot/fix-8`:

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

O Copilot criou o recurso de jogos relacionados. Você pode solicitar atualizações iterativamente por meio de um novo comentário na guia **Conversation**, como ajustar quantos jogos são exibidos ou adicionar cabeçalhos de comentário e comentários TSDoc. Observe que esse trabalho foi atribuído **antes** da atualização das instruções personalizadas.

## Revisar os recursos de acessibilidade

Por fim, revise os recursos de acessibilidade implementados pelo agente personalizado. O PR deve incluir o modo de alto contraste atribuído no Exercício 3 e o modo claro solicitado no painel de agentes do Exercício 4.

1. Volte ao repositório no GitHub.com.
2. Selecione **Pull Requests**.
3. Abra o PR com um título semelhante a **Add high contrast mode to website**.

> [!NOTE]
> Se o Copilot ainda estiver trabalhando, o pull request terá a marca **[WIP]**. Aguarde até que ele termine.

4. Selecione **Files changed** e revise o código.
5. Preste atenção especial a:
   - componentes da interface para alternar entre modos;
   - armazenamento local das preferências;
   - alterações de CSS ou estilo para os modos de alto contraste e claro;
   - atributos de acessibilidade (rótulos ARIA, navegação por teclado etc.);
   - código JavaScript/TypeScript que controla a alternância.

6. Depois da revisão, volte à guia **Conversation** e role a página para baixo.
7. Verifique se há fluxos de trabalho aguardando aprovação.
8. Se houver, selecione **Approve and run workflows**.

   ![Aprovar e executar fluxos de trabalho](../../../_images/shared-approve-workflows.png)

9. Confirme se as verificações do projeto para o aplicativo Astro passam.
10. **Opcional:** teste manualmente os recursos de acessibilidade no codespace, substituindo `<branch-name>` pelo nome da branch criada pelo Copilot:

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

    Inicie a aplicação e teste os controles de alto contraste e modo claro no navegador. Confirme que funcionam e que as preferências persistem após recarregar a página.

O agente personalizado de acessibilidade ajudou a orientar a implementação segundo as práticas recomendadas. Se encontrar problemas ou melhorias, mencione **@copilot** em um comentário para solicitar alterações, como nos outros PRs.

## Exercício opcional: continuar delegando

O agente de nuvem é útil para tarefas reais do backlog que você pode delegar enquanto trabalha em outras atividades. Para praticar, crie algumas issues no repositório e atribua-as ao Copilot. Algumas ideias:

- criar um formulário de interesse de apoiadores na página de detalhes do jogo;
- implementar paginação na página de lista de jogos;
- adicionar validação de entrada e tratamento de erros aos helpers de acesso a dados.

## Resumo

Você concluiu o percurso de agente de nuvem. Nestas lições:

- **Examinou os arquivos de instruções personalizados do repositório** para ver como influenciam o trabalho do agente.
- **Atribuiu issues ao agente de nuvem do Copilot** e acompanhou a configuração, o planejamento e a execução assíncrona.
- **Criou e usou um agente personalizado** para adicionar modos de alto contraste e claro.
- **Usou a página de agentes do Copilot como painel central** para acompanhar e orientar a sessão de acessibilidade.
- **Revisou e iterou nos pull requests**, mencionando `@copilot` para solicitar alterações e aprovando fluxos de trabalho.

## Revisão e próximos passos

Você concluiu o percurso de agente de nuvem. Para continuar explorando, os outros percursos complementam o que aprendeu:

- 🖥️ **[Percurso de VS Code](../../vscode/)** — explore o modo de agente do Copilot Chat e a integração com MCP diretamente no IDE.
- 💻 **[Percurso de CLI](../../cli/)** — entregue duas alterações revisadas no terminal usando Plan e Autopilot, skills de agente, um agente de QA personalizado, MCP do Playwright, Agent Merge e uma ponte opcional `/delegate` para o agente de nuvem.

No seu próprio repositório, experimente estas ideias:

- atribuir ao agente de nuvem uma issue de refatoração ou cobertura de testes;
- criar um agente personalizado para outro domínio;
- configurar `copilot-setup-steps.yml` para outra pilha de tecnologias.

## Recursos

- [GitHub Copilot][github-copilot]
- [Sobre agentes do Copilot][copilot-agents]
- [Atribuir issues do GitHub ao Copilot][assign-issue]
- [Práticas recomendadas para configurar o agente de nuvem][cloud-agent-best-practices]
- [Configurar o firewall do agente de nuvem][agent-firewall]

---

| [← Lição anterior: Gerenciar agentes][previous-lesson] |
|:--|

[github-copilot]: https://github.com/features/copilot
[cloud-agent-overview]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[agent-firewall]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall

[previous-lesson]: ../4-managing-agents/
