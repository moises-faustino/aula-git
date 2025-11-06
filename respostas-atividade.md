### 📘Perguntas
**1. Por que o Git é considerado um sistema de controle de versão
 distribuído?**
 
 💡 Resposta: Porque cada clone contém todo o histórico e os metadados do repositório (commits, branches, tags). Assim, é possível commitar, revisar histórico e criar branches offline, sem depender de um servidor central.

**2. Qual a diferença entre working directory, staging area e repository?** 

💡 Resposta:
* Working directory (árvore de trabalho): os arquivos “normais” no disco, que editamos
* Staging area (index): “área de preparação” onde selecionamos exatamente o que vai entrar no próximo commit.
* Repository (.git): banco de dados de objetos e referências (commits, blobs, trees, refs), que guarda o histórico.

**3. Para que serve o comando git clone ?**

💡 Resposta: Para copiar um repositório existente (inclusive seu histórico completo) para nossa máquina, já configurando o remote padrão (origin).

**4. Onde estão implementados fisicamente working directory, staging area e repository ?**

💡Resposta:
Working directory: pasta onde estamos (arquivos no sistema de arquivos).
Staging area: arquivo .git/index.
Repository: pasta .git/ (contém objects/, refs/, HEAD, etc.).

**5. Quais os estados de um arquivo no repositório do git ?**

💡Resposta:
* untracked (não rastreado)
* tracked (rastreados), que podem estar unmodified, modified ou staged
* (opcional) ignored (se listado em .gitignore)


**6. Explique as possíveis transições de estado de um arquivo no repositório do git ?**

💡Resposta:

* untracked → (git add) → staged → (git commit) → tracked/unmodified
* tracked/unmodified → (editar) → modified → (git add) → staged → (git commit) → unmodified
* untracked → (.gitignore) → ignored
* staged → (editar de novo o mesmo arquivo) → volta a modified (as mudanças novas não estão mais staged até você dar git add de novo)


### 2. Prática com Git Local
 Execute os comandos a seguir e responda às perguntas baseadas no
 resultado do terminal.

#### 🧩 Etapa 1 – Criar o repositório
 mkdir aula-git
 cd aula-git
 git init
 
**Pergunta: Qual foi a mensagem exibida após o comando git init e o que ela significa na prática?**

💡Resposta: 
```Initialized empty Git repository in C:/Users/haruk/aula-git/.git/ ```
Significa que a pasta .git/ foi criada — a partir de agora, esta pasta é um repositório Git

 
#### 🧩 Etapa 2 – Adicionar arquivo e fazer commit
 echo "Primeiro arquivo" > arquivo.txt
 git status
 git add arquivo.txt
 git commit -m "Primeiro commit"

Perguntas:
 **1. Qual o estado do arquivo antes e depois do git add ?** 

💡 Resposta: Antes: Untracked / Depois: Staged

 **2. O que significa o estado untracked e tracked ?** 

💡 Resposta:
* untracked: o Git ainda não controla esse arquivo (não entrará no commit).
* tracked: o Git acompanha o arquivo; ele pode estar unmodified, modified ou staged

 **3. Qual o objetivo do git commit ?** 

💡 Resposta: Salvar um snapshot do que está staged no histórico, criando um novo commit com mensagem e metadados (autor, data, etc.).

 **4. Qual o estado do arquivo após o git commit ?** 

💡 Resposta: tracked/unmodified
 
#### 🧩Etapa 3 – Histórico e alterações

 git log --oneline
 echo "Nova linha" >> arquivo.txt
git diff

 Perguntas:
** 1. O que o comando git diff mostra? **

💡 Resposta:
```
diff --git a/arquivo.txt b/arquivo.txt
 index a602fde..b16172b 100644
--- a/arquivo.txt
+++ b/arquivo.txt
@@ -1 +1,2 @@
"Primeiro arquivo"
+"Nova linha"
```
Mostra as diferenças não staged entre o working directory e o que está comitado
 
**2. Qual commit está atualmente apontado por HEAD?**

💡 Resposta: O HEAD aponta para o último commit da branch atual “Primeiro commit”

#### 🧩 Etapa 4 – Trabalhando com Branches
 git branch nova-feature
 git checkout nova-feature
 echo "Linha da nova branch" >> arquivo.txt
 git add arquivo.txt
 git commit -m "Alteração na nova branch"

Perguntas:
 **1. Como verificar em qual branch você está?** 

💡Resposta: Existem algumas formas. 
* git status, que aparece “on branch …”
* git branch, onde o * indica a branch atual

 **2. O que acontece se você rodar git merge nova-feature estando na
 branch principal?**

💡 Resposta:

```
Updating 243e62b..bb0fa08
Fast-forward
 arquivo.txt | 2 ++
 1 file changed, 2 insertions(+)
```
O Git traz os commits da nova-feature para a branch principal


**3. Conectando ao GitHub**
 1. Crie um repositório vazio no GitHub chamado aula-git.
 2. Conecte o repositório local ao remoto:
 git remote add origin https://github.com/<usuario>/aula-git.git
 git branch -M main
 git push -u origin main
 
Perguntas:
 **1. O que significa o -u no comando git push -u origin main ?**

💡Resposta: Define upstream tracking: a branch local main passa a rastrear origin/main. Depois disso, é possível usar git push/git pull sem especificar o remote/branch.

 **2. Como verificar os remotes configurados no repositório?**
 
💡Resposta: Existem algumas opções
* git remote -v -> lista as URLs de fetch/push
* git remote show origin-> detalhes do remote e branches de rastreamento
