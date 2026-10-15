# avaliacao-github

Projeto de Desenvolvimento Web com GitHub Actions.

## Objetivo

Demonstrar a utilização de integração contínua (CI), validação automática de código e proteção da branch principal no GitHub.

## GitHub Actions

O projeto utiliza um workflow de CI que executa verificações automáticas:

- Verificação de possíveis segredos no repositório.
- Execução das migrações SQL em um banco SQLite de teste.
- Validação dos arquivos HTML.

## Proteção da branch main

Foi configurado um Ruleset para proteger a branch `main`, exigindo:

- Criação de Pull Request antes da integração.
- Aprovação dos status checks obrigatórios.
- Restrição de exclusão da branch.

## Testes realizados

Foi criado um Pull Request contendo um erro em uma migração SQL.

O GitHub Actions identificou a falha e os testes não passaram.

Após a correção do código, os testes foram executados novamente e concluídos com sucesso.

O Pull Request #2 foi integrado à branch `main` após a aprovação dos três checks.

## Resultado

A atividade demonstrou como o GitHub Actions pode identificar erros automaticamente e como as regras de proteção ajudam a impedir a integração de alterações que não passaram nas verificações obrigatórias.
## Evidências do projeto

As capturas de tela foram adicionadas ao repositório no Pull Request #11.

### Integração contínua (CI)
Os testes automáticos verificam o código HTML, as migrações SQL e possíveis segredos no repositório.

### Proteção da branch main
As alterações são realizadas por Pull Requests, com verificações obrigatórias antes da integração.

### Revisão de código com IA
O workflow de revisão automática analisa as alterações e publica comentários nos Pull Requests.

### Cloudflare Pages
O projeto possui implantação automática pelo Cloudflare Pages.

### Banco de dados Cloudflare D1
O banco `banco_avaliacao` contém a tabela `notas`, incluindo a coluna `observacao`.

### Capturas de tela
As 10 imagens de evidência estão disponíveis na raiz do repositório.

[Ver as evidências no Pull Request #11](https://github.com/Luxinn159/avaliacao-github/pull/11)
