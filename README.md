# Ansible playbook to install plesk on windows server
run it with 
ansible-playbook -i hosts main.yml -e ansible_password='{{ lookup("env", "ANSIBLE_PASSWORD") }}'

# set the admin pass via  
 export ANSIBLE_PASSWORD="Password_Goes Here"
## Prepare the server using: https://docs.ansible.com/ansible/latest/user_guide/windows_setup.html