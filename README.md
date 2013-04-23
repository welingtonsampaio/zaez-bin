# Zaez Bin - 0.0.2
Arquivos de auxilio para facilitar operações de rotina
+ [Requisitos](#requisitos)
+ [Instalação](#instalao)
+ [VirtualHost](#virtualhost)
+ [My Clone](#my-clone)

***

## Requisitos

+ [Ruby](http://www.ruby-lang.org/)
+ [Thor](https://github.com/wycats/thor)

***

## Instalação

Por costume e melhor manuseio dos arquivos e projetos mantemos tudo no diretorio do usuário na pasta `Development`
```console
mkdir ~/Development
git clone git@github.com:welingtonsampaio/zaez-bin.git ~/Development/bin
chmod +x ~/Development/bin/*
echo 'export PATH="$HOME/Development/bin:$PATH"' >> ~/.bash_profile
```

***

## Virtualhost

Manipula vhost do apache para manipulação de hosts na maquina

### new
Adiciona um novo vhost a biblioteca deve ser usado com usuário root `sudo`
```console
sudo virtualhost new --path="path-da-pasta" --url="url-desejada" --name="nome_para_manipulacao"
```

#### Opções
+  `--path="path-da-pasta"` ou `-p="path-da-pasta"`: Caminho absoluto para a pasta que contém o projeto web, `.` para a pasta atual
+  `--url="url-desejada"` ou `-u="url-desejada"`: Url para acessar pelo browser o vhost
+  `--name="nome_para_manipulacao"` ou `-n="nome_para_manipulacao"`: Nome para manipulação e/ou identificação do virtual host

#### Utilização com de forma reduzida
```console
sudo virtualhost new -p="path-da-pasta" -u="url-desejada" -n="nome_para_manipulacao"
```

#### Utilização sem paramentros
```console
sudo virtualhost new
Entre com o caminho absoluto da pasta dos arquivos: .
Entre com a url desejada: site.zaez.net
```
O resultado disso será:
```console
      append  /etc/hosts
      append  /private/etc/apache2/extra/httpd-vhosts.conf
         run  apachectl restart from "."
-------------------------------------------------------------------------------------
Conteudo inserido no arquivo: /etc/hosts


##<virtualhost site_zaez_net>
127.0.0.1  site.zaez.net
##</virtualhost site_zaez_net>
-------------------------------------------------------------------------------------
Conteudo inserido no arquivo: /private/etc/apache2/extra/httpd-vhosts.conf


##<virtualhost site_zaez_net>

<VirtualHost *:80>
	DocumentRoot "/Users/welington/Development/bin"
	ServerName site.zaez.net

	<Directory /Users/welington/Development/bin>
		AllowOverride All
		Order allow,deny
		Allow from all
	</Directory>
</VirtualHost>

##</virtualhost site_zaez_net>
-------------------------------------------------------------------------------------
Para manutencoes/remover, utilize o nome: site_zaez_net
Finish
```

***

### list
Lista todos os vhosts criados pela "virtualhost"
```console
virtualhost list
```
A saida no terminal será parecida com:
```console
+----------------------------------------
| 1. site1_com
| 2. site2_com
| 3. site3_com
+----------------------------------------
```

### clean
Remove definitivamente o vhost dos arquivos, deve ser usado com usuário root `sudo`
```console
sudo virtualhost clean NAME
```
Onde "NAME" é o nome de manipulção gerado pelo virtualhost. Exemplo: `site1_com`
Caso existe um vhost para `site1_com` para excluí-lo o comando seria:
```console
sudo virtualhost clean site1_com
```
e a saída do terminal seria algo como:
```console
        gsub  /etc/hosts
        gsub  /private/etc/apache2/extra/httpd-vhosts.conf
Files cleaning, for name content: site1_com
Finish.
```

### doctor
Ele examina e descomenta a linha de configuracao ao arquivo do apache, deve ser usado com usuário root `sudo`
```console
sudo virtualhost doctor
```
a saída no terminal será algo como:
```console
        gsub  /etc/apache2/httpd.conf
         run  apachectl restart from "."
```

### default
Imprime no console as configurações default para utilização do virtualhost
```console
virtualhost default
```
a saída será algo como:
```console
+-----------------------------------------------------------------------------------------------------
| Arquivo de configuracao do apache.........: /etc/apache2/httpd.conf
| Arquivo de configuracao dos virtuais hosts: /private/etc/apache2/extra/httpd-vhosts.conf
| Arquivo de configuracao dos ips dos hosts.: /etc/hosts
+-----------------------------------------------------------------------------------------------------
```
> Essas configurações foram feitas a princípio para ser utilizado no Mac OS X 10.8 (Montain Lion), porém o arquivo pode ser modificado para ser trabalhar em qualquer OS
Veja o local de edição de cada configuração:
+ [Arquivo de configuracao do apache](https://github.com/welingtonsampaio/zaez-bin/blob/master/virtualhost#L13)
+ [Arquivo de configuracao dos virtuais hosts](https://github.com/welingtonsampaio/zaez-bin/blob/master/virtualhost#L9)
+ [Arquivo de configuracao dos ips dos hosts](https://github.com/welingtonsampaio/zaez-bin/blob/master/virtualhost#L17)

***

## My Clone
-- em desenvolvimento --

# Licensa 
The MIT License (MIT)

Copyright (c) 2013 Zaez Soluções em Tecnologia

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.