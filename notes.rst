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

* A solution to continuously deploying to multiple kubernetes environments such as dev, qa, performance requires templated kubernetes manifests or hardcoded manifests for each env (app deployment, service creation, namespace creation, eg.)

  * One possible set of tools to achieve this for lets say a simple web app:

    * Jenkins as the CI/CD server
    * Ansible (able to authenticate to clusters, apply kubernetes manifests, jinja templating allows for changing the templated kubernetes manifests with specific vars)
    * postman/newman for integration test


Building Containers
------------

* Best video I've ever seen for how to build effective docker containers (https://dockercon2018.hubs.vidyard.com/watch/YppHjLzVXAoF2PaRg3oQRs)

* In your CI build process, you should include a stage for running clair before pushing your image to a repo (https://github.com/coreos/clair). This will scan your built container for CVEs.

* Microscanner is also another alternative to clair https://github.com/aquasecurity/microscanner

Kubernetes Control Plane Solutions
-------------

* AWS EKS

  * Cloud lock-in
  * Doesn't do kubernetes aware worker node upgrades
  *
  *

* Google Cloud Platform

  * Cloud lock-in
  *
  *
  *

* Azure Kubernetes Services

  * Cloud lock-in
  *
  *
  *

* CoreOS tectonic && RedHat Openshift (https://coreos.com/blog/coreos-tech-to-combine-with-red-hat-openshift/)

  * Not tied to a specific Cloud
  * Native worker node upgrades
  * Currently being merged with Redhat Openshift to provide the 'best' solution

* Rancher

  * containers within containers
  * deploy rancher on a few VMs
  * install kubernetes on top of rancher
  * useful for dev and testing

Some Kubernetes best practises
------------

* Set resource limits on your kubernetes deployments (prevents pods from using ridiculous amounts of resources. Also don't allow someone to define 8gb in a request limit!!!)

*

Essential Extra Kubernetes Goodies
-----------

* Ambassador is super useful for web based microservices. https://www.getambassador.io/

*

Kubernetes Security
------------

* Networking and ACLS

  * Calico
  * Weave
  * Ingress

* Service Mesh and why it is so important and useful (https://akomljen.com/kubernetes-service-mesh/)

  * istio

* Rbac is how kubernetes does authorization.

  * Roles
  * ClusterRoles
  * RoleBindings
  * ClusterRoleBindings

Kubernetes Cluster Organization
-------------

 * You will probably want to segregate your environments into different clusters to ensure one environment doesn't demolish another. (Security reasons as well)

 * For non critical environments you can define namespaces to segregate environments.

 * A typical setup might be:

   * Cluster 1 -> Namespace dev, Namespace qa
   * Cluster 2 -> Namespace perf
   * Cluster 3 -> Namespace prod

Kubernetes Administration
---------------

 * Kubectl commands are pretty straight forward and the documentation around it are great.

 * Kubectl command completion is a must https://kubernetes.io/docs/tasks/tools/install-kubectl/#enabling-shell-autocompletion

 * Running a jumpbox(bastion) instance in the kubernetes cluster is very useful for diagnosing issues. Pods running alpine probably won't have many utilities needed.


Helm Tiller
-----------

* it's a repo of deployment manifests

  * it's docker compose for kubernetes
  * the whole deployment is defined in a single file

* alternative service deployment: thinking about your app, not how you get there

  * ubuntu has juju

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

Research
--------

* gamedev with kubernetes

  * there are some good articles on fortnight for database scaling

* you have to educate people on their density usage

  * when you cycle your nodes, you may exhaust your limit


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
