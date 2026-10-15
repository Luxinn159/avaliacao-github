# AVALIAÇÃO — GitHub Actions e Cloudflare

## 1. Repositório do projeto

https://github.com/Luxinn159/avaliacao-github

## 2. Integração contínua (CI)

O projeto utiliza GitHub Actions para executar verificações automáticas nas alterações do repositório.

As verificações incluem validações de arquivos, segurança e integração com o Cloudflare Pages.

## 3. Revisão automática com IA

Foi configurado um workflow de revisão automática com IA para analisar Pull Requests e publicar comentários com os resultados.

## 4. Implantação no Cloudflare Pages

O projeto está integrado ao Cloudflare Pages, permitindo a implantação automática do site.

## 5. Migrações do banco Cloudflare D1

O projeto utiliza migrações SQL para controlar as alterações no banco de dados D1.

Foram criadas três migrações:
- `0001_criar_tabela.sql`
- `0002_teste_erro.sql`
- `0003_adiciona_coluna.sql`

Execução bem-sucedida das migrações:

https://github.com/Luxinn159/avaliacao-github/actions/runs/3878526052

## 6. Evidências

As capturas de tela do projeto estão disponíveis na pasta:

https://github.com/Luxinn159/avaliacao-github/tree/main/evidencias

## 7. Pull Requests

Os Pull Requests foram utilizados para revisar e integrar alterações à branch `main`, respeitando a proteção configurada.

Histórico de Pull Requests:

https://github.com/Luxinn159/avaliacao-github/pulls

## 8. Considerações finais

O projeto demonstra o uso de GitHub Actions para integração contínua, revisão automatizada com IA, implantação no Cloudflare Pages e aplicação de migrações no banco Cloudflare D1.
## 9. Respostas às perguntas da avaliação

### Pergunta 1 — Por que o CI roda duas vezes?

O `ci.yml` roda duas vezes porque está configurado para os eventos `push` e `pull_request`. Quando fazemos push em uma branch com PR aberto, os dois eventos podem disparar execuções, mas a proteção da `main` considera o status check exigido pela regra de proteção, associado ao PR.

### Pergunta 2 — Por que um fork não recebe o COPILOT_PAT?

Por segurança, os workflows de Pull Requests vindos de forks não recebem os segredos do repositório de destino, como `secrets.COPILOT_PAT`. Isso impede que alguém envie código malicioso em um PR para tentar roubar tokens e outras credenciais.

### Pergunta 3 — Por que declarar permissions?

O workflow declara `permissions` para definir explicitamente quais acessos o `GITHUB_TOKEN` precisa ter, seguindo o princípio do menor privilégio. A revisão precisa ler o conteúdo do repositório e publicar comentários nos Pull Requests, sem receber permissões desnecessárias.

### Pergunta 4 — A revisão da IA substitui o CI?

Não. A revisão da IA pode ajudar a identificar problemas, mas suas respostas podem conter erros, omissões ou observações irrelevantes; por isso, precisam de avaliação humana. O CI executa verificações automáticas e objetivas que podem bloquear um merge quando falham, enquanto a IA funciona como uma análise complementar.
