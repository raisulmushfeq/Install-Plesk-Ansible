# Ansible playbook to install plesk on windows server
## To prepare the windows server for remote management via ansible, run the following commands one by one
```
$url = "https://raw.githubusercontent.com/jborean93/ansible-windows/master/scripts/Install-WMF3Hotfix.ps1"
$file = "$env:temp\Install-WMF3Hotfix.ps1"
(New-Object -TypeName System.Net.WebClient).DownloadFile($url, $file)
powershell.exe -ExecutionPolicy ByPass -File $file -Verbose
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
$url = "https://raw.githubusercontent.com/ansible/ansible/devel/examples/scripts/ConfigureRemotingForAnsible.ps1"
$file = "$env:temp\ConfigureRemotingForAnsible.ps1"
(New-Object -TypeName System.Net.WebClient).DownloadFile($url, $file)
powershell.exe -ExecutionPolicy ByPass -File $file
winrm enumerate winrm/config/Listener
```
### run it with 
time ansible-playbook -i hosts main.yml -e ansible_password='{{ lookup("env", "ANSIBLE_WIN_ADMINISTRATOR_PASS") }}'

# set the admin pass via  
 export ANSIBLE_WIN_ADMINISTRATOR_PASS="Password_Goes Here" or add it "export ANSIBLE_WIN_ADMINISTRATOR_PASS="Password_Goes Here" to ~/.bashrc
## Prepare the server using: https://docs.ansible.com/ansible/latest/user_guide/windows_setup.html
## Ansible Modules Collection: https://docs.ansible.com/ansible/latest/collections/ansible/windows/index.html