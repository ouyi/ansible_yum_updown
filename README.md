# yum\_updown is an Ansible role which supports downgrade and normal RPM installation

Example:

ansible-playbook -i inventory test\_dependency.yml -v --extra-vars "rollback=false" -u your\_username -s
