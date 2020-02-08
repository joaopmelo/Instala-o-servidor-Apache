
# Instalando o Servido Apache
_______________________________  

## Estrutura de arquivos de configuração do Apache

  /etc/apache2/  
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;|
               -`ports.conf`  
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;|
               -`apache.conf`  
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;|
               -`/sites-available`  
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;|
               -`/sites-enable`  

## Primeiro instale o apache utilizando os comandos abaixo:

 sudo apt-get install apache2

### Após a instalação estar concluída verifique se o serviço do Apache foi iniciado com sucesso utilizando os seguintes comando:

 systemctl status apache2


## Criar estrutura de diretórios
__________________________________________________________________

* Primeiro vamos criar o diretório onde ficarão os arquivos do nosso site  

`sudo mkdir /var/www/nomesite`  

* Agora vamos alterar a propriedade do diretório criado do ROOT para nosso usuário para que possamos modificar os arquivos.  

`sudo chown -R $USER:$USER /var/www/nomesite`  

 _Obs: A variável `$USER` representa o usuário o qual você está logado atualmente._  

## Configurando configurando hosts virtuais
_____________________________________________  

#### No /etc/apache2/ existem dois diretórios que utilizaremos para configurar os nossos hosts virtuais para que possamos hospedar varios sites no nosso servidor. Sendo eles:  

    * sites-available  - Diretório onde ficará disponível o arquivo de configuração do host de cada site.  
    * sites-enable     - Diretório onde ficará os arquivos de configuração dos hosts ativos.

#### No diretório sites-available existe um arquivo chamado "000-default.conf" o qual iremos fazer uma cópia com o nome do nosso site:  

    cp 000-default.conf nomesite.conf  

#### Logo após editamos o novo arquivo com previlégios de ROOT:  

    sudo nano nomesite.conf
    
#### Agora o deixaremos da seguite forma e depois salvamos:  

   `<VirtualHost *:80>`  
      &ensp;&ensp;&ensp;&ensp;`ServerAdmin admin@nomesite.com`  
      &ensp;&ensp;&ensp;&ensp;`ServerName nomesite.com`  
      &ensp;&ensp;&ensp;&ensp;`ServerAlias www.nomesite.com`  
      &ensp;&ensp;&ensp;&ensp;`DocumentRoot /var/www/nomesite`  
      &ensp;&ensp;&ensp;&ensp;`ErrorLog ${APACHE_LOG_DIR}/error.log`  
      &ensp;&ensp;&ensp;&ensp;`CustomLog ${APACHE_LOG_DIR}/access.log combined`  
    `</VirtualHost>`  
   

 


        
    

