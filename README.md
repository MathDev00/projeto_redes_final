*Documentação - Projeto de Administração de Redes Final*

1. Introdução e Topologia de rede

O projeto consistiu em criar uma rede de computadores com os requisitos de serviços abaixo

| N | REQUISITOS |
| ------------- | ------------- |
|  RQ01  | Configure um servidor DHCP no ambiente Linux para atribuir endereços IP automaticamente aos dispositivos na rede. |
| RQ02  |Implante um servidor DNS para resolver nomes de domínio dentro da rede e configurar registros DNS como A, CNAME, MX  |
| RQ03| Configure e hospede um servidor web Apache ou Nginx para fornecer serviços de hospedagem de sites internos|
| RQ04| Implemente um servidor FTP (por exemplo, vsftpd) para permitir a transferência de arquivos na rede |
| RQ05| Configure um servidor NFS para compartilhar diretórios e arquivos entre máquinas na rede.|


Topologia de rede

[Notebook]
     |
[VirtualBox Host]
     |
[Switch Virtual do VirtualBox]
  /   |   \
VM1  VM2  VM3
     |    |  \
    [Cliente1, Cliente2, Cliente3]

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

Máquinas Virtuais

| Nome  | Serviços | Descrição|
| ------------- | ------------- | ------------- |
| VM1  | DHCP| Automatiza a atribuição de endereços IP e configurações de rede para dispositivos em uma rede |
| VM2  | DNS | Associando nomes de domínio a endereços IP correspondentes |
| VM3  | APACHE, FTP E NFS | Serviços de hospedagem web, transferência de arquivos e compartilhamento de arquivos em uma infraestrutura de rede |

2.1 Configuração do servidor DHCP





3. Testes e conclusão

| Ordem | VM | Descrição|
| ------------- | ------------- | ------------- |
| 1   | VM1    | Teste do synced_folder, checagem de compartilhamento das pastas, por meio da navegação das pastas e observação de hospedagem de sites. Teste de instalação do Apache, com comandos Linux na VM em execução. Teste do ping de comunicação entre as máquinas de mesma rede, com endereço de rede 192.168.56.1|
| 2     | VM2     | Teste de ping e instação do Mysql     |
| 3     | VM3    | Teste de configuração da rede pública. Comunicação com outras VM's e provimento de internet para as demais redes. Teste de mascaramento das redes |


