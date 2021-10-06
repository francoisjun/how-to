# Configuração inicial de uma VM

It's alive!!!

Sua VM está rodando. A mão chega a coçar para instalar aquele WordPress. No entanto, algumas configurações iniciais são necessárias para deixar o ambiente mais seguro e consistente. Se você não sabe por onde começar, esse roteiro vai te guiar nas configurações básicas iniciais.

Pensando no iniciante da área de TI, tentarei utilizar termos menos técnicos e darei uma breve explicação do que será feito e a razão para tal, ficando como tarefinha de casa a pesquisa mais profunda sobre o tema e dos comandos utilizados. 

É importante que o profissional não trabalhe de forma mecânica (que apenas segue um passo a passo), mas que entenda o que está sendo feito em cada etapa e assim consiga encontrar soluções quando as coisas derem errado (passo a passo não é garantia de sucesso e certamente algo dará errado em algum momento. Acostume-se!).

Let's go?

## Roteiro

> Esse roteiro é baseado na configuração de uma VM da Digital Ocean com o sistema Ubuntu 20.04 LTS. Em outras distribuições ou serviços, alguns comandos podem ser diferentes.

1. 🤦 [Crie o seu usuário e ingresse no grupo dos sudoers](https://github.com/francoisjun/how-to/blob/main/linux/criar_usuario.md)
2. 🔑 [Crie e copie sua chave SSH para a VM](https://github.com/francoisjun/how-to/blob/main/linux/criar_chave_ssh.md)
3. 🖥 [Configure o servidor SSH](https://github.com/francoisjun/how-to/blob/main/linux/configurar_ssh.md)
4. 🔖 [Altere o nome da VM (hostname)](https://github.com/francoisjun/how-to/blob/main/linux/configurar_hostname.md)
5. ⏱ [Ajuste a hora do sistema (timezone)](https://github.com/francoisjun/how-to/blob/main/linux/configurar_timezone.md)
6. 💾 [Habilite a memória SWAP](https://github.com/francoisjun/how-to/blob/main/linux/habilitar_swap.md)
7. 📦 [Atualize os pacotes do sistema](https://github.com/francoisjun/how-to/blob/main/linux/atualizar_pacotes.md)
8. 🔥 [Configure o Firewall](https://github.com/francoisjun/how-to/blob/main/linux/configurar_firewall.md)
