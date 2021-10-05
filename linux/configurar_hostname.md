# 🔖 Configurar o hostname do servidor

Prazer! Meu nome é *vpc-4nc-1gb-ubuntu-20-04-01*. 

Fica difícil saber que esse é o servidor que está rodando aquele site maroto em WordPress em meio a tantos outros que você tem!!! Que tal atribuir um nome mais simpático para facilitar a identificação no terminal e em sistemas de log centralizados? E isso pode salvar um emprego (me pergunte como depois).

Para essa missão, iremos recorrer ao comando `hostnamectl`. Sua sintaxe segue abaixo:

    $ sudo hostnamectl set-hostname nome_da_vm

Fácil assim. Use um nome que ajude a identificar o propósito do servidor, como producao, vm_teste, app_teste, o nome do projeto, personagens da sua série preferida (se fizer sentido para a equipe, porque não?).

Você pode verificar algumas informações da VM digitando o comando sem parâmetros. Veja um exemplo da saída em uma simulação:

    $ hostnamectl
     Static hostname: servidor_web 
           Icon name: computer-vm
             Chassis: vm
          Machine ID: 449faa078e1974e6df4e57f67a676a2f
             Boot ID: 6d379b4fb4bcba7d351e6592c9647463
      Virtualization: kvm
    Operating System: Ubuntu 20.04.3 LTS
              Kernel: Linux 5.4.0-88-generic
        Architecture: x86-64

O hostname geralmente fica visivel o tempo todo no terminal, ao lado do nome do usuário:

    nome_usuario@servidor_web$


## Alterar o hostname manualmente

Confesso que o comando é um tanto grande para algo tão simples e é fácil de esquecê-lo. Podemos alterar o hostname editando diretamente um arquivo chamado `hostname` (ah vá) localizado no diretório `/etc`.

Abra-o no editor de texto e altere seu conteúdo com o nome que deseja:
    
    $ sudo nano /etc/hostname

Ou ainda, você pode alterar o conteúdo do arquivo sem precisar abrir o editor de texto:

    $ echo "servidor_web" | sudo tee /etc/hostname

Após essa alteração, é necessário reiniciar o servidor:

    $ sudo reboot

> ℹ️ O uso do comando `hostnameclt` elimina a necessidade de reiniciar o servidor.