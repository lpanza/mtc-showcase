# mtc-showcase
This repository is used to showcase the capabilities of the Migration Toolkit for Containers (MTC).

In the ```base``` directory, you will find the default objects needed for the MTC Operator to work, such as: <br>
* ```Namespace```; <br>
* ```OperatorGroup```; <br>
* ```Subscription```; <br>
* ```MigrationController``` (installed CRD). <br>

In the ```overlays``` directory, you will find the various host types:

* ```host```, the OCP Cluster where the Migration Controller / UI will be located (usually the target cluster, but can be an external one):
  * ```ObjectBucketClaim``` required by the migration process (note: we are using OpenShift Data Foundation in this example, which is provided [here]([url](https://github.com/lpanza/multicluster-devsecops)) )
  * a Kustomize patch to add the Migration Controller and Migration UI capabilities to the already defined ```MigrationController```.
* ```source```, the OCP Cluster where the migration process will start:
  * ```test-migration Namespace``` where we are going to set up our workload;
  * ```mariadb``` all the required objects to create a stateful application based on MariaDB;
    * This directory also contains a job to automatically create a table and fill it with test rows;
  * ```nginx``` all the required objects to create a stateless application based on Nginx;
* ```target``` the OCP Cluster where the source workload will be migrated, so the overlay just consists of the ```base``` resources.
