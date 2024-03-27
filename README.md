Instalação e configuração do libvirt para criar virtualização:

    sudo apt install virt-manager libvirt-dev ansible
    sudo adduser SEU-USER libvirt

Instalação do plugin do libvirt no ansible:

    vagrant plugin install vagrant-libvirt

Instalando roles:

    cd ansible-proaluno
    ansible-galaxy install -r requirements.yml --force

Subindo sambadc:

    vagrant up sambadc
    ansible-playbook playbooks/sambadc.yml
    