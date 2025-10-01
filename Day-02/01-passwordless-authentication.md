# How to setup Passwordless Authentication

# Local connecting
    ls /mnt/c/Users/squar/Downloads/

     cp /mnt/c/Users/squar/Downloads/ansible.pem ~/.ssh/
     chmod 600 ~/.ssh/ansible.pem
     ssh -i ~/.ssh/ansible.pem ubuntu@65.1.131.120


## EC2 Instances

### Using Public Key

```
ssh-copy-id -f "-o IdentityFile <PATH TO PEM FILE>" ubuntu@<INSTANCE-PUBLIC-IP>
```



- ssh-copy-id: This is the command used to copy your public key to a remote machine.
- -f: This flag forces the copying of keys, which can be useful if you have keys already set up and want to overwrite them.
- "-o IdentityFile <PATH TO PEM FILE>": This option specifies the identity file (private key) to use for the connection. The -o flag passes this option to the underlying ssh command.
- ubuntu@<INSTANCE-IP>: This is the username (ubuntu) and the IP address of the remote server you want to access.

### Using Password 

- Go to the file `/etc/ssh/sshd_config.d/60-cloudimg-settings.conf`
- Update `PasswordAuthentication yes`
- Restart SSH -> `sudo systemctl restart ssh`

      eval "$(ssh-agent -s)"
      ssh-add ~/ansible.pem



- ssh-agent is a program that runs in the background and stores your private keys in memory.  

- -s tells it to output shell commands to set the right environment variables.

- eval executes those commands so your current shell knows how to talk to the agent.

👉 Effect: You now have an SSH agent process running in your WSL session, ready to hold keys.

 **2. ssh-add ~/<your key.pem>**  
 
ssh-add loads your private key into the running ssh-agent.

Example:

    ssh-add ~/ansible.pem


Once added, the key is cached in memory → so you don’t need to pass -i ~/ansible.pem every time you SSH or use Ansible.

👉 Effect: Your SSH agent now has the key ready to authenticate automatically.

🔁 Typical workflow
```
eval "$(ssh-agent -s)"        # start the agent
ssh-add ~/ansible.pem         # add your AWS key to the agent
ssh-add -l                    # list loaded keys (verify)
ssh ubuntu@<server-ip>        # connect without specifying -i
```

⚠️ By default, keys are only loaded for the current WSL session. If you open a new terminal, you’ll need to run ssh-add again unless you automate it.

# Steps to Auto-Load Your Key in WSL
# 1. Start ssh-agent automatically

Edit your ~/.bashrc (or ~/.zshrc if you use zsh):

     sudo vim ~/.bashrc

Add this at the end of the file:

# Start ssh-agent if not already running

    eval "$(ssh-agent -s)" > /dev/null 2>&1

# 2. Auto-add your key

Right after that line, add:

# Add AWS/Ansible private key

    ssh-add -q ~/ansible.pem 2>/dev/null

-q = quiet mode (no output).

2>/dev/null = suppress errors if the key is already added.

# 3. Reload your shell

    source ~/.bashrc

# 4. Verify

Check that the key is loaded:

     ssh-add -l

You should see your key fingerprint.

**⚠️ Important Notes**

Make sure your .pem file has correct permissions:

    chmod 400 ~/ansible.pem
    
If you restart your WSL instance completely, it will restart ssh-agent and re-add the key (because of .bashrc).
