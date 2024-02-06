Ad-hoc commands are one-liners that we can use to perform quick tasks on managed nodes without the need for writing a complete playbook. 
Ad-hoc commands are useful for tasks like gathering information, troubleshooting, or making one-time changes. Here are some examples:

***Remember to use the `-b` flag to run these ad-hoc commands with elevated privileges (as a superuser).***

***The -a option specifies the module arguments or parameters that you want to pass to the module being used. It stands for "arguments".***

**Ping all servers:**

   - Check if Ansible control node can communicate with all servers in the inventory.
   
   ```bash
   ansible all -m ping
   ```
   This sends a "ping" message to all servers, and if successful, it indicates that Ansible can connect to the servers.

**Run a command:**

   - Execute a shell command on all servers. This runs the `uptime` command on all servers and displays their uptime.
   
   ```bash
   ansible all -m command -a "uptime"
   ```
**Check disk space:**

   - Get information about disk space on all servers. This command runs the `df -h` command on all servers to display disk space information.
   
   ```bash
   ansible all -m shell -a "df -Th"
   ```
**Create a directory:**

   - Create a directory on all servers. This command creates a new directory on all servers using the `file` module.

   ```bash
   ansible all -m file -a "path=/home/ansibleusr/testdir state=directory" -b
   ```
**Install a package:**

   - Install a package on all servers using the package manager. This installs the Nginx package on all servers using the `yum` module.

   ```bash
   ansible all -m yum -a "name=httpd state=present" -b
   ```
**Start httpd service:**

   - Start httpd service on all servers using service module.

   ```bash
   ansible all -m service -a "name=httpd state=stopped enabled=true" -b
   ```
**Copy a file:**

   - Copy a file from the local machine to all servers. This copies a file from the local machine to the specified path on all servers.
   
   ```bash
   ansible all -m copy -a "src=/path/to/local/file.txt dest=/path/on/remote/server/file.txt" -b
   ```
   ***Example : ***
   ```bash
   ansible all -m copy -a "src=index.html dest=/var/www/html/" -b
   ```
