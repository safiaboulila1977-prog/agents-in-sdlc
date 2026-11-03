---
title: "Exercício 2 - Adicionar funcionalidade com o Agent Mode do Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Até mesmo uma alteração simples costuma envolver vários arquivos e tarefas, como executar testes. Uma pessoa desenvolvedora normalmente precisa localizar os arquivos, fazer as alterações, executar os testes, depurar, identificar o que faltou e repetir o processo. O Agent Mode do Copilot pode explorar a estrutura do projeto, atualizar arquivos, executar tarefas e corrigir problemas encontrados.

> [!NOTE]
> Embora os nomes sejam parecidos, o Agent Mode e o agente de nuvem oferecem experiências diferentes. O Agent Mode trabalha no IDE, com ciclos rápidos de feedback e interação. O agente de nuvem trabalha de forma assíncrona, como uma pessoa da equipe, interagindo por meio de issues e pull requests.

Neste exercício, você vai aprender como:

- o Agent Mode explora o projeto, identifica arquivos relevantes e coordena alterações;
- o Agent Mode implementa funcionalidades na interface e na camada de dados;
- revisar alterações e testes gerados pelo Agent Mode antes do merge.

## Cenário

À medida que a lista de jogos cresce, você quer permitir a filtragem por categoria e editora. Você já adicionou um helper de editoras no exercício anterior; agora concluirá as alterações restantes na camada de dados, na interface e nos testes usando o Agent Mode do Copilot.

## Executar o site Tailspin Toys

Antes de fazer alterações, explore o site para conhecer a funcionalidade atual. A aplicação Tailspin Toys é uma plataforma de financiamento coletivo para jogos de tabuleiro com tema de desenvolvimento. Ela lista jogos e exibe seus detalhes.

O site é um único aplicativo Astro, que renderiza páginas como HTML estático durante a compilação. As páginas consultam um banco de dados SQLite local diretamente no frontmatter por meio do Drizzle ORM. Não há uma API de back-end separada nem uma estrutura de interface no lado do cliente. Os helpers reutilizáveis de acesso a dados ficam em `src/lib/`; a interatividade usa um pequeno `<script>` do Astro com APIs padrão do DOM.

### Iniciar o site

O comando `npm run dev` inicia o servidor de desenvolvimento Astro. Para executá-lo no GitHub Codespaces:

1. Volte ao codespace. Você deverá estar em `main` depois do exercício anterior.
2. Abra um terminal com <kbd>Control</kbd>+<kbd>`</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux).
3. Crie uma branch para o trabalho de filtragem:

   ```bash
   git checkout main
   git pull
   git checkout -b filtering-vscode
   ```

4. Inicie o site:

   ```bash
   npm run dev
   ```

   Quando o servidor Astro estiver pronto, você verá um aviso semelhante a este:

   ```bash
   🚀 Tailspin Toys is ready!
      Astro server: http://localhost:4321
      Press Ctrl-C to stop.
   ```

> [!NOTE]
> Se aparecer uma caixa de diálogo perguntando se você quer abrir `http://localhost:4321` em uma janela do navegador, feche-a selecionando **x**.

5. Abra o site mantendo <kbd>Command</kbd> (Mac) ou <kbd>Ctrl</kbd> (Windows/Linux) pressionado e selecionando `http://localhost:4321` no terminal.

> [!NOTE]
> Em um codespace, selecionar o link localhost no terminal redireciona automaticamente para `https://<your-codespace-name>-4321.app.github.dev/`. Esse é um túnel privado para o codespace, que hospeda o servidor Web.

### Explorar o site

Os principais recursos do site são:

- **Home Page**: mostra uma lista de jogos de tabuleiro com títulos, imagens e descrições.
- **Game Details Page**: ao selecionar um jogo, você abre uma página com mais informações, incluindo título, descrição, editora e categoria.

## Explorar o backlog com o Copilot

> [!TIP]
> **Abrir o Copilot Chat**
>
> Antes de começar os exercícios abaixo, volte ao codespace, abra o painel do Copilot Chat e selecione **New Chat** para iniciar uma conversa limpa. O modo e o modelo variam conforme o exercício; cada etapa informa quando isso for relevante.

O site já funciona, mas você vai adicionar novos recursos. O modelo do projeto cria automaticamente um backlog de issues. Peça ao GitHub Copilot para exibi-lo:

1. Na lista de agentes da visualização Chat, selecione **Agent**. Esse agente planeja e implementa alterações em vários arquivos, executa comandos no terminal e usa ferramentas.

   ![Captura de tela do seletor de agente na visualização Chat.](../../../_images/shared-chat-mode-selector.png)

2. Na lista de modelos, selecione **Claude Sonnet 4.5**.

> [!CAUTION]
> A inclusão de um modelo nestas instruções não representa preferência dos autores. O workshop foi criado com o Claude Sonnet 4.5 para que as sugestões fossem relativamente consistentes. Como os LLMs são probabilísticos, as sugestões podem ser diferentes das descritas; isso é normal.

> [!NOTE]
> Devido à natureza probabilística dos LLMs, o Copilot pode usar um comando MCP diferente, mas ainda deverá concluir a tarefa.

3. Envie este prompt:

   ```plaintext
   Please show me the backlog of items from my GitHub repository. Help me prioritize them based on those which will be most useful to the user.
   ```

4. Selecione **Continue** para permitir que o comando liste todas as issues.
5. Revise a lista criada.

Observe como o Copilot também prioriza os itens com base no que considera mais útil para as pessoas usuárias.

## Revisar os arquivos de instruções

Antes de pedir ao agente para gerar código, examine o arquivo de instruções que fornecerá contexto. O arquivo [de interface (UI)](https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md) explica como adicionar funcionalidades ao site.

1. No codespace, abra `.github/instructions/ui.instructions.md`.
2. Observe as orientações gerais para adicionar funcionalidades, incluindo:
   - uma visão geral da arquitetura;
   - princípios para criar componentes, facilitar testes e garantir acessibilidade;
   - links para instruções de tipos de arquivo, incluindo Astro, Tailwind CSS e Drizzle.

> [!TIP]
> Os arquivos de instruções podem referenciar outros arquivos de instruções e arquivos do projeto. Os caminhos são relativos ao arquivo de instruções. Assim, você pode reutilizar orientações, dividir conjuntos complexos em partes menores e fornecer exemplos e modelos.

## Implementar a filtragem

Para concluir a filtragem, serão necessárias várias alterações:

- adicionar ou aprimorar a lógica de filtragem na camada de dados (`src/lib/`);
- adicionar ou atualizar testes do comportamento de filtragem;
- atualizar a página de listagem de jogos com a interface de filtragem.

Os testes também precisam passar antes de você fazer o merge. O Agent Mode pode realizar essas tarefas:

1. Continue na conversa atual ou selecione **New Chat** para iniciar outra.
2. Selecione **Add Context**, **Instructions** e **ui** como arquivo de instruções.

   ![Exemplo de seleção do arquivo de instruções da interface](../../../_images/ex3-select-instructions-file.png)

3. Confirme que **Agent** continua selecionado.

   ![Captura de tela do seletor de agente na visualização Chat.](../../../_images/shared-chat-mode-selector.png)

4. Confirme que o modelo selecionado continua sendo **Claude Sonnet 4.5**.
5. Peça ao Copilot para implementar a funcionalidade com base na issue:

   ```plaintext
   Please update the site to include filtering by publisher and category based on the requirements from the related GitHub issue in the backlog. A publishers helper already exists from the previous exercise, so preserve and refine that work as needed while completing the remaining data-layer, UI, and tests. Ensure all tests are passing before completion. The server is already running, so you do not need to start it up.
   ```

6. Observe o Copilot explorar o projeto e localizar os arquivos relacionados ao recurso, incluindo os helpers da camada de dados, a interface e os testes. Em seguida, ele alterará os arquivos e executará testes.

   ![Copilot explorando os arquivos do projeto](../../../_images/ex3-agent-mode-explores.png)

> [!NOTE]
> O Copilot executará várias tarefas, como explorar o projeto, alterar arquivos e executar testes. Isso pode levar alguns minutos. Durante o trabalho, os botões **Keep** e **Undo** podem aparecer no editor. Quando o Copilot terminar, você poderá aceitar ou desfazer todas as alterações; não é necessário selecionar esses botões enquanto ele ainda estiver trabalhando.

7. Quando solicitado pelo Copilot, selecione **Continue** para executar os testes.

   ![Caixa de diálogo do Copilot Chat pedindo confirmação para executar os testes](../../../_images/ex3-agent-mode-run-tests.png)

8. Pode haver pausas e falhas em alguns testes durante o processo. O Copilot alterna entre gerar código e executar testes até concluir a tarefa sem detectar erros.

   ![Sessão completa do Copilot Agent Mode no Chat](../../../_images/ex3-agent-mode-proposed-changes.png)

9. Examine o código gerado para identificar possíveis problemas.

> [!CAUTION]
> Sempre revise o código gerado pelo Copilot ou por qualquer outra ferramenta de IA.

10. Volte ao navegador com o site em execução e explore o novo recurso.
11. Depois de confirmar que tudo funciona e revisar o código, selecione **Keep** na janela do Copilot Chat.

## Resumo e próximos passos

Você usou o Agent Mode do GitHub Copilot para adicionar recursos ao site Tailspin Toys e aprendeu como:

- o Agent Mode implementa recursos na interface e na camada de dados;
- o Agent Mode explora o projeto, identifica arquivos relevantes e coordena alterações;
- revisar alterações e testes antes do merge.

Agora, [teste o recurso com o servidor MCP do Playwright][next-lesson] e abra um pull request.

### Exercício bônus: implementar paginação

À medida que a lista de jogos cresce, será necessário implementar paginação. Use as habilidades deste exercício e peça ao Copilot para atualizar o site. Considere:

- seguir as práticas recomendadas e usar os arquivos de instruções existentes;
- decidir se as pessoas poderão escolher o tamanho da página ou se ele será fixo;
- fornecer orientações suficientes no prompt para que o Copilot implemente o comportamento desejado;
- iterar com o Copilot, solicitando alterações e fornecendo contexto. Esse é o fluxo normal de trabalho.

## Recursos

- [Copilot ask, edit e agent modes: para que servem e quando usar cada um][choose-mode]
- [Modo de agente no VS Code][vs-code-agent-mode]

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-mcp/
[choose-mode]: https://github.blog/ai-and-ml/github-copilot/copilot-ask-edit-and-agent-modes-what-they-do-and-when-to-use-them/
[vs-code-agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
