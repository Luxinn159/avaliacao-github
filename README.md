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
