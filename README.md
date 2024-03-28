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

    vagrant up cups
    ansible-playbook playbooks/cups.yml

### Adicionando impressora:

    vagrant ssh cups
    hpsetup -i ip.da.impressora

### Configurando o impressoras:
```bash
# 1. mariadb (supondo IP 172.17.0.2. confirme)
docker run --rm --name mariadb --env MARIADB_DATABASE=impressoras --env MARIADB_ROOT_PASSWORD=alfafa mariadb
# 2. senhaunica-faker (172.17.0.3)
docker run --rm --name faker --env APP_URL=http://172.17.0.3 uspdev/senhaunica-faker
# 3. impressoras (172.17.0.4)
# configurar o .env considerando os serviços cups, mariadb e senhaunica-faker
docker run --rm --name impressoras --env-file=.env uspdev/impressoras
# 3.1 pode ser necessário criar o APP_KEY
docker exec -it impressoras php artisan key:generate --show
# 4. migration
docker exec -it impressoras php artisan migrate
```
