# 🤦 Criando um usuário no linux

Ao criar uma nova VM você obtem acesso pelo usuário root. No entanto não é boa prática utilizar esse usuário a todo momento. Vamos iniciar as configurações adicionando um usuário para você chamar de seu!

Primeiramente faça o login no servidor linux com o usuário root via SSH:

    $ ssh root@<ip_servidor>

> ℹ️ As linhas de comando iniciadas com `#` indicam que são executadas como usuário root, enquanto que as iniciadas com `$` indicam usuário comum. 

Use o comando `adduser` com a seguinte sintaxe:

    # adduser nome_usuario

onde `nome_usuario` é o nome que você deseja. O nome de usuário não pode conter espaços.

O comando solicitará uma senha e sua confirmação, além de algumas outras informações, como seu nome completo, telefone, etc. Apenas pressione a tecla *enter* para as informações que não deseja informar. Abaixo segue a saída do comando em uma simulação:

    # adduser nome_usuario
    Adding user `nome_usuario' ...
    Adding new group `nome_usuario' (1002) ...
    Adding new user `nome_usuario' (1002) with group `nome_usuario' ...
    Creating home directory `/home/nome_usuario' ...
    Copying files from `/etc/skel' ...
    New password: 
    Retype new password: 
    passwd: password updated successfully
    Changing the user information for nome_usuario
    Enter the new value, or press ENTER for the default
    	Full Name []: Meu Nome         
    	Room Number []: 
    	Work Phone []: 
    	Home Phone []: 
    	Other []: 
    Is the information correct? [Y/n]

> 💡 Quando o comando espera uma resposta do usuário, como Yes ou No, a resposta padrão aparece em caixa alta. Para aceitá-la, basta pressionar a tecla *enter*.

## Dando poder administrativo ao usuário

Caso o novo usuário precise executar comandos a nível de administrador (como apt-get ou editar arquivos de configuração do sistema), adicione-o ao grupo `sudo`. 

O comando e sua sintaxe segue abaixo:

    # usermod -a -G sudo nome_usuario

onde: 
- `-a` indica que o novo grupo será adicionado à lista de grupos que o usuário já possui;
- `-G sudo` informa o nome do grupo que será adicionado.

> 🚨 Caso não seja passado o parâmetro `-a`, a lista de grupos do usuário será substituída, ficando apenas o grupo informado no parâmetro `-G`.

Após adicioná-lo ao grupo, vamos fazer um teste para confirmar se está tudo funcionando.

Mude o usuário ativo para o novo usuário e tente executar um comando administrativo:

    # su nome_usuario
    $ sudo apt update

Se o comando for executado com sucesso, você já pode se logar diretamente com seu usuário e sempre que precisar executar comandos administrativos inclua o comando `sudo` antes do comando principal (será solicitado a senha do seu usuário quando executar o comando `sudo` na primeira vez na sessão).