
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

##### Após a instalação estar concluída verifique se o serviço do Apache foi iniciado com sucesso utilizando os seguintes comando:

 systemctl status apache2  



## Criar estrutura de diretórios
__________________________________________________________________

1º - Criamos o diretório onde ficarão os arquivos do nosso site  

  `sudo mkdir /var/www/nomesite`  

2º - Alteramos a propriedade do diretório criado do ROOT para nosso usuário para que possamos modificar os arquivos.  

  `sudo chown -R $USER:$USER /var/www/nomesite`  

 _Obs: A variável `$USER` representa o usuário o qual você está logado atualmente._  
 
3º - Alteraremos também as permissões do diretório raiz onde ficarão os arquivos web.  

  `sudo chmod -R 755 /var/www`  
  
4º - Para finalizar esta etapa salve um arquivo HTML como `index.html` no diretório `/var/www/nomesite`  



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



    
        
    

