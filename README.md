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
* Logs
```
root@zu-elk-master1:~# curl http://10.200.200.11:9200/_cat/nodes?v
ip            heap.percent ram.percent cpu load_1m load_5m load_15m node.role master name
10.200.200.14           28          38   0    0.09    0.27     0.23 di        -      \zu-elk-data1
10.200.200.13           30          38   0    0.10    0.25     0.17 mi        -      \zu-elk-master3
10.200.200.15           25          38   0    0.12    0.29     0.25 di        -      \zu-elk-data2
10.200.200.11           30          38   0    0.09    0.22     0.15 mi        *      \zu-elk-master1
10.200.200.12           28          38   0    0.08    0.20     0.11 mi        -      \zu-elk-master2
root@zu-elk-master1:~# curl http://10.200.200.11:9200/_cluster/health?pretty
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
