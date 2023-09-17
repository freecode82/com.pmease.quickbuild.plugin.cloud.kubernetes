# com.pmease.quickbuild.plugin.cloud.kubernetes
quickbuild kubernetes plugin(my custom version)

It was added so that a service could be created using the clusterip method, and the pod name could also be created using the qbagent-[specified pod name] method.

Additionally, a volume name was specified when creating a pod so that pre-made PVC could be used.


However, when a volume name exists, the agent is created only between the Agent start Number and Agent end Number.

The name of the agent was also created as qbagent-[specified pod name]-Agent start Number ~ Agent end Number.


Ingress can also be created using the pod name by specifying metadata.name as ${name}.

install
----------------------------------------------------------------
1. move com.pmease.quickbuild.plugin.cloud.kubernetes-custom_13.0.43.jar to quickbuild plugin folder
2. ex) mv com.pmease.quickbuild.plugin.cloud.kubernetes-custom_13.0.43.jar /quickbuild-location-dir/plugins
3. remove already exist com.pmease.quickbuild.plugin.cloud.kubernetes_13.0.43.jar
4. ex) rm /quickbuild-location-dir/plugins/com.pmease.quickbuild.plugin.cloud.kubernetes-custom_13.0.43.jar
5. quickbuild server restart
----------------------------------------------------------------

Pod kustomization to use volumes
----------------------------------------------------------------
```
apiVersion: v1
kind: Pod
metadata:
  name: ${name}
spec:
  containers:
  - name: ${name}
    volumeMounts:
    - name: ${volumename}
      mountPath: /data/data
#    resources:
#      requests:
#        cpu: 2000m
#        memory: 8000m
  volumes:
  - name: ${volumename}
  nodeSelector:
    beta.kubernetes.io/os: linux
  restartPolicy: Never
```
-------------------------------------------------------------------------

ingress sample yaml
-------------------------------------------------------------------------
```
apiVersion: networking.k8s.io/v1beta1
kind: Ingress
metadata:
  name: ${name}
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
  - http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          serviceName: test
          servicePort: 80
```
--------------------------------------------------------------------------------
