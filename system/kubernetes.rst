Kubernetes
==========

Kubernetes is an open-source system for automating deployment, scaling, and management of containerized applications.

http://kubernetes.io/

Basically, it's a project that overlaps a bit in value proposition with :wiki:`System/CoreOS`, even if both can be complementary (you can run a Kubernetes cluster on CoreOS).

Run a web related thing: Ingress -> Service -> Deployment -> ReplicaSet -> Pod

Rollout / rollback using deployments
::::::::::::::::::::::::::::::::::::

Tip article: `How to rollout or rollback a deployment on a Kubernetes cluster? </blog/en/tips/2016/08/27/rollout-rollback-kubernetes-deployment.html>`_

Rollout
-------

.. code-block:: shell

    kubectl patch deployment $DEPLOYMENT \
            -p'{"spec":{"template":{"spec":{"containers":[{"name":"$CONTAINER","image":"$IMAGE"}]}}}}'

Rollback
--------

.. code-block:: shell

    kubectl rollout undo deployment/$DEPLOYMENT [--to-revision 42]

Status
------

.. code-block:: shell

    kubectl rollout status deployment/$DEPLOYMENT

Google Container Engine (GKE)
:::::::::::::::::::::::::::::

GKE is a managed Kubernetes cluster. For now, Ingresses are a bit buggy and it's often necessary to use the Google Cloud API to
update backends and firewall rules.

Checklist when things goes wrong:

* K8S: Ingress -> Service -> Deployment -> ReplicaSet -> Pod
* GC: Firewall rules matches the service exposed NodePort (describe service to get the port)
* GC: L7 router configuration is correct (backend, routes, frontend)
* GC: Health checks show green status.
