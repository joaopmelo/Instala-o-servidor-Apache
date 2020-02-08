
# Instalando o Servido Apache

## Estrutura de arquivos de configuração do Apache

  `_/etc/apache2/_`
  
               `_ports.conf_`
               
               `_apache.conf_`
               
               `_/sites-available_`
               
               `_/sites-enable_`

## Primeiro instale o apache utilizando os comandos abaixo:

 sudo apt-get install apache2

### Após a instalação estar concluída verifique se o serviço do Apache foi iniciado com sucesso utilizando os seguintes comando:

 systemctl status apache2

## Configurando configurando hosts virtuais

### No /etc/apache2/ existem dois diret贸rios que utilizaremos para configurar os nossos hosts virtuais para que possamos hospedar varios sites no nosso servidor. Sendo eles:

    * sites-available  - Diretório onde ficará disponível o arquivo de configuração do host de cada site.
    * sites-enable     - Diretório onde ficará os arquivos de configuração dos hosts ativos.

## No diretório sites-available existe um arquivo chamado "000-default.conf" o qual iremos fazer uma cópia com o nome do nosso site:

    cp 000-default.conf nomesite.conf

### Logo após o editamos:

    sudo nano nomesite.conf
    
   


        
    

