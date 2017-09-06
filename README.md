# ansible-in-galaxy
Ansible galaxy roles collection

## ansible galaxy
+ Galaxy provides pre-packaged units of work known to Anasible as roles
+ Roles can be dropped into Ansible PlayBooks and immediately put to work
+ You can regard ansible-galaxy binary as python's pip
+ Your can always install a role from internet by

```
$ ansible-galaxy install uername.rolename
```

+ However, previous usage will install role to *ANSIBLE_ROLES_PATH*, which is
/etc/ansible/roles by default. Most of the time, you are not root, so we prefer
to run following command to install a role

```
$ ansible-galaxy install --roles-path . uername.rolename
```

+ If you want to install multiple roles at one, you should first create a .yml file
like install_roles.yml here

```
# install_roles.yml

# from galaxy
- src: yatesr.timezone

# from github
- src: https://github.com/bennojoy/nginx

# from github, overriding the name and specifying a specific tag
- src: https://github.com/bennojoy/nginx
  version: master
  name: nginx_role

# from a webserver, where the role is packaged in a tar.gz
- src: https://some.webserver.example.com/files/master.tar.gz
  name: http-role

# from bitbucket, if bitbucket happens to be operational right now :)
- src: git+http://bitbucket.org/willthames/git-ansible-galaxy
  version: v1.4

# from bitbucket, alternative syntax and caveats
- src: http://bitbucket.org/willthames/hg-ansible-galaxy
  scm: hg
  ```

+ And then you install all of them by

```
$ ansible-galaxy install --roles-path . -r install_roles.yml
```
