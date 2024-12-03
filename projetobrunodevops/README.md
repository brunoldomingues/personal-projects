### DOCUMENTAÇÃO - DESAFIO DEVOPS BRY ###

Esta documentação tem por objetivo demonstrar a estrutura de código para serviço whoami, Zabbix, Grafana e Nginx.

### Premissas:

1 - O projeto foi desenvolvido para Linux;

2 - Para execução do código, usuário deverá ter privilégios 'root' (sudo -i);

3 - Baixe o projeto no diretório ' /tmp/projetobrunodevops '

4 - Não foi possível criar um subdominio para o projeto, portanto, o mesmo é executado localmente (localhost);


### Estrutura:

Os diretórios e códigos estão organizados da seguinte maneira:

Ansible: contendo os arquivos de 'host.yml' (inventário) e 'site.yml' (playbook) e as roles;
    - Roles:
            As roles de ansible para docker, grafana, nginx, postegresql, whoami e zabbix. Cada uma contem a seguinte estrutura de diretórios:

            - files: contendo os arquivos 'default' (onde necessário);
            - tasks: as 'tasks' com seus respectivos arquivos 'main.yml' ;
            - templates: templates de arquivos, caso necessário;

Docker: contendo o 'docker-compose.yml', que fará a criação dos containers;

Nginx: durante a execução do ansible, será criado o arquivo de configuração do nginx com ingress (nginx.conf);

questoes-teoricas: arquivo com as respostas para o questionário do desafio;

README.md : Este arquivo, contendo a documentação do projeto.


### Sobre o projeto

Esse projeto foi desenvolvido no intuíto de, a partir de um simples comando de ansible ('ansible-playbook -i host.yml site.yml'), fazer toda a configuração de um ambiente 'dockerizado' para as aplicações abaixo:

- whoami: Serviço docker HTTP que imprime a ID do container;
- Zabbix: Interface Web para para monitoramento e recebimento de alertas da esturura/ambiente;
- PostegreSQL: Banco de dados para o Zabbix;
- Grafana: Ambiente para visualização e monitoramento da estrutura através de dashboards e painéis; 
- Nginx: Atuando como proxy reverso, permitindo que os containers sejam acessados através de um único ponto de entrada na porta 80 (HTTP);


Todo código está devidamente comentado, tornando seu entendimento e funcionamento compreensível;

Ao final da execução do ansible, é criado um arquivo 'servicos_urls.txt' com as URLs de cada serviço e as credenciais para acesso. O usuário poderá acessar via web esses serviços;

### TEST VALIDATION

Dentro do diretório '/tmp/projetobrunodevops/ansible', deverá ser aberto o terminal e executado o comando abaixo:

-
``` bash
$ ansible-playbook -i host.yml site.yml 

```

O resultado deverá ser esse:

``` bash

PLAY [local] *******************************************************************

TASK [Gathering Facts] *********************************************************
ok: [local]

TASK [Criar o diretório do projeto] ********************************************
ok: [local]

TASK [Garantir a instalação do Docker] *****************************************
ok: [local]

TASK [Iniciar serviço Docker] **************************************************
ok: [local]

TASK [Verificar se o Docker está funcionando] **********************************
changed: [local]

TASK [Copiar arquivo docker-compose] *******************************************
changed: [local]

TASK [Garantir que o NGINX esteja configurado dentro do Docker] ****************
changed: [local]

TASK [Executar Docker Compose] *************************************************
changed: [local]

TASK [Criar arquivo de texto com endereços] ************************************
changed: [local]

PLAY RECAP *********************************************************************
local                      : ok=9    changed=5    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

```

O arquivo 'servicos_urls.txt' deverá conter:

Grafana: http://localhost:3000/login
usuário: admin | senha: admin

Zabbix Web: http://localhost:8081
usuário: Admin | senha: zabbix

Whoami: http://localhost:8082


### Considerações finais:

Este projeto tem como objetivo fornecer uma solução automatizada e de fácil implantação para ambientes 'dockerizados' com múltiplos serviços. Combinando as ferramentas e tecnologias Ansible e Docker, é possível criar uma infraestrutura robusta, simplificando a gestão e operação de containers. A configuração do nginx como proxy reverso centraliza o acesso a todos os serviços, proporcionando maior flexibilidade e controle.

Caso haja falha na execução ou duvidas, segue contato:

Email: brunoluizdomingues92@gmail.com
LinkedIn: https://www.linkedin.com/in/brunodomingues1/


