# Configurar o servidor SSH

A essa altura você já deve ter seu usuário devidamente configurado. Está na hora de proteger melhor o acesso ao servidor!!!

## Desativar o login do usuário root

O usuário `root` é o administrador geral do sistema. Ele pode acessar qualquer arquivo e serviço. Como disse o *Tio Ben*: "com grandes poderes vêm grandes responsabilidades". Com isso em mente, é uma boa prática desabilitar o login do `root` pelo SSH.


Uma vez logado com o seu usuário, abra o arquivo de configuração do servidor SSH:
    
    $ sudo nano /etc/ssh/sshd_config

Procure pela linha que contém o texto abaixo:

    PermitRootLogin yes

> ℹ️ Você pode pesquisar pressionando as teclas `ctrl + w`.

Uma ves localizado, substitua o *yes* por *no*:

    PermitRootLogin no

> ℹ️ As linhas que começam com o caracter `#` são comentários e são ignoradas pelo serviço. Caso a linha mencionada esteja comentada, delete o caracter `#` para a configuração surtir efeito.

## Desativar o login com senha

Você já deve ter criado sua chave SSH e já fez a instalação dela no servidor (caso não, [siga esses passos](https://github.com/francoisjun/how-to/blob/main/linux/criar_chave_ssh.md)). É interessante desativar o login por senha para evitar ataques de força bruta. Para isso, localize a linha abaixo:

    PasswordAuthentication yes

Da mesma forma que no passo anterior, substitua o *yes* por *no*:

    PasswordAuthentication no

> 🚨 Cuidado! Caso não tenha configurado **e testado** o login por chave SSH, desabilitar o login por senha vai impossibilitar o acesso ao servidor.

## Alterar a porta de acesso (opcional)

A porta padrão de acesso ao SSH é a 22. Todo mundo sabe disso e isso pode ser um problema. Scanners de rede vão verificar essa porta e reportá-la como aberta. Uma opção é mudar o número da porta para dificultar esse rastreamento.

Procure pela linha abaixo (geralmente encontra-se no início do arquivo):

    #Port 22

Por ser a porta padrão, a linha geralmente vem comentada. Delete o caracter `#` e altere o valor para um outro de preferencia:

    Port 2002

> 🚨 Cuidado para não utilizar uma porta que já está sendo usada por outro serviço. Caso contrário, o servidor SSH não vai executar.

Para acessar por uma porta customizada, utilize o comando `ssh` com o parâmetro `-p numero_porta`:

    $ ssh -p 2002 nome_usuario@ip_do_servidor

## Reiniciar o servidor SSH para aplicar as alterações

Salve o arquivo de configuração pressionando as teclas `ctrl + x` (confirme que deseja salvar as alterações). Em seguida, reinicie o servidor SSH com o comando abaixo:

    $ sudo systemctl restart sshd.service