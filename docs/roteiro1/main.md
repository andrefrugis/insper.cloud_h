## Objetivo

Este Roteiro tem o objetivo a documentação e implementação de conceitos sobre uma plataforma de gerenciamento de hardware

## Montagem do Roteiro



### Tarefa 1

Instalando o MAAS:

<!-- termynal -->

``` bash
sudo snap install maas --channel=3.5/Stable
```

![Tela do Dashboard do MAAS](./maas.png)
 caption
Dashboard do MAAS


Conforme ilustrado acima, a tela inicial do MAAS apresenta um dashboard com informações sobre o estado atual dos servidores gerenciados. O dashboard é composto por diversos painéis, cada um exibindo informações sobre um aspecto específico do ambiente gerenciado. Os painéis podem ser configurados e personalizados de acordo com as necessidades do usuário.

### 1. Verificar se está funcionando e se o status está ativo.

![Tela do Dashboard do MAAS](./1.png)


### 2.Verificar acessibilidade na própria máquina: 
![Tela do Dashboard do MAAS](./2.png)

O comando: psql -U cloud -h 172.16.0.4 tasks. Faz o seguinte:
psql: Inicia o cliente interativo do PostgreSQL.
-U cloud: Específica o usuário do banco de dados, que no caso é cloud.
-h 172.16.0.4: Define o host (endereço IP) do servidor PostgreSQL ao qual você deseja se conectar. Neste caso, a conexão será feita para o IP 172.16.0.4, que pode ser um outro servidor na rede ou até mesmo o próprio servidor se esse for o IP dele.
tasks: Define o nome do banco de dados ao qual o usuário cloud tentará se conectar.
Esse código foi executado dentro do Server1.
Abaixo uma imagem da conexão bem sucedida: 


### 3. Acessibilidade a partir da máquina main: 
![Tela do Dashboard do MAAS](./3.png)
 
Usando o mesmo comando para verificar a conexão interna, porém agora a partir da minha máquina main. 
Instalei o client na main usando o comando:
sudo apt update && sudo apt install postgresql-client -y


### 4. Porta em que o serviço está funcionando:
![Tela do Dashboard do MAAS](./4.png)
 
Ao executar o nmap. Foi conferido que o serviço está rodando na porta 5432:
5432/tcp open postgresql


### Tarefa 2

### 1.Do Dashboard do **MAAS** com as máquinas.
![Tela do Dashboard do MAAS](./5.png)

### 2.Da aba de imagens, com as imagens sincronizadas
![Tela do Dashboard do MAAS](./6.png)

### 3. Cada máquina
### máquina 1:
![Tela do Dashboard do MAAS](./7.png)
![Tela do Dashboard do MAAS](./8.png)

### máquina 2:
![Tela do Dashboard do MAAS](./9.png)
![Tela do Dashboard do MAAS](./10.png)

### máquina 3:
![Tela do Dashboard do MAAS](./11.png)
![Tela do Dashboard do MAAS](./12.png)

### máquina 4:
![Tela do Dashboard do MAAS](./13.png)
![Tela do Dashboard do MAAS](./14.png)

### máquina 5:
![Tela do Dashboard do MAAS](./15.png)
![Tela do Dashboard do MAAS](./16.png)  

### Tarefa 3

### 1.máquinas e respectivos IPs
![Tela do Dashboard do MAAS](./17.png)  

### 2.Aplicação Django
![Tela do Dashboard do MAAS](./18.png)  

### 3. Explicação da aplicação manual do Django:
 
a. Deploy feito pelo dashboard do maas - deploy por linha de comando não estava funcionando

b. No ssh do server2 foi clonado o seguinte repositório: 

git clone https://github.com/raulikeda/tasks.git

c. dentro do diretorio tasks. Foi feita a instalação

./install.sh 

d. reboot do server2

sudo reboot

e. testando o acesso:

wget http://[IP server2]:8080/admin/

f. Ao testar o acesso obtivemos erros de conexão:

mudança no etc/hosts

172.16.0.4 server1 (onde estava instalado o postgres)

g. Tunel ssh:

conectanmos no maas utilizando: ssh cloud@10.103.0.X -L 8001:[IP server2]:8080

h. acesso no django feito: 

user: cloud

senha: cloud


Exemplo de diagrama

```mermaid
architecture-beta
    group api(cloud)[API]

    service db(database)[Database] in api
    service disk1(disk)[Storage] in api
    service disk2(disk)[Storage] in api
    service server(server)[Server] in api

    db:L -- R:server
    disk1:T -- B:server
    disk2:T -- B:db
```

[Mermaid](https://mermaid.js.org/syntax/architecture.html){:target="_blank"}

## Questionário, Projeto ou Plano

Esse seção deve ser preenchida apenas se houver demanda do roteiro.

## Discussões

Quais as dificuldades encontradas? O que foi mais fácil? O que foi mais difícil?

## Conclusão

O que foi possível concluir com a realização do roteiro?
