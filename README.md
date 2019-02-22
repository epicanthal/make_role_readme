Ansible Role: **make_role_readme**
=========

Generate Role markdown file (README.md) from meta data and a template. Inspired by and based on Jason Edelman's [ansible-webdocs](https://github.com/jedelman8/ansible-webdocs).
- Goal:  Keep a somewhat consistent format for README.md and as
  Mr. Edelman states " if I didn’t end up creating this, I would
  have spent a ton of time manually creating tables in markdown
  one at a time for each [role] I was building! And just imagine
  making a small change like adding a row or column to each one!"

- Notes:

    - Since markdown and jinja are "funny", you may need extra
      [line breaks](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet#lines) and
      [escaping](http://jinja.pocoo.org/docs/2.10/templates/#escaping) to get things just right.

    - You can omit any variables in readme.yml, which will
      result in empty sections.

    - **_choices_** for a variable are supplied as a list.

    - Look at meta/readme.yml from this role to see how it was used to
      generate this README.md

---
Requirements
------------

Copy **_readme.yml_** skeleton to role meta/ directory for every role.  Modify as necessary.

---
Role Variables
--------------
| variable    | required    | default  | choices    | comments |
| ------------- |-------------| ---------|----------- |--------- |
| mr_path_to_roles | yes | **_first path in roles_path_** | <ul></ul> | The path to your roles.  [DEFAULT_ROLES_PATH](https://docs.ansible.com/ansible/latest/reference_appendices/config.html#default-roles-path) is used in defaults/main.yml |
| mr_md_filename | yes | README.md | <ul></ul> | The name of the markdown file to be generated. |
| mr_role_name | yes || <ul></ul> | The name of the role. |


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

### Supply a path to role(s)
```YAML
- name: include 'make_role_readme'
  include_role:
    name: make_role_readme
  vars:
    mr_role_name: aci_build
    mr_path_to_roles: /aci_project/roles
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
