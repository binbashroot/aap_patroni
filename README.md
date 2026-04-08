AAP2.6+ in an HA config using Patroni    

1. Build your AAP and Postgres hosts to spec
2. Create a patroni "inventory". Refer to the [Patroni](./examples/patroni_inventory) inventory.
3. Run deploy_pgcluster.yml playbook against your patroni inventory
4. Run deploy_haproxy.yml playbook against your patroni inventory
5. Update your AAP installation inventory to use "localhost" for your pg hosts. This is NOT your patroni inventory. Refer to the example AAP 2.6 [inventory](./examples/aap26_inventory)
6. Run the AAP installation against your modified inventory

Additional information:  
ETCD and Patroni are installed from an external Postgres yum repo
Postgres 16 is installed from the RHEL9 supported repositories

To check etcd health
etcdctl --endpoints=http://PG1_IP:2379,http://PG2_IP:2379,http://PG3_IP:2379 endpoint health

To check your patroni health
patronictl -c /etc/patroni/patroni.yml list
