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
