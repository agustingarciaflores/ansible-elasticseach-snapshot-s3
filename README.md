Role Name
=========

This Ansible Role allows to create snapshots of a ElasticSearch cluster in Amazon S3.

Requirements
------------

* A IAM Role must be attached to all EC2 instances of the cluster in order to allow access to the S3 bucket where we are gonna store the snapshot.
* _repository-s3_ plugin have to be installed in all instances of the cluster.

Role Variables
--------------

* **elastic_host**: Node of the cluster from where we want to launch the snapshot.
* **elastic_port**: Port where ElasticSearch is running.
* **snapshot_repository**: Name of the snapshot repository
* **snapshot_bucket**: Name of the S3 bucket where the snapshots will be stored.
* **snapshot_name**: Name of the snapshot
* **wait_for_completion**: Wait until the snapshot is complete

Dependencies
------------

None

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```
- name: Create Elastic snaphost
  hosts: hosts
  gather_facts: true
  tags: api
  tasks:
    - name: Create snapshot in S3
      include_role:
        name: ansible-elastic-snapshot-s3
      vars:
        elastic_host: localhost
        elastic_port: 9200
        snapshot_repository: "{{ elastic_snapshot_repository_name }}"
        snapshot_bucket: "{{ elastic_snapshot_bucket }}"
        snapshot_name: "{{ lookup('pipe','date +%Y%m%d') }}"
        wait_for_completion: "true"
```

Author Information
------------------

[Agustín García Flores](https://www.linkedin.com/in/agustingarciaflores/)
