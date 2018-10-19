Notes
=====

Objectives
----------

* least amount of dev work for biggest gain

  * we don't want to have to change this tool chain a lot in the future

* set good examples

  * document them and make them the easiest solution to use

* get something working that covers all of our known requirements as quickly as possible

Unit Testing
------------

* unit testing

  * gitlab runner setup

Integration Testing
-------------------

* integration testing

  * spin up a full deployment in kubernetes
  * run tests
  * tear it down

Rancher
-------

* containers within containers

 * deploy ranger on a few VMs
 * install kubernetes on top of rancher

* useful for dev and testing

Helm Tiller
-----------

* it's a repo of deployment manifests

  * it's docker compose for kubernetes
  * the whole deployment is defined in a single file

* alternative service deployment: thinking about your app, not how you get there

  * ubuntu has juju

OS Selection
------------

* CoreOS

  * acquired by redhat

* generally smaller containers are better

  * fewer layers in your container, the better

* for a min environment

  * you want to run a bastion instance
  * run fedora or something

OpenShift
---------

* Kubernetes with redhat tools

  * with a redhat spin
  * useful for CI

Persistent Storage
------------------

* databases ect.

* glusterfs can be used

  * two VMs with a fibre channel back end storage
  * the more nodes you have, the better
  * benchmarks rely on local storage
  * you can create volume groups that can be tuned for the workload
  * running it with 2 nodes and high latency is not good
  * run performance tests here

* another solution: don't do it in kubernetes

  * it depends on what you're trying to store

* keepalived, proxy

  * handy for multimaster replication

* you can run postgres on gcp

  * it's pricey but it's boss

Ingress
-------

* routing

AWS EKS
-------

* it's a shit show
* use gcloud

* Jenkins is used as a CI tool

  * ansible roles for the apps
  * kubernetes manifests are in anisble playbook
  * ginga template the manifests for different environments

* if you have to update your worker nodes

  * amazon is the only cloud where they don't recycle nodes in a kubernetes aware mode
  * abs will pull the plug on the node and shove in another one
  * mid processed requests get dropped

* coreos tecktonics seems pretty good

  * the general consensus is go gcp

Research
--------

* gamedev with kubernetes

  * there are some good articles on fortnight for database scaling

* you have to educate people on their density usage

  * when you cycle your nodes, you may exhaust your limit

Security
--------

* clair - container scanning tool

  * it scans for vulnerabilities
  * should be used in the CI stack
  * maintained by coreos
  * you can set the scan level

* authorization: rbac

  * you can define RBAC rules for AD groups

* authentication: AWS IAM

* service mesh

  * istio
  * calico
  * they are controllers in the cluster
  * they setup mutual TLS between applications
  * everything is encrypted except for the kubernets dashboard

Topology
--------

* dev, qa, performance

  * different namespaces in the same cluster

* separate clusters for staging, production

Administration
--------------

* the command line tools are good

Monitoring
----------

* for performance

  * kabana, logstash
  * the builtin dashboard is good
  * heapster: pulls all containers for metrics

* prometheus

  * going to take over
  * the gitlab stack looks solid
  * install different exporters that shove metrics into prometheus
  * it doesn't store much data
  * more efficient at storing a lot of data
  * better than casandra
  * casandra is resource heavy for a few 1000 pods
  * can send metrics to graphana
  * graphana can send emails

Platforms
---------

* AWS isn't awful

  * it's about 6 months behind GCP
