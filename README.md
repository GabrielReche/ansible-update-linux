# Ansible Atualização de Pacotes

## Visão Geral
Este playbook Ansible foi desenvolvido para automatizar a atualização e o upgrade de pacotes nos sistemas gerenciados. Ele suporta tanto sistemas baseados em apt (como Debian e Ubuntu) quanto sistemas baseados em yum (como CentOS e Red Hat).


Neste playbook:

Verificação de atualizações disponíveis:

O playbook começa verificando se há atualizações disponíveis usando comandos específicos para apt e yum, dependendo do gerenciador de pacotes do sistema.
Atualização de pacotes:

Atualiza os pacotes disponíveis usando o apt ou yum, dependendo do sistema operacional.
Upgrade de pacotes:

Realiza o upgrade dos pacotes para a versão mais recente disponível. No caso do apt, o upgrade é para a distribuição (dist-upgrade), enquanto no yum, apenas os pacotes são atualizados, exceto o kernel.
Verificação da necessidade de reboot (apenas Debian/Ubuntu):

Verifica se há necessidade de reboot após o upgrade dos pacotes no caso de sistemas Debian/Ubuntu.
Exibição de informações e resultados:

Exibe informações detalhadas sobre as atualizações disponíveis, resultados das operações de atualização e upgrade, e se um reboot é necessário.
Notificação de reboot (apenas Debian/Ubuntu):

Caso seja detectada a necessidade de reboot após o upgrade dos pacotes, o playbook notifica e lista os pacotes que exigem reboot.

## Arquivos
- `inventory/hosts`: Arquivo de inventário com detalhes dos servidores.
- `playbooks/update-linux.yml`: Playbook para executar o update.


## Uso
1. Atualize o arquivo `inventory/hosts` com os detalhes do seu servidor.

## IP
IP: Este é o endereço IP do host ao qual o Ansible se conectará para executar as tarefas. Pode ser um endereço IP ou um nome de domínio.

## ansible_user

ansible_user=nomedousuário: Define o nome de usuário usado para se conectar ao host remoto. Neste caso, nomedousuário será usado como o nome de usuário SSH.

## ansible_ssh_pass

ansible_ssh_pass=senhadousuário: Define a senha usada para autenticação SSH. senhadousuário será usada como a senha para se autenticar no host remoto.

## ansible_become_pass

ansible_become_pass=senhadousuário: Define a senha que será usada para elevar privilégios (sudo). Isso é útil quando o usuário precisa executar comandos como superusuário (root).

## ansible_ssh_common_args

ansible_ssh_common_args='-o StrictHostKeyChecking=no': Define argumentos adicionais para a linha de comando SSH. A opção -o StrictHostKeyChecking=no desativa a verificação da chave de host SSH. Isso é útil em ambientes onde os hosts são dinâmicos ou quando você deseja evitar a verificação manual das chaves de host. No entanto, pode ser uma prática insegura, pois desativa uma camada de proteção contra ataques de "man-in-the-middle".


2. Execute o playbook com:

```sh
ansible-playbook -i inventory/hosts playbooks/update-linux.yml