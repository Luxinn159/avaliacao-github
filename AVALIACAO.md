# Avaliação: GitHub Actions com IA

**Repositório:** https://github.com/Luxinn159/avaliacao-github

## Tarefa 1 — CI a cada commit

Foi criado o workflow `.github/workflows/ci.yml`, com verificações automáticas de possíveis segredos versionados, migrações SQL em SQLite local e validação de HTML.

**Execução aprovada:** [Adicionar link da execução verde]

**Execução com erro proposital:** [Adicionar link da execução vermelha]

**Erro identificado no log:** [Adicionar a mensagem do erro de SQL]

**Por que testar as migrações no SQLite antes do D1?**

Porque isso permite identificar erros de sintaxe ou estrutura no SQL antes de aplicar as alterações no banco de dados remoto.

## Tarefa 2 — Proteção da branch main

Foi configurada uma regra de proteção da branch `main`, exigindo pull request e aprovação do status check `verificar`.

**PR bloqueado e posteriormente liberado:** [Adicionar link do PR]

**Evidência de push direto recusado:** [Adicionar saída do comando ou evidência]

## Tarefa 3 — Revisão automática por IA

Foi criado o workflow `.github/workflows/revisao-ia.yml`, utilizando `actions/ai-inference` para analisar alterações e publicar comentários nos pull requests.

**PR com comentários da IA:** [Adicionar link do PR com as duas revisões exigidas]

**Teste de erro de permissão:** [Adicionar link da execução com erro]

**Análise crítica da IA:**

No PR #10, a IA informou que não havia diferenças para revisar. A aba *Files changed* também mostrou que não existiam arquivos alterados. Esse caso demonstra que uma revisão automática pode não produzir uma análise útil quando não recebe alterações de código. Por isso, os comentários da IA precisam ser avaliados criticamente e não devem substituir os testes automáticos.

## Tarefa 4 — Migrações D1 após o merge

Foi criado o workflow `.github/workflows/migrar.yml`, configurado para executar após um `push` na branch `main` que altere arquivos da pasta `migrations/`.

**Execução aprovada da migração:**

https://github.com/Luxinn159/avaliacao-github/actions/runs/38785260502

**Migração aplicada:** `0003_adiciona_coluna.sql`

**Banco:** `banco_avaliacao`

**Consulta de verificação:**

```sql
PRAGMA table_info(notas);
```

**Resultado observado:** a tabela `notas` possui as colunas `id`, `aluno`, `nota` e `observacao`. A coluna `observacao` foi confirmada no banco D1 remoto com o tipo `TEXT`.

**Merge sem alterações em `migrations/`:** [Adicionar link do PR após realizar o teste]

**Evidência de que o workflow não executou:** [Adicionar descrição e link da página de Actions]

## Perguntas

### 1. Por que o ci.yml roda duas vezes quando há push em uma branch com PR aberto? Qual execução a proteção da main considera?

Porque o workflow está configurado para os eventos `push` e `pull_request`. Um commit enviado para uma branch com PR aberto pode disparar uma execução para cada evento. A proteção da `main` considera o status check exigido para o pull request antes de permitir o merge.

### 2. Por que um PR vindo de um fork não consegue usar secrets.COPILOT_PAT? Qual ataque essa regra impede?

Por segurança, os segredos do repositório não são disponibilizados normalmente aos workflows de pull requests vindos de forks. Isso impede que alguém envie código malicioso em um PR para tentar capturar tokens e outras credenciais privadas.

### 3. Por que o workflow da Tarefa 3 declara permissions em vez de usar as permissões padrão do GITHUB_TOKEN?

Porque o workflow precisa de permissões específicas para ler o conteúdo e publicar comentários nos pull requests. Declarar `permissions` explicitamente permite controlar os acessos e aplicar o princípio do menor privilégio.

### 4. A revisão da IA pode substituir o status check da Tarefa 2?

Não. A revisão da IA pode ajudar a identificar problemas, mas suas respostas dependem do contexto e podem ser incompletas ou irrelevantes. O status check executa verificações automáticas e fornece um resultado objetivo para bloquear o merge quando alguma verificação obrigatória falha.
