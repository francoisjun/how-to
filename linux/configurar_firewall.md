# 🔥 Configurar o Firewall

Configurar o Firewall não é uma tarefa muito fácil pois você precisa definir muito bem as regras de acesso. Se você pesquisar pelo iptables (Firewall padrão do linux) vai ver que a sintaxe é bem complexa. Felizmente temos uma ferramenta que facilita esse trabalho: o `UFW (Uncomplicated Firewall)`. 

> ℹ️ Caso o comando não esteja disponível na sua distro linux, você pode instalar com o comando `sudo apt install ufw`

E tudo começa com a política padrão de segurança: bloquear tudo e liberar à medida que precisa ou liberar tudo e bloquear só o que não deseja que funcione?

## Definindo a política padrão

Na premissa do servidor que deve rodar apenas o necessário, é muito mais fácil e seguro bloquear tudo e liberar apenas o que precisa. 

Portanto vamos começar definindo essa política padrão:

    $ sudo ufw default deny incoming
    $ sudo ufw default allow outgoing

Na primeira linha estamos bloqueando todas as conexões de entrada e na segunda liberando todas as de saída.

Mas um servidor precisa aceitar conexões de entrada, não é mesmo? A partir de agora iremos liberar apenas as portas dos serviços que queremos expor na internet. A primeira delas é o SSH que configuramos anteriormente (caso não, dê uma olhada [nesse guia](https://github.com/francoisjun/how-to/blob/main/linux/configurar_ssh.md)).

## Liberando portas

Lembra quando falei que a porta padrão do SSH é a 22 e todo mundo sabe disso? Pois bem, outros serviços também possuem portas padrões, como a porta 80 para HTTP, 443 para HTTPS, 3306 para o MySQL, etc.

Sendo assim, não precisamos especificar a porta. No lugar, podemos informar o serviço:

    $ sudo ufw allow ssh

No comando acima, estamos liberando a conexão SSH em nosso servidor. Caso você tenha customizado a porta desse serviço, será necessário informá-la como abaixo:

    $ sudo ufw allow 2002

Outras portas serão liberadas a medida que instalarmos novos serviços.

> 🚨 Em hipótese alguma ative o firewall sem antes liberar a porta do SSH. Caso contrário você não terá mais acesso ao servidor.

## Ativando o firewall

Agora que temos as regras definidas, vamos ativar o firewall:
    
    $ sudo ufw enable

Aparecerá uma mensagem informando que as conexões SSH ativas serão interrompidas. Como já liberamos a porta desse serviço, podemos prosseguir sem problemas. Digite a tecla `y` e, em seguida, `enter`:

    Command may disrupt existing ssh connections. Proceed with operation (y|n)? y
    Firewall is active and enabled on system startup

## Verificando o status do firewall

Para ver as regras ativas, use o comando a seguir:

    $sudo ufw status verbose

Segue um exemplo da saída do comando:

    Status: active
    Logging: on (low)
    Default: deny (incoming), allow (outgoing), disabled (routed)
    New profiles: skip

    To                         Action      From
    --                         ------      ----
    22/tcp                     ALLOW IN    Anywhere                  
    22/tcp (v6)                ALLOW IN    Anywhere (v6)  

## Outras regras de firewall

Temos aqui uma ferramenta fantástica onde podemos ser bastante específicos no que queremos, como por exemplo liberar o SSH apenas para um IP específico, bloquear conexões de um IP que está tentando acessar seu servidor (malditos hackers), definir limites de tráfego, definir rotas, etc.

Como foge um pouco do escopo desse guia básico, deixo aqui um tutorial mais completo da Digital Ocean: [How To Set Up a Firewall with UFW on Ubuntu 20.04](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-with-ufw-on-ubuntu-20-04)