# Setting up JupyterHub (for admin)

These are the steps I took to install JupyterHub, set up user accounts, and add R language tools.

1. Set up a virtual machine running Ubuntu 18.04. This was tested on an AWS EC2 instance of the t2.medium class.
2. Set permissions for internet traffic. On AWS EC2, this involves setting a security group and allowing inbound traffic on some ports (e.g., 80)
3. ssh into the VM.
4. Run the following:
```
sudo apt-get update
sudo apt-get install python3-venv
```
5. Follow this [tutorial](https://jupyterhub.readthedocs.io/en/stable/installation-guide-hard.html). **NOTE**: there are several steps which require `sudo su` and will not work with a simple `sudo` from the base account. Make sure the following lines are in the config file:
```
c.Spawner.default_url = '/lab'
c.JupyterHub.ip = '0.0.0.0'
c.JupyterHub.port = 80
c.PAMAuthenticator.open_sessions = False
c.Authenticator.admin_users = {'jupyter-admin'}
c.LocalAuthenticator.create_system_users=True
```
6. Create an administrator account:
```
sudo useradd -s /bin/bash -m jupyter-admin
sudo passwd jupyter-admin
```
7. Log into JupyterHub and verify it's working. Should be at `<vm_ip_address>:8080`
8. Set up R language for JupyterHub:
This will open `R` in a `sudo` session:
```
sudo /opt/conda/bin/conda install -c r r-base
sudo -i /opt/conda/lib/R/bin/R
```
This should install the iRkernel system-wide:
```
install.packages("IRkernel")
old_path = Sys.getenv("PATH")
Sys.setenv(PATH=paste(old_path, "/opt/conda/bin/", sep=":"))
IRkernel::installspec()
```
Need to be root for this next part:
```
sudo su
```
This will make the iRkernel visible to JupyterHub:
```
sudo /opt/jupyterhub/bin/jupyter-kernelspec install /root/.local/share/jupyter/kernels/ir/
```
It may be that the location in which the iRkernel was installed was different than this. The output of the `IRkernel::installspec()` command will say. So more generally the final commmand is:
```
sudo /opt/jupyterhub/bin/jupyter-kernelspec install <location_of_iR_kernel>
```
Exit sudo:
```
exit
```
Restart JupyterHub:
```
sudo systemctl restart jupyterhub.service
```
You should now be able to log into JupyterHub and see the R language is available. 

