*Documentação - Projeto de Administração de Redes Final*

1. Introdução e Topologia de rede

O projeto consistiu em criar uma rede de computadores com os requisitos de serviços abaixo:

| N | REQUISITOS |
| ------------- | ------------- |
|  RQ01  | Configure um servidor DHCP no ambiente Linux para atribuir endereços IP automaticamente aos dispositivos na rede. |
| RQ02  |Implante um servidor DNS para resolver nomes de domínio dentro da rede e configurar registros DNS como A, CNAME, MX.  |
| RQ03| Configure e hospede um servidor web Apache ou Nginx para fornecer serviços de hospedagem de sites internos.|
| RQ04| Implemente um servidor FTP (por exemplo, vsftpd) para permitir a transferência de arquivos na rede.|
| RQ05| Configure um servidor NFS para compartilhar diretórios e arquivos entre máquinas na rede.|


1.1 Topologia de rede


![Texto Alternativo](REDES.png)



   
2. Execução e configuração dos container

Requisitos

| Nome  | Versão |
| ------------- | ------------- |
| Sistema Operacional  | Linux Mint 21.2 |
| Intereface de virtualização  | Vagrant 2.2.19  |
| Provedor  |  VirtualBox Versão 6.1.38 para Ubuntu |
| Fornecimento de serviços para as VM's  |  Docker 24.0.5 |

Comandos básicos

| Ordem | Comandos | Descrição|
| ------------- | ------------- | ------------- |
| 1    | vagrant up      | Geração da rede de computadores com Vagrantfile |
| 2    | docker run     | Fornecimento dos serviços solicitados por meio da conteinerização|

Com o vagrant up, as vm's serão criados e teremos acesso à rede de computadores.
Já com o docker run, é possível criar container a partir da imagem do serviço solicitado.
A execução da rede de computadores e o ofericimento dos serviços solicitados.

Máquinas Virtuais

| Nome  | Serviços | Descrição|
| ------------- | ------------- | ------------- |
| VM1  | DHCP| Automatiza a atribuição de endereços IP e configurações de rede para dispositivos em uma rede.|
| VM2  | DNS | Associando nomes de domínio a endereços IP correspondentes. |
| VM3  | APACHE, FTP E NFS | Serviços de hospedagem web, transferência de arquivos e compartilhamento de arquivos em uma infraestrutura de rede. |

2.1 Configuração do servidor DHCP

Observação: exemplo base, adaptado durante a execução

Arquivo responsavel por determinar a configuração dos IP's automaticamente para dispositivos de redes. Definir a lógica de atribuição, minutagem
e outras relacionadas à configuração DHCP.

```
ddns-update-style none;
default-lease-time 600;
max-lease-time 7200;
authoritative;
subnet 192.168.1.0 netmask 255.255.255.0
{
   range 192.168.1.100 192.168.1.200;
   option routers 192.168.1.2;
   option domain-name "minhaempresa";
   option domain-name-servers 192.168.1.2;
   option broadcast-address 192.168.1.255;
}
```
 
 2.1.1
 
 default-lease-time e max-lease-tim e -> controle de tempo das concessões;

 2.1.2

 subnet e netmask -> define IP e mascara


3. Testes e conclusão

| Ordem | VM | Descrição|
| ------------- | ------------- | ------------- |
| 1   | Todas as VM's  | Teste da instalação do docker, com intuito de checar a possibilidade de fornecer os serviços por meio do container.|
| 2     | Todas as VM's | Uso do docker ps para checagem de execução dos container, a fim de testar posteriormente os serviços.|
| 3     | VM1  | Teste de funcionamento do "dhcp.config", responsável pelo endereço de rede fornecido pelo serviço.|
| 4     | VM2  | Teste de funcionamento para verificar qual o enderço IP do gateway "ip r" e para avaliar a conectividade entre os equipamentos e verificar problemas de conexão com a Internet "ping -c (IP)".|
| 5     | VM3  | Teste de funcionamento para verificar a versão instalada de seu servidor web Apache "apache2 -V" que mostra todos os dados do servidor Apache, como a versão, a data de criação e dados em geral.|
| 6     | VM3  | Para testar o protocolo de rede para a transmissão de arquivos entre computadores (FTP), usamos apenas o "status" para mostrar o status atual da conexão.|
| 7     | VM3  | Teste de verificação para mostrar que o NFS apareça que está em execução "showmount -e hostname"|





