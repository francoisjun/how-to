# 💾 Habilitar a memória SWAP

Os planos mais básicos de computação em nuvem disponibilizam cerca de 1GB de memória RAM. Isso pode ser suficiente para algumas aplicações, mas dependendo da quantidade de usuários ou de recursos da aplicação, rapidamente essa memória será ocupada. 

Com a falta de memória, o sistema operacional trava e será necessário reiniciar a VM por força bruta, o que pode provocar corrompimento e perda de dados. Para contornar esse problema, é bastante aconselhável habilitar a memória SWAP.

A SWAP é uma memória RAM virtual. Isso é possível através da utilização do armazenamento de disco. Quando a memória RAM começa a chegar perto do limite, o sistema operacional move os dados em cache da memória RAM para a SWAP (é um pouco mais complexo que isso e o método varia dependendo do SO, mas para facilitar o entendimento é o suficiente), permitindo que o sistema continue operante.

Primeiramente devemos verificar o quanto de memória temos disponível no sistema. Para isso, utilize o comando abaixo:

    $ free -h

onde:
- `-h` converte os valores de bytes para uma grandeza mais legível (Kilo, Mega ou Gigabyte).

Observe a saída do comando:

    $ free -h
            total        used        free      shared  buff/cache   available
    Mem:    981Mi       191Mi       125Mi       0.0Ki       663Mi       633Mi
    Swap:      0B          0B          0B


Na primeira `Mem` temos informações da memória RAM e na linha abaixo da memória SWAP. Observe que ela está zerada, indicando que está desabilitada.

A memória SWAP pode ser criada como uma partição especial no disco ou em arquivo. Iremos utilizar o segundo método.

Vamos começar criando um arquivo do tamanho que queremos para memória SWAP com o comando `fallocate`:

    $ sudo fallocate -l 2GB /swapfile

onde:

- `-l 2GB` é o tamanho do arquivo;
- `/swapfile` é o nome do arquivo. Neste caso ele será armazenado no diretório raiz `/`.

Nesse exemplo criaremos uma SWAP com o dobro da memória RAM. Você precisa monitorar os recursos do sistema para dimencionar melhor esses valores. Lembre-se que a SWAP oculpa espaço no disco.

Uma vez criado o arquivo, devemos alterar as permissões de acesso conforme segue:

    $ sudo chmod 600 /swapfile

Em sequencia, devemos preparar o arquivo para funcionar como SWAP. Fazemos isso com o comando abaixo:

    $ sudo mkswap /swapfile

Por fim, vamos habilitar a SWAP com este comando:

    $ sudo swapon /swapfile

Caso precise desabilitar a memória SWAP, use o comando:

    $ sudo swapoff /swapfile

Verifique agora com o comando `free` que a memória SWAP está habilitada:

    $ free -h
            total        used        free      shared  buff/cache   available
    Mem:    981Mi       186Mi       131Mi       0.0Ki       663Mi       638Mi
    Swap:   1.9Gi          0B       1.9Gi


## Habilitando a memória SWAP permanentemente

Quando a VM for reiniciada, a memória SWAP estará desabilitada, apensar do arquivo permanecer no disco. Para contornar essa característica devemos adicionar no arquivo `fstab` as instruções para habilitar a memória SWAP durante o boot.

Abra o arquivo no editor de texto:

    $ sudo nano /etc/fstab

 e acrescente a linha abaixo no final do arquivo:

    /swapfile none swap sw 0 0

Como alternativa, você pode adicionar essa linha diretamente sem precisar abrir o editor de arquivos com o comando abaixo:

    $ echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab

> 🚨 Muito cuidado ao manipular o arquivo `fstab`. Ele contém as instruções de carregamento das partições do disco. Caso altere algo inapropriadamente, o sistema operacional pode não ser carregado.