# <a name="run-playbook"></a>Run playbook
Change working directory to playbook home:

    cd httpd_centos

Run playbook (check first)

    ansible-playbook --check site.yml -i hosts --ask-vault-pass --extra-vars '@passwd_vault.yml'

This command asks for the vault password. And does a 'dry-run' of the playbook, no modifications to the system will be performed.  Once you are happy with the results, perform the real deal:

    ansible-playbook site.yml -i hosts --ask-vault-pass --extra-vars '@passwd_vault.yml'


## <a name="rollback-httpd-to-a-specific-version"></a> Rollback httpd to a specific version
The current playbook provides a downgrade option for the httpd package. Check the [appendix](#appendix) for instructions on how to obtain available versions.

To downgrade to a specific version, modify the file `group_vars/all` in the playbook directory. In it, replace the version specified with `httpd_previous:`, eg: `httpd-2.4.6-88.el7.centos`. After modifying the file, you perform the downgrade by issuing the command

    ansible-playbook site.yml -vv -i hosts --ask-vault-pass --extra-vars '@passwd_vault.yml' --extra-vars "rollback=true"

## <a name="remove-httpd"></a> Remove httpd
The playbook also provides a remove method for the httpd package. You remove the installed httpd by issuing the command

    ansible-playbook site.yml -vv -i hosts --ask-vault-pass --extra-vars '@passwd_vault.yml' --extra-vars "remove=true"

# <a name="run-specific-tasks-or-skip-them"></a>Run specific tasks (tags) or skip them:
Throughout the plays 'tags' are used which enable installation (or skipping) of specific plays:
To install packages and update the firewalld config of these packages, run

    ansible-playbook site.yml --ask-vault-pass --extra-vars '@passwd_vault.yml' --tags "packages,firewalld"

To skip deployment of packages, use

    ansible-playbook site.yml --ask-vault-pass --extra-vars '@passwd_vault.yml' --skip-tags "packages"

# <a name="appendix"></a> Appendix
## <a name="check-available-version-of-a-package"></a>Check available versions of package
In order to obtain a list of currently available package versions for httpd on a host, run:

   yum --showduplicates list httpd*
