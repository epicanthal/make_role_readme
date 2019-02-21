Role Name: **make_role_readme**
=========

Generate Role markdown file (README.md) from meta data and a template. Inspired by and based on Jason Edelman's [ansible-webdocs](https://github.com/jedelman8/ansible-webdocs).

Notes:
- Since markdown and jinja are "funny", you may need extra [line breaks](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet#lines) and [escaping](http://jinja.pocoo.org/docs/2.10/templates/#escaping) to get things just right.
- You can omit any variables in readme.yml, which will result in empty sections.

---
Requirements
------------

Copy **_readme.yml_** to role meta/ directory for every role.  Complete/Modify variable values as necessary.

---
Role Variables
--------------
| Variable     | required    | default  | choices    | comments |
| ------------- |-------------| ---------|----------- |--------- |
| mr_path_to_roles | yes | first path in roles_path | | The path to your roles.  [DEFAULT_ROLES_PATH](https://docs.ansible.com/ansible/latest/reference_appendices/config.html#default-roles-path) is used in defaults/main.yml |
| mr_md_filename | yes | README.md | | The name of the markdown file to be generated. |
| mr_role_name | yes || | The name of the role. |


---
Dependencies
------------

You can place a list of galaxy roles here (use extra line breaks as necessary):
- example.dependency_role1
- example.dependency_role2

---
Example Playbooks
----------------
Maybe you want to place some extra text here to explain the following examples.


### Create README.md for role 'aci_build'
```YAML
- name: Generate Role(s) README.md
  hosts: localhost
  connection: local
  gather_facts: yes

  tasks:
    - name: include 'make_role_readme'
      include_role:
        name: make_role_readme
      vars:
        mr_role_name: aci_build
```

### Loop through multiple roles to create a README.md for each.
* Caveat - [Escaping](http://jinja.pocoo.org/docs/2.10/templates/#escaping) may be necessary in readme.yml.
```YAML
- name: Generate Role(s) README.md
  hosts: localhost
  connection: local
  gather_facts: yes

  vars:
    mr_role_names:
      - make_role_readme
      - another_role
      - yet_another_role

  tasks:
    - name: include 'make_role_readme'
      include_role:
        name: make_role_readme
      vars:
        mr_role_name: "{{ mr_role_names_item }}"
      loop: "{{ mr_role_names }}"
      loop_control:
        loop_var: mr_role_names_item
```


---
License
-------

BSD

---
Author Information
------------------

Kris Vensl
