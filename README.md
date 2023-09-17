# com.pmease.quickbuild.plugin.cloud.kubernetes
quickbuild kubernetes plugin(my custom version)

It was added so that a service could be created using the clusterip method, and the pod name could also be created using the qbagent-[specified pod name] method.

Additionally, a volume name was specified when creating a pod so that pre-made PVC could be used.


However, when a volume name exists, the agent is created only between the Agent start Number and Agent end Number.

The name of the agent was also created as qbagent-[specified pod name]-Agent start Number ~ Agent end Number.


Ingress can also be created using the pod name by specifying metadata.name as ${name}.
