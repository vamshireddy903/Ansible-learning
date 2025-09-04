<img width="1199" height="585" alt="image" src="https://github.com/user-attachments/assets/e70cad7e-09c8-494e-a96b-611a92a01f74" />

# Common commands

<img width="1081" height="611" alt="image" src="https://github.com/user-attachments/assets/c8894639-c778-4eed-aa07-f5f39ef2e146" />
<img width="1034" height="221" alt="image" src="https://github.com/user-attachments/assets/3990be7d-9b86-497d-b096-f15bbda59d95" />
<img width="993" height="670" alt="image" src="https://github.com/user-attachments/assets/f36c6797-8b35-47dc-87b4-ddbd60049759" />
<img width="970" height="432" alt="image" src="https://github.com/user-attachments/assets/4796117b-973b-43a3-9f2b-d5baeefaa4ae" />
<img width="901" height="646" alt="image" src="https://github.com/user-attachments/assets/a401e757-d763-4f04-9c45-b51ec7e5e883" />
<img width="906" height="339" alt="image" src="https://github.com/user-attachments/assets/bf9fa35f-540c-488e-9ffe-bf7381e4ccba" />

<img width="1085" height="391" alt="image" src="https://github.com/user-attachments/assets/efb3075a-1d60-4b66-a8b6-6e61917c0c18" />
<img width="1119" height="366" alt="image" src="https://github.com/user-attachments/assets/e8b39cba-e2fe-48b4-ad90-1ca0a59dc603" />

# Copy files from local to remote

               ansible -i inventory.ini all -m copy -a "src=/home/devops/file.txt dest=/tmp/file.txt" -b
# Reboot servers

             ansible -i inventory.ini all -m reboot -b
             
# Check service status

           ansible -i inventory.ini all -m shell -a "systemctl is-active nginx" -b
           ansible -i inventory.ini all -m shell -a "systemctl is-enabled nginx" -b

<img width="923" height="171" alt="image" src="https://github.com/user-attachments/assets/d9ebe191-f77e-4d77-bcdb-82033924783b" />

# Stop service before uninstall

# It’s a good practice to stop the service before uninstalling:

     ansible -i inventory.ini all -m service -a "name=nginx state=stopped" -b
     
     ansible -i inventory.ini all -m apt -a "name=nginx state=absent purge=yes" -b

# Update the package to the latest version

      ansible -i inventory.ini all -m apt -a "name=nginx state=latest update_cache=yes" -b
      
# Reboot the server

      ansible -i inventory.ini all -m command -a "/sbin/reboot" -b

# Create a directory

       ansible -i inventory.ini all -m file -a "path=/tmp/testdir state=directory mode=0755" -b

       ansible -i inventory.ini all -m file -a "path=Testdir state=directory mode=0755"
       
<img width="739" height="231" alt="image" src="https://github.com/user-attachments/assets/e8d8e4d7-073a-4097-89cd-11eaba65e4de" />

# Create a file 

      ansible -i inventory.ini all -m file -a "path=/tmp/testfile.txt state=touch mode=0644" -b

<img width="1028" height="594" alt="image" src="https://github.com/user-attachments/assets/06372f51-8707-4e22-87c8-3fcb36352031" />

      
<img width="717" height="186" alt="image" src="https://github.com/user-attachments/assets/efe6fc57-b4ab-48bc-a7d7-87ed07d1b863" />



