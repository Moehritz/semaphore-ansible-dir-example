# Problem

In semaphore, ansible is expected to be in root dir of git repo.

This git repo shows a (I think common) setup when the IaC tooling consists of more than ansible (for example, also having a terraform/tofu folder, ...).

<img width="1216" height="674" alt="image" src="https://github.com/user-attachments/assets/4fc26841-910c-4924-b529-aa36adf49c4b" />

Leads to this error:
```
10:36:35 AM
[ERROR]: the role 'create_file' was not found in /private/var/folders/l7/fmbz2tqj52s8jqtqgc069x_m0000gp/T/semaphore/project_1/repository_1_template_1/ansible/playbooks/roles:/var/folders/l7/fmbz2tqj52s8jqtqgc069x_m0000gp/T/semaphore/project_1/repository_1_template_1_home/.ansible/roles:/usr/share/ansible/roles:/etc/ansible/roles:/private/var/folders/l7/fmbz2tqj52s8jqtqgc069x_m0000gp/T/semaphore/project_1/repository_1_template_1/ansible/playbooks
10:36:35 AM
Origin: /private/var/folders/l7/fmbz2tqj52s8jqtqgc069x_m0000gp/T/semaphore/project_1/repository_1_template_1/ansible/playbooks/debug.yml:7:7
10:36:35 AM
10:36:35 AM
5
10:36:35 AM
6   roles:
10:36:35 AM
7     - create_file
10:36:35 AM
        ^ column 7
10:36:35 AM
10:36:35 AM
Failed to run task: exit status 1
```

# Proposed fix:
 Like for terraform/tofu tasks, allow a "workdir" to be set for ansible,
 so instead of running:
 `ansible-playbook ansible/playbooks/debug.yml`
 this would be run:
 `cd ansible; ansible-playbook playbooks/debug.yml`
