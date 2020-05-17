# Guia prático (e resumido) de comandos do git

Além de conter alguns passos para acabar com a raça do git, há alguns links com resumos práticos e leituras interessantes.


## O Git Básico

### Inicializando um novo repositório

**Utilizando *git clone***

Esse processo é utilizado quando já existe conteúdo no repositório remoto e você deseja criar uma cópia local.
O *git clone* é usado para apontar para um repositório existente e fazer um clone ou cópia deste repositório em outro local.
Por conveniência, a clonagem cria com agilidade uma conexão remota chamada "origem" apontando para o repositório original. Isso facilita muito a interação com um repositório central.

Passo a passo:

1. Crie um repositório na sua conta do GitHub (Inicialize seu repositório marcando a opção de criar um arquivo README);
2. Obtenha o endereço do repositório através do botão **Clone or download** na página de seu projeto;
3. Crie uma pasta em seu computador e acesse ela (ou utilize alguma pasta já existente);
4. Execute o comando *git clone* seguido do endereço copiado. Ex.: *git clone https://github.com/reprograma/T9-git.git*, onde o endereço é a url para clone.

**Utilizando *git remote***

Esse processo é utilizado quando o repositório remoto está vazio, você já tem arquivos em sua máquina, e deseja enviá-los para o repositório remoto.
O comando *git init* cria um novo repositório do Git. Ele pode ser usado para converter um projeto existente e não versionado em um repositório do Git ou inicializar um novo repositório vazio.
O comando *git remote* é um comando com uma série de funções. Ele permite criar, ver e excluir conexões com outros repositórios.

Passo a passo:

1. Crie um repositório na sua conta do GitHub (Não inicialize criando um arquivo README, queremos um repositório vazio);
2. Obtenha o endereço do repositório através do botão **Clone or download** na página de seu projeto;
3. Crie uma pasta em seu computador e acesse ela, (ou utilize alguma pasta já existente);
4. Execute os seguintes comandos:
	1. *git init* (cria os arquivos necessários para tornar sua pasta um repositório local, esses arquivos vão aparecer numa pasta oculta chamada .git);
	2. *git remote add origin enderecodorepositorio* (esse comando informa qual é o repositório remoto com que o seu repositório local vai se comunicar);
    3. *git push -u origin master* ou *git push origin master* (esse comando "empurra" suas alterações para o repositório remoto, nesse caso *master* indica em qual branch você está trabalhando, veremos o mesmo comando utilizando outra branch mais a frente).

### Adicionar e confirmar alterações

Após fazer suas alterações em seu projeto, elas ainda não estão verdadeiramente salvas em seu repositório local. Para salvar essas alterações em seu repositório precisamos utilizar o comando *git add*, ele informa ao Git que você quer incluir atualizações a um arquivo particular na próxima confirmação. 

    *git add <file>* - Adiciona todas as alterações em <file> para a próxima confirmação.

    *git add <directory>* - Adiciona todas as alterações em <directory> para a próxima confirmação.

    *git add --all* (ou alguma de suas variações) - Adiciona todas as alterações do repositório para a próxima confirmação.

No entanto, *git add* não afeta realmente o repositório de nenhuma forma significativa — as alterações não são realmente gravadas ou confirmadas até você executar *git commit*.

    *git commit* - Faça o commit do instantâneo preparado, o que abre um editor de texto solicitando a você uma mensagem de commit. Depois de escrever a mensagem, salve o arquivo e feche o editor para criar o commit real.

    *git commit -m "mensagem"* - Um comando de atalho que cria de imediato um commit com uma mensagem de commit transmitida. Transmitir a opção -m vai pular a solicitação do editor de texto em favor de uma mensagem integrada.

Coloque uma mensagem que defina exatamente o que você fez. De preferência, a cada pequena parte que você codar, comite com uma mensagem que diga o que está sendo feito até ali.

Fontes: 
* https://rogerdudler.github.io/git-guide/index.pt_BR.html
* https://www.atlassian.com/br/git/tutorials
* https://blog.da2k.com.br/2015/02/04/git-e-github-do-clone-ao-pull-request/

## Fork

Cria uma cópia do repositório principal de um código-fonte do projeto em seu perfil do GitHub. Assim, você pode modificar o projeto sem afetar o repositório principal desse projeto.
O fork é usado principalmente para indicar ou propor alterações no projeto de origem ou criar uma nova ideia usando essa fonte de projeto como ponto de partida.
	
Por que precisamos de Fork?
* Você pode não ter permissão de gravação para trabalhar diretamente no repositório principal.
* Se todos clonarem e trabalharem diretamente no repositório/branch principal do projeto, será muito difícil de gerenciar.

Passo a passo:
1. Acesse o repositório fornecido por mim e clique no botão **Fork**;
2. Faça um *git clone* (siga o passo a passo da seção anterior) do repositório que você "forkou";
3. Adicione alguns arquivos ao repositório local, confirme e envie suas alterações.

As alterações que você fez não serão replicadas para o repositório remoto original. Além disso, se um contribuidor com acesso ao repositório remoto principal fizer uma atualização um simples *git pull* não irá atualizar seu repositório local nem seu repositório remoto. Para atualizar o seu projeto com as alterações do repositório remoto original segue um passo a passo.

Passo a passo:

1. Acesse seu repositório local utilizando o terminal;
2. Utilize o comando *git remote -v* para verificar quais repositórios remotos estão ligados ao seu repositório local. As linhas que contém o seu repositório remoto devem estar iniciadas pela palavra *origin*. As linhas que contém o repositório remoto original devem estar iniciadas pela palavra *upstream*. No caso do repositório remoto você pode se deparar com três situações: (1) o repositório remoto original está correto, passe para o passo 5; (2) não há um repositório "marcado" como *upstream*, é preciso indicar o repositório remoto original, siga para o passo 4; (3) existe um repositório "marcado" como *upstream* entretanto o endereço não corresponde ao repositório remoto original, siga para o passo 3;
3. Antes de indicar o repositório remoto original correto, é necessário excluir a ligação com o repositório remoto incorreto. Utilize o comando *git remote rm upstream*. rm nesse comando quer dizer remove. Utilize novamente o comando *git remote -v* para verificar se o comando funcionou corretamente;
4. Agora vamos adicionar um novo repositório remoto, para isso vamos utilizar um comando já conhecido. Utilize *git remote add origin enderecodorepositorio*, onde o endereço do repositório deve ser a url para clone do repositório original. Utilize novamente o comando *git remote -v* para verificar se o comando funcionou corretamente;
5. Para obter as atualizações do repositório remoto original, utilize o comando *git fetch upstream* e em seguida *git pull upstream*;
6. Até esse ponto seu repositório local já deve estar atualizado com as alterações do repositório remoto original, utilize os comandos já aprendidos na seção anterior para enviar as atualizações para seu repositório remoto.

Caso deseje enviar suas alterações para o repositório principal crie uma solicitação de atualização (pull request) para o repositório principal. Se o(s) proprietário(s) do repositório principal desejarem, eles mesclarão suas alterações ao repositório principal. Essa função é muito utilizada em projetos de código aberto em que todos podem contribuir. Por exemplo, alguém desenvolve um plugin e outras pessoas podem ajudar traduzindo arquivos, corrigindo problemas ou adicionando novas funcionalidades; no entanto, ao invés de essas alteração serem enviadas diretamente ao repositório, quem contribuiu solicita que o proprietário aceite suas alterações; o proprietário por sua vez decide se quer que essas modificações feitas por terceiros sejam incorporadas ao seu projeto. 

Passo a passo para Pull Request:
1. Acesse o seu repositório "forkado";
2. Clique no botão **Compare & Pull Request**;
3. Adicione um título a sua solicitação;
4. Adicione um comentário se necessário, esse comentário pode ser um descritivo de sua alteração e/ou uma justificativa da necessidade dela;
5. Confirme a criação de sua solicitação.

Passo a passo para aceitar o Pull Request:
*(em construção)*

Fonte: 
https://medium.com/@tharis63/git-fork-vs-git-clone-8aad0c0e38c0
https://github.com/grupy-sp/encontros/wiki/Como-sincronizar-o-seu-Fork-com-o-repo-principal

## Branches

Branches ("ramos") são utilizados para desenvolver funcionalidades isoladas umas das outras. A branch master é a branch "padrão" quando você cria um repositório. Use outras branches para desenvolver e mescle-os (merge) ao branch master após a conclusão. Uma branch permite que várias pessoas trabalhem em um mesmo repositório em funcionalidades que não se relacionam uma com a outra. Ao finalizar as alterações, a branch criada pode ser reintegrada a branch principal (master).

O comando *git branch* permite criar, listar, renomear e excluir ramificações. Ele não permite que você alterne entre as ramificações ou reúna uma história bifurcada novamente. Por esse motivo, o comando *git branch* é comumente integrado com os comandos *git checkout* e *git merge*.

    *git branch <branch>* - Criar uma nova ramificação chamada <branch>. Isso não verifica a nova ramificação.

    *git branch -D <branch>* - Excluir localmente uma ramificação chamada <branch>.

    *git push origin --delete <branch>* - Excluir remotamente uma ramificação chamada <branch>.

O comando *git checkout* permite navegar entre branches criados pelo *git branch*. O comando *git checkout* pode, às vezes, ser confundido com o *git clone*. A diferença entre os dois é que o clone trabalha para buscar código de um repositório remoto, já o checkout serve para alternar entre versões de código já existentes no repositório local (sua máquina).

    *git checkout <branch>* - O comando seleciona a ramificação <branch> a ser trabalhada.

    *git checkout -b <new-branch>* - Cria e alterna para <new branch> ao mesmo tempo. A opção -b é uma sinalização de conveniência que diz ao Git para rodar o *git branch <new-branch>* antes de rodar o *git checkout <new-branch>*.

Ao colaborar com uma equipe, é comum utilizar repositórios remotos. Esses repositórios podem ser hospedados e compartilhados ou podem ser uma cópia local de outro colega. Para verificar um branch remoto, você precisa primeiro buscar o conteúdo do branch.

    *git fetch --all* - Atualiza a lista local de branches.

    *git checkout <remotebranch> origin/<remotebranch>* - Em versões mais antigas do Git para alternar para uma branch remota você deve usar este comando, onde <remotebranch> é o nome da branch. Em versões mais novas você pode simplesmente utilizar *git checkout <remotebranch>*.

A mesclagem é o jeito do Git de unificar diferentes linhas de desenvolvimento (branches). O comando *git merge* permite que você pegue as linhas de desenvolvimento independentes criadas pelo *git branch* e as integre em um único branch.

Vamos supor que temos um novo recurso de branch que é baseado na branch principal. Agora, a gente quer mesclar este recurso no branch principal.

![](https://wac-cdn.atlassian.com/dam/jcr:86eba9ec-9391-45ea-800a-948cec1f2ed7/Branch-2.png?cdnVersion=1017)

Executar este comando vai mesclar o recurso de branch especificado no branch atual, vamos supor que seja a principal.

![](https://wac-cdn.atlassian.com/dam/jcr:83323200-3c57-4c29-9b7e-e67e98745427/Branch-1.png?cdnVersion=1017)

Passo a passo (considere um projeto para um aplicativo de câmera em que cada desenvolvedor trabalha numa funcionalidade diferente):

1. *git checkout -b feature-focus* (Cria nova ramificação chamada feature-focus e seleciona ela para trabalhar);
2. Vamos fazer algumas alterações:
    1. *git add <file>*
    2. *git commit -m "Adicionando foco manual"*
3. Vamos fazer mais algumas alterações:
    1. *git add <file>*
    2. *git commit -m "Adicionando foco automático"*
4. Você concluiu a funcionalidade que você estava desenvolvendo, e não há mais necessidade de utilizar essa branch.
    1. *git checkout master* (alternando para a branch principal, a master);
    2. *git merge feature-focus* (mesclando as alterações da branch que você desenvolveu à master);
    3. *git branch -d feature-focus* (excluindo a branch que você desenvolveu)

O passo a passo acima, foi feito considerando uma branch que só existia localmente. Se você quiser enviar sua branch para o repositório remoto não se esqueça de usar os comandos que informam qual a origem remota do seu repositório, bem como *git push -u origin <suabranch>* na primeira vez que fizer um push.

Se as duas ramificações que você está tentando mesclar alterarem a mesma parte do mesmo arquivo, o Git pode não conseguir decidir qual versão usar. Quando essa situação ocorre, ele para antes do commit de mesclagem para que você possa resolver os conflitos.

Quando você encontra um conflito de mesclagem, executar o comando *git status* vai exibir quais arquivos precisam ser resolvidos. O Git vai editar o conteúdo dos arquivos afetados com indicações visuais, marcando ambos os lados do conteúdo em conflito. Estas marcações visuais são: <<<<<<<, =======, e >>>>>>>. É útil pesquisar um projeto por estes indicadores durante uma mesclagem para encontrar onde conflitos precisam ser resolvidos. (Veja o exemplo abaixo)

    aqui está um conteúdo não afetado pelo conflito
    <<<<<<< master
    aqui está um texto conflitante do branch principal
    =======
    aqui está um texto conflitante da branch de recurso

Em geral, o conteúdo antes do marcador ======= é o branch receptor e a parte seguinte é o branch que vai ser mesclado.

Após identificar as seções conflitantes, você pode corrigir a mesclagem como preferir. Quando você estiver pronto para concluir a mesclagem, tudo o que precisa fazer é executar *git add* no(s) arquivo(s) conflitante(s) para dizer ao Git que eles foram resolvidos. Em seguida, você executa um *git commit* normal para gerar o commit de mesclagem.