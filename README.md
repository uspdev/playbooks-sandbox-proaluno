## Geral

#### Instalação e configuração do libvirt para criar virtualização:

    sudo apt install virt-manager libvirt-dev ansible
    sudo adduser SEU-USER libvirt

#### Instalação do plugin do libvirt no ansible:

    vagrant plugin install vagrant-libvirt

#### Instalando roles:

    cd ansible-proaluno
    ansible-galaxy install -r requirements.yml --force

## Samba DC:

### Subindo Samba DC

    vagrant up sambadc
    ansible-playbook playbooks/sambadc.yml

### Criando usuário

    vagrant ssh sambadc
    sudo samba-tool user create rickastley

### Subindo cliente:

    vagrant up clientedeb
    ansible-playbook playbooks/clientedeb.yml

### Testando cliente:

    sudo virt-viewer

### Subindo cups:
Copiar o role cups_server de https://github.com/wgnann/ansible-roles.

    vagrant up cups
    ansible-playbook playbooks/cups.yml

### Adicionando impressora:

    vagrant ssh cups
    hpsetup -i ip.da.impressora

### Configurando o impressoras:
Faremos a instalação do impressoras usando uma instância com docker.

    vagrant up docker
    vagrant ssh docker

Dentro da instância:
```bash
sudo apt install docker.io docker-compose
sudo usermod -a -G docker vagrant
# deslogar e logar para pegar o grupo

# build do senhaunica-faker (temporário)
git clone https://github.com/uspdev/senhaunica-faker
cd senhaunica-faker
cp .env.example .env
docker build -t faker .

# build do impressoras (temporário)
git clone https://github.com/wgnann/impressoras
cd impressoras
docker build -t impressoras .

# editar o compose.yaml
#  - adicionar configurações do replicado
#  - modificar o SENHAUNICA_ADMINS
cd /vagrant/impressoras
docker-compose up

# OBS: o env.example é exatamente o mesmo do repositório do impressoras

# rodar as migrations
docker-compose exec impressoras php artisan migrate

# acessar http://192.168.40.5:8000
```
