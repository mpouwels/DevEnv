**Install my local development environment**

Installs my Vagrant set-up with 1 server: development.

**Step 1:**

- vagrant up  (brings up the server)

**Step 2**

After server is up, grab the DHCP ip address with:

- vagrant ssh -c "hostname -I | cut -d\" \" -f2" 2>/dev/null

And edit the file ** in inventory/hosts ** with the vagrant's ip so ansible can use it.

**Step 3**

Then copy the public ssh key to the vagrant environment with.

- ssh-copy-id -i ~/.ssh/id_rsa.pub vagrant@[IP_OF_THE_VAGRANT_MACHINE}

**Step 4**

Configure servers with ansible playbook:

* passswords are in ansible vault (vars/vault.yml)
* password for vault: if needed ask me :-)

Execute playbook with:
- ansible-playbook playbook.yml -i inventory/hosts

Now the development set-up is ready for use!