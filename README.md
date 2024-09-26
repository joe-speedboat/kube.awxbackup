# kube.awxbackup
Howto backup awx in k3s or any kubernetes

This are just my notes how i got it working in my lab, it may be a good starting point to create your own backup.
* Keep in mind to change the application name and pv settings to your needs

```
[root@k3s01 ~]# kubectl get awx
NAME      AGE
bitbull   2d16h
[root@k3s01 ~]# kubectl get awxbackups.awx.ansible.com 
NAME                        AGE
awxbackup-2024-09-22-0536   27m
awxbackup-2024-09-22-0538   25m
awxbackup-2024-09-22-0558   4m48s
[root@k3s01 ~]# grep bitbull kube.awxbackup/*yml
kube.awxbackup/awx-backup-cron.yml:                deployment_name: bitbull
# change this to your instance name before setting up

# install daily backup
for i in awx-backup-role.yml awx-backup-rolebinding.yml awx-backup-pvc.yml awx-backup-cron.yml awx-backup-cleanup-cron.yaml
do
  echo $i
  kubectl apply -f $i
done

```
