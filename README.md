# Ansible Elasticsearch Cluster
Ansible template to create elasticsearch cluster

### Testing in
* 3 Master node
* 2 Data node
* Ubuntu 18.04 

## Step
* Prepare deployer nodes (ansible is installed in here)
```
sudo apt-add-repository ppa:ansible/ansible
sudo apt update
sudo apt install ansible
```
* Make sure deployer have root access into all nodes (tips using ssh-copy-id)
```
ssh-copy-id root@master
ssh-copy-id root@data
```
* Clone this repository
```
git clone https://github.com/zufardhiyaulhaq/ansible-elasticsearch-cluster.git
```
* Change some variable
```
group_vars/all.yml
hosts/hosts
```
* Run ansible
```
ansible-playbook main.yml -i hosts/hosts
```
