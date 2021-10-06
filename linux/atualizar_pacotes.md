# 📦 Atualizar os pacotes do Linux

Manter o sistema operacional e programas atualizados é uma prática importante para manter a segurança de todo o conjunto.

No mundo linux, felizmente, as atualizações são frequentes. Algumas distribuições disponibilizam semanalmente correções de bugs e updates de segurança.

Nas distribuições baseadas no Debian (como o Ubuntu) fazer atualização dos pacotes é tão fácil quanto contar até dois. Duvida?

1️⃣ Atualize a lista de pacotes com o comando abaixo:

    $ sudo apt update

Ao final ele já informa se tem ou não atualizações disponíveis:

    $ sudo apt update
    [...]                       
    Reading package lists... Done
    Building dependency tree       
    Reading state information... Done
    5 packages can be upgraded. Run 'apt list --upgradable' to see them.

2️⃣ Faça a instalação das atualizações:

    $ sudo apt dist-upgrade

Confirme que deseja atualizar pressionando a tecla *enter*. Se nem quiser ter esse trabalho, acrescente o parâmetro `-y` no final do comando:

    $ sudo apt dist-upgrade -y

> ℹ️ Muitas vezes pacotes adicionais são instalados para que um programa possa funcionar. Portanto é aconselhavel **não** utilizar o parâmetro `-y` para que você possa conferir o que será instalado e evitar problemas.

É importante verificar com frequência se tem atualizações disponíveis e aplicá-las assim que possível. 

> 🚨 Uma atualização pode fazer com que algum recurso ou serviço pare de funcionar (principalmente quando muda a versão principal do pacote, como da 2.x para 3.x), então é sempre bom testar antes de fazer, principalmente em ambiente de produção.

## Atualização do kernel linux

Quando a distribuição disponibiliza uma atualização do kernel linux, ele também é instalado pelo comando `apt dist-upgrade`. Observe na lista de pacotes a serem atualizados se algum kernel será instalado (geralmente o nome começa com `linux-image`).

Caso algum kernel novo seja instalado, é necessário reiniciar a VM para que ele seja utilizado.

## Removendo pacotes não utilizados e limpando o cache

Assim como manter os pacotes atualizados é importante para a segurança, remover os que não são mais utilizados também é. Em servidores devemos ter apenas o necessário para manter os serviços em funcionamento.

Felizmente também é muito fácil fazer essa limpeza. O parâmetro `autoremove` do comando `apt` irá remover todos os pacotes que não são mais necessários:

    $ sudo apt autoremove

Enquanto que o parâmetro `autoclean` apaga do disco os instaladores de pacotes que por ventura ficaram armazenados.

    $ sudo apt autoclean

> ℹ️ O `autoremove` também deleta os *kernels* mais antigos (que por sinal ocupam um espaço razoável no disco).

## Um pouco mais sobre o APT

O comando `apt` (ou `apt-get` para os mais antigos) é um gerenciador de pacotes originado no Debian. Ele facilita bastante a tarefa de instalar (`apt install`) e remover (`apt remove`) programas. Além disso, é possível pesquisar por pacotes (`apt-cache search`) quando não sabemos o nome correto para instalação.

Certamente iremos utiliza-lo em outro guia para instalar alguns programas, como o trio Apache2, MySQL e PHP, necessários para o funcionamento do WordPress e outros sistemas desenvolvidos em PHP.