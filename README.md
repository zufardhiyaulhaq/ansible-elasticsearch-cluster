# Ansible Elasticsearch Cluster
Ansible template to create elasticsearch cluster

### Testing in
* 3 Master node
* 2 Data node
* Centos 7.6 

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
git clone https://github.com/zufardhiyaulhaq/ansible-elasticsearch-cluster.git -b centos
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
## logs
```
[root@zu-elk-master2 ~]# curl http://10.200.200.11:9200/_cat/nodes?v
ip            heap.percent ram.percent cpu load_1m load_5m load_15m node.role master name
10.200.200.14           32          31   8    0.82    0.54     0.31 di        -      \zu-elk-data1
10.200.200.12           32          31   6    0.63    0.49     0.32 mi        -      \zu-elk-master2
10.200.200.11           34          31   7    0.82    0.59     0.33 mi        -      \zu-elk-master1
10.200.200.13           32          31   6    0.71    0.52     0.32 mi        *      \zu-elk-master3
10.200.200.15           32          31   7    0.75    0.53     0.31 di        -      \zu-elk-data2
[root@zu-elk-master2 ~]# curl http://10.200.200.11:9200/_cluster/health?pretty
{
  "cluster_name" : "production",
  "status" : "green",
  "timed_out" : false,
  "number_of_nodes" : 5,
  "number_of_data_nodes" : 2,
  "active_primary_shards" : 0,
  "active_shards" : 0,
  "relocating_shards" : 0,
  "initializing_shards" : 0,
  "unassigned_shards" : 0,
  "delayed_unassigned_shards" : 0,
  "number_of_pending_tasks" : 0,
  "number_of_in_flight_fetch" : 0,
  "task_max_waiting_in_queue_millis" : 0,
  "active_shards_percent_as_number" : 100.0
}
```
