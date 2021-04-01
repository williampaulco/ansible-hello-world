# Setup
Install the following components.  If any of them are already installed, upgrade to the latest.  If they are not installed and you are on Windows, I recommend Chocolatey.  All of these instructions are for a Windoes installation only.
## Chocolatey
Open Powershell as administrator and run the following.
```
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
```
## VirtualBox
Open CMD as Administrator and run the following.
```
choco install virtualbox
```
## Vagrant
Open CMD as Administrator and run the following.
```
choco install vagrant
```
# Run Code
1. Pull down the code.
```
git clone https://github.com/williampaulco/ansible-hello-world.git
```
2. Navigate to the project directory.
3. Run the following.  This command pulls down the virtual machine images, starts them up, and provisions them using the scripts in the Vagrantfile.  The first time you run this will be really slow as it'll need to go over the wire and download the virtual machine image.  However, the second time will be much faster.
```
vagrant up
```
4. Once the machines are up, you can ssh into the Ansible controller VM.  Do this using the following command.
```
vagrant ssh controller
```
5. From this box, you can run the ansible scripts.  They will create a directory in the other VM, winhost.  While this is a very simple ansible script, it provides a starting point for learning ansible.  You can run the ansible scripts using the following command.
```
ansible-playbook /vagrant/yml/playbooks/main.yml -i /vagrant/yml/inventory/hosts.yml
```
# Notes
* On the VMs, the /vagrant directory is shared with your host machine.  Thus, you can modify the ansible scripts from your host machine and then rerun them using the command above.  This is a great way to experiment with and learn ansible.
# Useful Links
* [Ansible Windows Modules](https://docs.ansible.com/ansible/latest/collections/ansible/windows/)