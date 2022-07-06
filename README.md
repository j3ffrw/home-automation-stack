
# Encrypt passwords for secrets.yml
ansible-vault encrypt_string --vault-password-file vaultpassfile 'test'

# deploy containers and configuration
ansible-playbook -i inventory.yml --vault-password-file vaultpassfile  playbook.yml --tags deploy,reconfig

# Test templates
ansible all -i "localhost," -c local -m template -a "src=templates/hassio/config/configuration.yaml.j2 dest=./config.yaml" -e@host_vars/hassio-avcn.local.yml -e@secrets.yml --vault-password-file vaultpassfile -C -D
