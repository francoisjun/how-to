# Configuração inicial de uma VM

Ao criar uma nova VM você obtem acesso pelo usuário root. No entanto não é boa prática utilizar esse usuário a todo momento. Vamos iniciar as configurações adicionando um usuário para você chamar de seu!

Mas antes de começar a brincar no servidor remoto, crie uma chave SSH na sua máquina caso ainda não tenha.

## Roteiro

1. [Crie o seu usuário e ingresse no grupo dos sudoers](https://github.com/francoisjun/how-to/blob/main/linux/criar_usuario.md)
2. [Crie e copie sua chave SSH para a VM](https://github.com/francoisjun/how-to/blob/main/linux/criar_chave_ssh.md)
3. Configure o servidor SSH desativando o login do usuário root
4. Altere o nome da VM (hostname)
5. Ajuste a hora do sistema (timezone)
6. Habilite a memória SWAP
7. Atualize os pacotes do sistema
