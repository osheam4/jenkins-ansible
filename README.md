# jenkins-ansible
Set up a jenkins server with ansible - on docker


# Requirements
```
yum install docker-ce docker-compose
usermod -aG docker docker_admin
# docker_admin or local user on remote server who will run the ansible commands
```


# Deployment
This can be run from user laptop, or jenkins. Using the following commands.

```
python3 -m venv ~/.ansible_docker_venv
source ~/.ansible_docker_venv/bin/activate

pip install -r requirements.txt

# Create vault password file for ansible to use
# insecure password for this repo = changeme
~/.ansible_vault_passw

# Run the playbook to deploy logstash docker container
ansible-playbook -u ansible_svc --vault-password-file ~/.ansible_vault_passw -i stages/dev jenkins.yml
# Where dev = environment
```


# To replace certs a deployment is needed.
```
ansible-vault edit stages/dev/group_vars/docker_secrets.yml
# Replace the pem in secrets file.

Run the deployment, as above.

```

# To update the jenkins version.
```
docker image pull jenkins/jenkins:lts
# Run the Deployment section above to force image refresh.
# This section could be automated if desired.
```