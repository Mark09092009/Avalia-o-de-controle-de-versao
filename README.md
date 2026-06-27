# Portfólio do Grupo

## Descrição

Este projeto consiste na criação de um site de portfólio desenvolvido colaborativamente para a disciplina de Controle de Versão com Git e GitHub do IFPI - Campus Paulistana.

O objetivo é aplicar os conceitos de versionamento utilizando Git e GitHub, incluindo branches, commits, pull requests, merge e resolução de conflitos.

## Integrantes

- Marcos Vinicius de Sousa
- Pedro Lucas Gomes de Sousa
- Maria Clara de Souza Medrado
- Elissandra Pereira Rodrigues
- Tayla Maria de Sousa Gomes
- Luis Gustavo Macêdo Nunes

## Estrutura Inicial

- index.html
- integrantes.html
- projetos.html
- contato.html
- css/style.css

## Tecnologias Utilizadas

- HTML5
- CSS3
- Git
- GitHub

## Status do Projeto

Em desenvolvimento...

## Padrão de Commits

Commits semânticos são fundamentais para manter um histórico claro, facilitar a revisão de código e simplificar a geração de changelogs e releases. Mensagens bem escritas ajudam a equipe a entender rapidamente o contexto de cada alteração e a tomar decisões com mais segurança.

O padrão mais adotado é o Conventional Commits, que segue a estrutura:

```bash
git commit -m "tipo(escopo): descrição curta"
```

Exemplos comuns de tipos:

- `feat`: adiciona uma nova funcionalidade
- `fix`: corrige um bug
- `docs`: altera ou adiciona documentação
- `refactor`: reorganiza o código sem mudar comportamento
- `style`: ajustes de formatação, semântica ou estilo visual
- `test`: adiciona ou ajusta testes
- `chore`: tarefas de manutenção, build ou configuração

| Tipo       | Descrição                                  | Exemplo de mensagem                                 |
| ---------- | ------------------------------------------ | --------------------------------------------------- |
| `feat`     | Nova funcionalidade                        | `feat: adicionar formulário de contato`             |
| `fix`      | Correção de bug                            | `fix: corrigir erro de responsividade no menu`      |
| `docs`     | Atualização de documentação                | `docs: atualizar instruções do README`              |
| `refactor` | Melhoria interna sem alterar comportamento | `refactor: simplificar lógica de navegação`         |
| `style`    | Ajustes visuais ou de formatação           | `style: ajustar espaçamento do CSS`                 |
| `test`     | Testes adicionados ou atualizados          | `test: adicionar testes de validação do formulário` |
| `chore`    | Manutenção e configuração                  | `chore: atualizar configuração do GitHub Actions`   |

## Estrutura de Branches e Fluxo de Trabalho (Workflow)

O fluxo de trabalho adotado neste projeto pode ser baseado em um modelo simplificado de GitHub Flow, onde a branch principal é a `main` e as alterações são desenvolvidas em branches temporárias, específicas para cada tarefa.

### Padrão de nomenclatura de branches

Utilize nomes curtos e descritivos:

```bash
feature/nome-da-feature
bugfix/ajuste-banco
hotfix/correcao-urgente
chore/atualizacao-configuracao
```

### Passo a passo do fluxo

1. Atualize a branch principal:

```bash
git checkout main
git pull origin main
```

2. Crie uma nova branch para a tarefa:

```bash
git checkout -b feature/nome-da-feature
```

3. Faça as alterações e acompanhe o status:

```bash
git status
git add .
git commit -m "feat: adicionar nova funcionalidade"
```

4. Envie a branch para o repositório remoto:

```bash
git push -u origin feature/nome-da-feature
```

5. Abra um Pull Request (PR) no GitHub, descrevendo a mudança, o contexto e os testes realizados.

Boas práticas:

- mantenha branches curtas e focadas em uma única tarefa;
- revise o código antes de mesclar;
- evite commits muito grandes;
- sempre mantenha a branch atualizada com `main` antes de abrir o PR.

## Resolução de Conflitos (Merge Conflicts)

Conflitos acontecem quando duas alterações diferentes afetam a mesma parte de um arquivo, especialmente quando duas branches modificam o mesmo trecho de código simultaneamente. Eles são uma parte natural do trabalho colaborativo e devem ser resolvidos com cuidado.

### Como resolver conflitos localmente

#### Usando `git merge`

```bash
git checkout main
git pull origin main
git checkout feature/nome-da-feature
git merge main
```

Se houver conflito, o Git marcará o arquivo com blocos especiais:

```text
<<<<<<< HEAD
// versão atual da branch main
=======
// versão da branch que está sendo mesclada
>>>>>>> feature/nome-da-feature
```

### Como tratar as marcações

1. Abra o arquivo conflitante.
2. Escolha a versão correta da alteração.
3. Remova as marcações `<<<<<<<`, `=======` e `>>>>>>>`.
4. Salve o arquivo e marque como resolvido:

```bash
git add nome-do-arquivo
git commit
```

#### Usando `git rebase`

```bash
git checkout feature/nome-da-feature
git fetch origin
git rebase origin/main
```

Se houver conflito, resolva da mesma forma e siga com:

```bash
git add nome-do-arquivo
git rebase --continue
```

Se quiser cancelar o processo, use:

```bash
git rebase --abort
```

## Guia de Comandos Avançados do Git

### `git cherry-pick`

Usado para aplicar um commit específico de outra branch no contexto atual. É útil quando você quer trazer uma correção sem importar todo o histórico da branch.

```bash
git cherry-pick <hash-do-commit>
```

Exemplo:

```bash
git cherry-pick a1b2c3d
```

### `git stash`

Permite salvar alterações temporariamente sem commitá-las. É útil quando você precisa trocar de branch rapidamente.

```bash
git stash
```

Exemplos:

```bash
git stash save "trabalho em andamento"
git stash list
git stash pop
git stash drop
```

### `git rebase -i`

Rebase interativo permite reorganizar commits, corrigir mensagens ou combinar múltiplos commits em um só. É uma ferramenta poderosa para deixar o histórico mais limpo antes de abrir um PR.

```bash
git rebase -i HEAD~3
```

Exemplos de ações comuns:

- `pick`: manter o commit
- `squash`: combinar com o commit anterior
- `reword`: renomear a mensagem

### `git reset`

Serve para mover o ponteiro do repositório para outro ponto do histórico. O uso depende do risco desejado:

```bash
git reset --soft HEAD~1
```

- `--soft`: move o `HEAD` e mantém as alterações em staging.
- `--mixed` (padrão): move o `HEAD` e desfaz o staging, deixando as alterações no working directory.
- `--hard`: remove as alterações do diretório de trabalho e do índice.

Exemplos:

```bash
git reset --soft HEAD~1
git reset --mixed HEAD~1
git reset --hard HEAD~1
```

Use com cuidado, principalmente com `--hard`, pois apaga alterações locais.

### `git revert`

Cria um novo commit que desfaz as mudanças de um commit anterior, sem reescrever o histórico. É o método mais seguro para commits já compartilhados com a equipe.

```bash
git revert <hash-do-commit>
```

Exemplo:

```bash
git revert a1b2c3d
```

### `git reflog`

O `git reflog` registra movimentos do `HEAD` e pode ser usado para recuperar commits perdidos, branches apagadas ou alterações que foram sobrescritas.

```bash
git reflog
```

Exemplo de recuperação:

```bash
git checkout <hash-do-commit>
```

Esses comandos devem ser usados com entendimento do impacto que geram no histórico e na colaboração do time.

## Histórico de Commits

A seguir, encontra-se o histórico de commits do repositório, organizado em ordem cronológica, com base nas informações disponíveis no Git local.

| Hash      | Autor                | Data       | Mensagem                                               | Resumo                                                                       |
| --------- | -------------------- | ---------- | ------------------------------------------------------ | ---------------------------------------------------------------------------- |
| `8dcb8ec` | Mark09092009         | 2026-06-27 | Resolve conflito do merge                              | Finalizou a integração após a resolução de um conflito no processo de merge. |
| `5a212e9` | Mark09092009         | 2026-06-27 | Corrigido um texto no Index                            | Ajustou um texto na página inicial para corrigir conteúdo apresentado.       |
| `387a88f` | PedroLux-dev         | 2026-06-27 | Merge pull request #1 from Mark09092009/feature/css    | Integração da branch de estilo para a branch principal.                      |
| `9034449` | PedroLux-dev         | 2026-06-27 | Criado style para o formulário de contatos             | Adicionou estilos específicos para a seção de contato.                       |
| `2304437` | PedroLux-dev         | 2026-06-27 | Ajuste da página Contato para o Style                  | Ajustou a estrutura da página de contato para receber o estilo aplicado.     |
| `c55905a` | PedroLux-dev         | 2026-06-27 | Criado style para a estrutura e textos                 | Definiu a identidade visual e o layout do conteúdo.                          |
| `9b871f5` | Elissandra Rodrigues | 2026-06-25 | organiza habilidades por categorias e níveis           | Estruturou as habilidades em categorias e níveis de proficiência.            |
| `3b63777` | Elissandra Rodrigues | 2026-06-25 | adiciona descrições às habilidades                     | Incluiu descrições para cada habilidade apresentada.                         |
| `f13c59b` | Elissandra Rodrigues | 2026-06-25 | adiciona página de habilidades em formato de cards     | Implementou a página de habilidades com layout em cards.                     |
| `d01b397` | Mark09092009         | 2026-06-25 | Corrigido erros nos arquivos .html                     | Corrigiu inconsistências e pequenos erros nas páginas HTML.                  |
| `1779c17` | Luistav028           | 2026-06-25 | Juntando a Branch ao Main                              | Realizou a integração da seção de projetos na branch principal.              |
| `4dc59ed` | mariiaclarasm        | 2026-06-25 | Adiciona informações de contato da equipe à página     | Incluiu dados de contato da equipe no portfólio.                             |
| `4ad1137` | mariiaclarasm        | 2026-06-25 | Implementa formulário de contato no portfólio          | Adicionou um formulário de contato ao site.                                  |
| `4109725` | mariiaclarasm        | 2026-06-25 | Adiciona página de contato com informações da equipe   | Criou a página de contato com os dados da equipe.                            |
| `e41c361` | Luistav028           | 2026-06-25 | Finaliza seção de projetos com tecnologias utilizadas  | Completou a página de projetos com informações sobre tecnologias.            |
| `5026cee` | Luistav028           | 2026-06-25 | Adiciona novos projetos ao portfólio                   | Incluiu novos projetos na seção correspondente.                              |
| `8b04370` | Luistav028           | 2026-06-25 | Cria estrutura inicial da seção de projetos            | Definiu a estrutura inicial da página de projetos.                           |
| `5efcbb1` | Tayla Maria          | 2026-06-25 | Organizando as informações dos integrantes do grupo    | Reformulou e organizou os dados pessoais e acadêmicos dos integrantes.       |
| `059f7a9` | Tayla Maria          | 2026-06-25 | integra portfólio profissional à página de integrantes | Conectou a apresentação profissional à seção de integrantes.                 |
| `485567b` | Tayla Maria          | 2026-06-25 | adiciona biografia e habilidades aos integrantes       | Incluiu biografias e informações de habilidades para cada integrante.        |
| `5e1b945` | Tayla Maria          | 2026-06-25 | cria estrutura inicial da página de integrantes        | Estruturou a página inicial da seção de integrantes.                         |
| `cc61053` | Mark09092009         | 2026-06-24 | Adiciona seção sobre o projeto e cards informativos    | Criou a seção descritiva do projeto e os cards informativos.                 |
| `b20ba88` | Mark09092009         | 2026-06-24 | Adiciona banner principal da página inicial            | Implementou o banner principal da landing page.                              |
| `4cb8a29` | Mark09092009         | 2026-06-24 | Cria estrutura inicial da página inicial               | Definiu a base estrutural da página principal.                               |
| `60663b0` | Mark09092009         | 2026-06-24 | Criado o arquivo habilidades.html                      | Criou a página de habilidades do projeto.                                    |
| `0d79003` | Mark09092009         | 2026-06-24 | Corrigido o nome dos integrantes                       | Corrigiu inconsistências de nomes na lista de integrantes.                   |
| `6e0cac3` | Mark09092009         | 2026-06-24 | Criado a estrutura base e README inicial               | Estabeleceu a estrutura inicial do projeto e documentou o repositório.       |

## Estratégia de Branches

As branches foram utilizadas como mecanismo principal de organização do trabalho colaborativo. Cada integrante trabalhou em uma branch específica para desenvolver uma parte do portfólio, contribuindo para a branch principal apenas quando a implementação estava pronta.

### Branches existentes no projeto

| Branch                | Finalidade                                               | Status    |
| --------------------- | -------------------------------------------------------- | --------- |
| `main`                | Branch principal de integração e entrega do projeto.     | Ativa     |
| `feature/index`       | Desenvolvimento da página inicial e estrutura principal. | Utilizada |
| `feature/contato`     | Implementação da página de contato e formulário.         | Utilizada |
| `feature/css`         | Desenvolvimento de estilos e layout visual do projeto.   | Utilizada |
| `feature/habilidades` | Criação da página de habilidades.                        | Utilizada |
| `feature/integrantes` | Desenvolvimento da seção de integrantes.                 | Utilizada |
| `feature/projetos`    | Implementação da seção de projetos.                      | Utilizada |

### Fluxo de trabalho adotado

1. Cada tarefa iniciou em uma branch dedicada.
2. As alterações foram commitadas com mensagens descritivas.
3. Quando uma parte estava pronta, a branch era integrada à branch principal por meio de merge ou pull request.
4. A branch `main` foi mantida como ponto central de estabilização do projeto.

## Merge e Integração

O projeto realizou integrações em pontos importantes do desenvolvimento, especialmente quando uma funcionalidade concluída precisava ser incorporada à versão principal.

### Merges identificados

| Commit    | Branch integrada            | Comandos utilizados                                                                          | Observação                                                       |
| --------- | --------------------------- | -------------------------------------------------------------------------------------------- | ---------------------------------------------------------------- |
| `387a88f` | `feature/css` → `main`      | `git checkout main`, `git pull origin main`, `git merge feature/css`, `git push origin main` | Integração da estilização do projeto.                            |
| `1779c17` | branch de projetos → `main` | `git checkout main`, `git merge <branch-de-projetos>`, `git push origin main`                | Integração da seção de projetos.                                 |
| `8dcb8ec` | resolução de merge          | `git add`, `git commit`                                                                      | Commit dedicado à resolução de um conflito durante a integração. |

## Resolução de Conflitos

Conflitos ocorreram quando duas alterações diferentes afetaram a mesma área de um arquivo durante a integração das branches. No histórico analisado, há evidência de que esse tipo de situação foi tratada no processo de merge, com o commit `8dcb8ec` registrando a resolução.

Exemplo típico de marcadores de conflito do Git:

```text
<<<<<<< HEAD
Conteúdo da versão atual da branch principal
=======
Conteúdo da versão recebida da outra branch
>>>>>>> branch
```

### Como a resolução foi tratada

1. O arquivo conflitante foi aberto para análise.
2. As alterações foram comparadas e a versão correta foi escolhida.
3. As marcações de conflito foram removidas.
4. O arquivo foi marcado como resolvido com:

```bash
git add nome-do-arquivo
git commit -m "fix: resolver conflito de merge"
```

## Comandos Avançados do Git

Durante o desenvolvimento, foram utilizados vários comandos do Git para criar branches, integrar alterações, sincronizar com o repositório remoto e revisar o histórico.

### `git checkout -b`

Cria uma nova branch e já muda para ela imediatamente.

```bash
git checkout -b feature/nome-da-feature
```

### `git merge`

Integra as alterações de uma branch em outra. É o comando principal para consolidar o trabalho em `main`.

```bash
git checkout main
git merge feature/css
```

### `git pull`

Atualiza a branch local com as mudanças mais recentes do repositório remoto.

```bash
git pull origin main
```

### `git push -u`

Envia a branch local para o GitHub e define o rastreamento com o remoto.

```bash
git push -u origin feature/index
```

### `git branch`

Lista as branches existentes e mostra a branch atual.

```bash
git branch -a
```

### `git log`

Exibe o histórico de commits, permitindo acompanhar a evolução do projeto.

```bash
git log --oneline --decorate
```

### `git fetch`

Baixa informações atualizadas das branches remotas sem integrar imediatamente as mudanças.

```bash
git fetch origin
```

### `git rebase`

Reorganiza o histórico de commits, reaplicando alterações de uma branch sobre outra. Pode ser usado para manter o histórico mais linear.

```bash
git rebase origin/main
```

### `git reset`

Move o ponteiro do repositório para um ponto anterior do histórico. Pode ser usado com diferentes níveis de impacto:

```bash
git reset --soft HEAD~1
git reset --mixed HEAD~1
git reset --hard HEAD~1
```

### `git stash`

Salva alterações temporárias sem precisar criar um commit.

```bash
git stash
git stash pop
```

## Fluxo de Desenvolvimento

O fluxo de desenvolvimento do projeto seguiu uma abordagem colaborativa baseada em branches e integração gradual.

1. A estrutura inicial do projeto foi criada na branch principal.
2. Cada integrante iniciou uma branch específica para uma funcionalidade ou página.
3. As alterações foram desenvolvidas e commitadas com mensagens claras.
4. As branches foram atualizadas com `pull` e `fetch` para evitar divergências.
5. Quando a tarefa estava concluída, a branch era integrada à branch principal por meio de merge ou pull request.
6. O processo finalizou com a consolidação das páginas do portfólio na versão principal do projeto.

## Conclusão

Este projeto proporcionou uma experiência prática relevante no uso de Git e GitHub em ambiente colaborativo. Através do controle de versão, foi possível acompanhar cada alteração, organizar o trabalho entre os integrantes, integrar funcionalidades de forma segura e registrar o histórico de desenvolvimento de forma clara.

O uso adequado de commits, branches, merges e resolução de conflitos mostrou a importância do controle de versão em projetos acadêmicos e profissionais, pois melhora a organização, reduz riscos de perda de informação e facilita a colaboração entre equipes.
