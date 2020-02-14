
## Configurando configurando hosts virtuais
_____________________________________________  

##### 1º - No /etc/apache2/ existem dois diretórios que utilizaremos para configurar os nossos hosts virtuais para que possamos hospedar varios sites no nosso servidor. Sendo eles:  

    *sites-available*  -> Diretório onde ficará disponível o arquivo de configuração do host de cada site.  
    *sites-enable*     -> Diretório onde ficará os arquivos de configuração dos hosts ativos.  

##### 2º - No diretório 'sites-available' existe um arquivo chamado "000-default.conf" o qual iremos fazer uma cópia com o nome do nosso site:  

    cp 000-default.conf nomesite.conf  

##### 3º - Logo após editamos o novo arquivo com previlégios de ROOT:  

    sudo nano nomesite.conf
    
###### Agora o deixaremos da seguite forma e depois salvamos:  

   `<VirtualHost *:80>`  
      &ensp;&ensp;&ensp;&ensp;`ServerAdmin admin@nomesite.com`  
      &ensp;&ensp;&ensp;&ensp;`ServerName nomesite.com`  
      &ensp;&ensp;&ensp;&ensp;`ServerAlias www.nomesite.com`  
      &ensp;&ensp;&ensp;&ensp;`DocumentRoot /var/www/nomesite`  
      &ensp;&ensp;&ensp;&ensp;`ErrorLog ${APACHE_LOG_DIR}/error.log`  
      &ensp;&ensp;&ensp;&ensp;`CustomLog ${APACHE_LOG_DIR}/access.log combined`  
    `</VirtualHost>`  
   
##### 4º - Para ativar nosso hosts criado usamos o seguinte comando:  

    `sudo a2ensite nomesite.conf`  
   
Depois desabilite o site padrão definido em '000-default.conf':  

    `sudo a2dissite 000-default.conf`  
    
##### 5º - Após concluir, reinicie o servidor apache:  

    `sudo systemctl restart apache2`  
 
 
 
## Configurando o arquivo de hosts local
__________________________________________  


Para que possamos utilizar o domínio *nomesite.com* ou *www.nomesite.com* precisamos para o endereço IP da nossa placa de rede. Para isso editamos o arquivo `/etc/hosts` deixando-o da seguinte forma:  

    `127.0.0.1  localhost  
     127.0.0.1  MeuPC  
     xxx.xxx.xxx.xxx  nomesite.com  
     xxx.xxx.xxx.xxx  www.nomesite.com`  
    
_Obs: Substitua o 'xxx.xxx.xxx.xxx' pelo o endereço IP da sua placa de rede._  

Agora salve o arquivo e tente acessar seu site digitando este domínio na barra do seu navegador.  
