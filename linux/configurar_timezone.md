# ⏱ Configurar a timezone

Eis que você verificou no log que Joãozinho reiniciou o servidor mysql às 20:31, mas ainda são 17h! Será que Joãozinho aprendeu a fazer viagem no tempo? Ou será que o servidor está com o fuso horário errado? Vamos descobrir.

Com o comando `date` podemos checar rapidamente a data, hora e o fuso configurado no sistema:

    $ date
    Tue Oct  5 13:32:53 -03 2021

> O `-03` indica que estamos no fuso de 3h a menos em relação ao *Universal Time Coordinated (UTC)*.

Isso é util para saber as horas no terminal, mas podemos usar o comando `timedateclt` para mais detalhes:

    $ timedatectl 
                   Local time: Tue 2021-10-05 13:35:05 -03
               Universal time: Tue 2021-10-05 16:35:05 UTC
                     RTC time: Tue 2021-10-05 16:35:06    
                    Time zone: America/Recife (-03, -0300)
    System clock synchronized: yes                        
                  NTP service: active                     
              RTC in local TZ: no   

Observe que a timezone do servidor está em `America/Recife (-03, -0300)`, mas por padrão ele vem em `UTC (0)`.

Para alterar o fuso horário, utilize o comando `timedatectl` com a seguinte sintaxe:

    $ sudo timedatectl set-timezone "America/Recife"

Claro que isso se aplica para quem mora nessa região. Para verificar a lista de timezones disponíveis, utilize o comando abaixo: 

    $ timedatectl list-timezones

Ajustar corretamente a hora do servidor é importante principalmente em auditorias pois a data e hora registrada nos logs vão corresponder ao horário em que a ação foi executada.

Outra situação em que isso pode impactar é no uso de sistemas de autenticação centralizados (como Active Directory) em quem uma divergência no horário dos servidores pode impedir a autenticação do usuário.