# Introduction

yum\_updown is an Ansible role that supports downgrading and updating (including installing) of RPMs.

Using conditionals, these two tasks (downgrade and update) are made mutual exclusive, i.e., only one of the tasks gets executed at any point in time. The effect is that either a downgrade or an update of the RPM will be made (or nothing if the desired version is already installed). The variable can be passed via the command-line like this: `--extra-vars "rollback=true"`

# Usage

The role can be included in a playbook or included as a dependency of another role, as shown below:

1. Included in a playbook

    test_playbook.yml
    ---
      - hosts: web_tier
        roles:
          - { role: yum_updown, rpm_name: "cowsay-3.03-8.el6", repos_to_disable: "centos6-base-x86_64,centos6-updates-x86_64" }

2. Included in another role as a dependency

    roles/test_role/meta/main.yml
    ---
    dependencies:
      - { role: yum_updown, rpm_name: cowsay-3.03-8.el6, repos_to_disable: "centos6-base-x86_64,centos6-updates-x86_64" }

The parameter `repos_to_disable` is introduced to improve performance (by disabling, e.g., centos repositories where our RPM is not hosted).

# Examples

For a normal update/install:
    ansible-playbook -i inventory test_playbook.yml -v -u your_username -s

For a downgrade/rollback:
    ansible-playbook -i inventory test_playbook.yml -v -u your_username -s --extra-vars "rollback=true"

