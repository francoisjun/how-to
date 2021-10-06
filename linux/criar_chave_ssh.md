# 🔑 Criando uma chave SSH

Em miúdos, chave SSH consiste em um par de arquivos: a chave pública e privada. Elas são geradas por meio de algorítmos de criptografia assimétrica. A chave privada é como se fosse a senha e deve ser protegida com unhas e dentes. A chave pública pode ser distribuída livremente sem comprometer a segurança.

Esse par de chaves geralmente fica armazenado no seu computador em um diretório oculto chamado `.ssh` na raiz do seu diretório `home`. Qualquer informação criptografada com a chave pública só pode ser descriptografada com a sua chave privada. 

Ao cadastrar sua chave pública em serviços como o github ou no servidor ssh da sua VM, você tem acesso a eles sem precisar informar senha, desde que feito do computador que possui a chave privada. Portanto se alguem tiver acesso à sua chave privada, ela pode acessar qualquer serviço na qual sua chave pública foi cadastrada. Se não ficou claro: **CUIDE BEM DA SUA CHAVE PRIVADA**.

## Criando a chave SSH

O jeito mais simples é usando o comando `ssh-keygen` sem nenhum parâmetro:

    $ ssh-keygen

O comando vai perguntar o nome do arquivo de saída e já dá uma sugestão. Você deve aceitá-la pressionando a tecla *enter* caso não possua nenhuma chave (caso possua, faça backup de sua chave antiga antes de executar o comando). Em seguinda ele pede uma senha mas recomendo deixá-la vazia para nosso propósito (apenas pressione *enter*). Abaixo a saída do comando em uma simulação:

    $ ssh-keygen         
    Generating public/private rsa key pair.
    Enter file in which to save the key (/home/nome_usuario/.ssh/id_rsa): 
    Enter passphrase (empty for no passphrase): 
    Enter same passphrase again: 
    Your identification has been saved in id_rsa.
    Your public key has been saved in id_rsa.pub.
    The key fingerprint is:
    SHA256:+YW1vkur/B8l91oX0H7t//1aIzILDoqm5a0i2Tnkkzg nome_usuario@hostname_da_maquina
    The key's randomart image is:
    +---[RSA 3072]----+
    |                 |
    |              .  |
    |             . . |
    |         . . .o .|
    |     .  S ..o. +*|
    |.   E .   .o. .+*|
    |   . + . .. o . *|
    |++*.o o ...o . =+|
    |=oo=.  . .oo*++.B|
    +----[SHA256]-----+

Serão gerados dentro do diretório `/home/nome_usuario/.ssh` os arquivos `id_rsa` com a chave privada e `id_rsa.pub` com a chave pública.

Podemos incrementar o comando com alguns parâmetros, como no exemplo abaixo:

    $ ssh-keygen -t rsa -b 4096 -f /home/nome_usuario/minha_chave -C 'nome_usuario@meu_pc'

onde:

- `-t rsa` é o sistema de criptografia;
- `-b 4096` é o tamanho de bits da chave (alguns serviços exigem um tamanho mínimo);
- `-f /home/nome_usuario/minha_chave` é o nome do arquivo de saída. Será gerado o arquivo `minha_chave` com a chave privada e `minha_chave.pub` com a chave pública;
- `-C 'nome_usuario@meu_pc'` é um comentário no final da chave que pode ajudar a identificar o proprietário ou propósito da chave.

## Copiando a chave pública para um servidor remoto

Esse processo fica simples com o comando abaixo:

    $ ssh-copy-id ~/.ssh/id_rsa nome_usuario@ip_do_servidor

Esse comando fará a cópia da sua chave pública para o servidor remoto, no diretório do usuário informado. 

Você também pode fazer esse processo manualmente mas é um pouco mais trabalhoso. 
Primeiro copie o conteúdo da sua chave pública. Utilize o comando `cat` para imprimir o conteúdo do arquivo diretamente no terminal:

    $ cat ~/.ssh/id_rsa.pub

A saída do comando será algo pareciso com isto:

    ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDIE1DcdKGE1BX1vXTAaN7P/7B+Ey8Hdj0283bWYiS8bdgwDwqekAmQy2Uix1fG1dZnm75HxLKGeo27sNhB2GfVPA5E/PdmNCJ5wWSik4SBkDlE8/F7sgL3WgQbAdkrjY/GByTarew7HzbiffiSUlgHgutdQi9o+lJHb21ZX5ZIwcdz7N9PohlgbJVlFLj0lmlLPZV1/KgCUZvwEoMAugmEns0lBzYe6LRKrOm4GlyR5I4alIWK1YhCeWg0Xv44nF9kAnKK+pjMnyh5kAZbEOP4kN/u9K7SVutKyd+5gM9PyYXlXbrRMsXSYc9fUWaxdOgSFcBiI6mQHIYiGKbNS+2oROLWCViVeApr+4b9EFEBL9H+itU1rl17L3mBOj+ZHrRa+1nQhIzfkWd0o2AvuXefYDJckhJ4kzZcap5bSU0MAvooQFyezujZtExhp+5KUBFJeRpjZ57roQUBTF5tHLJoFhw7vSqN7T5JWosLjDxtObrgRIVlDvMjB8vA9cEe3k0= nome_usuario@meu_pc

Selecione todo esse conteúdo e copie. Agora acesse o servidor remoto com seu usuário. Vá para o diretório `.ssh`:

    $ cd .ssh

Caso o diretório não exista, você deve criá-lo com o comando abaixo:

    $ mkdir .ssh

Uma vez dentro do diretório, vamos editar um arquivo chamado `authorized_keys`:

    $ nano authorized_keys

> ℹ️ Quando tentamos editar um arquivo que não existe, o `nano` abre um arquivo novo. Na hora de salvar ele usará o nome do arquivo que informamos ao abrí-lo.

Simplesmente cole o conteúdo de sua chave pública dentro do arquivo. Caso já exista outra chave, deixe uma linha em branco entre elas.
