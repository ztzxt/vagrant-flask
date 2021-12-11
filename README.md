
# Flask Dev. Env. with Vagrant

## About

This git repository utilizes Vagrant to create a simple development environment for a Flask app. Flask app is just there for demonstration purposes and taken from [Flask Quickstart ](https://flask.palletsprojects.com/en/2.0.x/quickstart/) documentation.

Vagrant uses Virtual Box as a provider. VM created from the `ubuntu/focal64` box is provisioned by Ansible using the `ansible_local` provisioner. Vagrant installs Ansible on the guest by default when this provisioner is used. 

`provisioning.yml` ensures that all dependencies are installed. If a new PyPI dependency arises during development, the Ansible playbook should be modified to reflect the changes. Whenever the playbook is modified, `vagrant provision`  should run to apply the playbook. When playbook is applied, Gunicorn is started as a daemon. Error logs are written to `flask-logs.txt` on the workspace. `--reload` argument is used with Gunicorn to make sure new content is reflected immediately to the developer. Gunicorn binds to port 8080 on all interfaces on VM and the host's port 8080 on 127.0.0.1 is forwarded to the guest's port 8080. 

`vagrant up` command is enough to use this project as-is. This command downloads the VM image, creates the VM, and runs the Flask app via Gunicorn. After runnig the command, go to [localhost:8080](localhost:8080) to see the app. Modify `main.py` and make sure changes are reflected to browser. 

Enjoy :)