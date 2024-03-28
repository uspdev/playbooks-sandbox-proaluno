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
