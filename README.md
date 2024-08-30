## Geral

#### Instalação e configuração do libvirt para criar virtualização:

    sudo apt install virt-manager libvirt-dev ansible
    sudo adduser SEU-USER libvirt

#### Instalação do plugin do libvirt no ansible:

    vagrant plugin install vagrant-libvirt

#### Instalando roles:

    cd ansible-proaluno
    ansible-galaxy install -r requirements.yml --force

## Samba DC

### Subindo Samba DC

    vagrant up sambadc
    ansible-playbook playbooks/sambadc.yml

### Criando usuário

    vagrant ssh sambadc
    sudo samba-tool user create rickastley

## Cliente

### Subindo cliente:

    vagrant up clientedeb
    ansible-playbook playbooks/clientedeb.yml

### Testando cliente:

    sudo virt-viewer

## Impressoras

### Subindo cups:
Copiar o role cups_server de https://github.com/wgnann/ansible-roles.

    vagrant up cups
    ansible-playbook playbooks/cups.yml

### Adicionando impressora:

    vagrant ssh cups
    hpsetup -i ip.da.impressora

### Configurando o impressoras:
Faremos a instalação do impressoras usando uma instância com docker.

Editar o `impressoras/compose.yaml`
  - adicionar configurações do replicado
  - modificar o `SENHAUNICA_ADMINS`

Depois:

    vagrant up docker
    ansible-playbook playbooks/docker.yml
    vagrant ssh docker
    cd /vagrant/impressoras
    docker-compose up -d
    docker-compose exec impressoras php artisan migrate

OBS: o env.example é exatamente o mesmo do repositório do impressoras

Acessar http://192.168.40.5:8000

## Cenário para casos com login numérico

Criar um grupo chamado linux no domínio pandora.tux.local:

    samba-tool group add linux --nis-domain=smbdomain --gid-number=6000

Criar um usuário numérico 123456 com senha senha123 no grupo proaluno:

    samba-tool user create 123456 senha123 --given-name=Maria --uid=a123456 --uid-number=123456 --gid-number=6000 --unix-home=/home/a123456 --login-shell=/bin/bash
