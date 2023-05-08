<img src="https://img.shields.io/badge/language-DockerCompose-blue.svg"/> <img src="https://img.shields.io/github/last-commit/vmzcloud/DockerCompose_GitLab.svg"/>

# GitLab 

## Preparation

### Change the docker host sshd port first
vi /etc/ssh/sshd_config
<pre>
Port 34001
</pre>

Restart sshd
<pre>
systemctl restart sshd
</pre>

firewall for Port 34001
<pre>
firewall-cmd --permanent --add-port=34001/tcp
firewall-cmd --reload
</pre>

## GITLAB HOME

### Add new HDD for GITLAB HOME
<pre>
pvcreate /dev/sdc
vgcreate VG_Gitlab /dev/sdc
lvcreate -n home -l100%FREE VG_Gitlab

mkfs.xfs /dev/mapper/VG_Gitlab-home
</pre>

### Create folder, add to /etc/fstab, mount the mountpoint
<pre>
mkdir /srv/gitlab
</pre>

vi /etc/fstab, add the following
<pre>
/dev/mapper/VG_Gitlab-home /srv/gitlab xfs defaults 0 0
</pre>

<pre>
mount -a
</pre>

### Start the GitLab container
Put the

- docker-compose.yaml
- .env

into /root/GitLab folder\
Execute the following command
<pre>
docker compose up -d
</pre>
