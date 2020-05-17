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
	
Passo a passo:
1. Acesse o seu repositório "forkado";
2. Clique no botão Compare & Pull Request;
3. Adicione um título a sua solicitação;
4. Adicione um comentário se necessário, esse comentário pode ser um descritivo de sua alteração e/ou uma justificativa da necessidade dela;
5. Confirme a criação de sua solicitação.
