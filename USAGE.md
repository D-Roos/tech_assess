# Run playbook
Change working directory to playbook home:

    cd httpd_centos

Run playbook (check first)

    ansible-playbook --check site.yml -i hosts --ask-vault-pass --extra-vars '@passwd_vault.yml'

This command asks for the vault password. And does a 'dry-run' of the playbook, no modifications to the system will be performed.  Once you are happy with the results, perform the real deal:

    ansible-playbook site.yml -i hosts --ask-vault-pass --extra-vars '@passwd_vault.yml'

# Run specific tasks (tags) or skip them:
Throughout the plays 'tags' are used which enable installation (or skipping) of specific plays:
To install packages and update the firewalld config of these packages, run

    ansible-playbook site.yml --ask-vault-pass --extra-vars '@passwd_vault.yml' --tags "packages,firewalld"
To skip deployment of packages, use

    ansible-playbook site.yml --ask-vault-pass --extra-vars '@passwd_vault.yml' --skip-tags "packages"
