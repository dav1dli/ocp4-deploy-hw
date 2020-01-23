# Lab parameters
* GUID: 9f52
* Bastion: ssh bastion.9f52.sandbox483.opentlc.com
* aws_access_key_id = ****
* aws_secret_access_key = ****
* Base domain: .sandbox483.opentlc.com
* Users: john, paul, ringo, george, pete 
* Architecture: 3 masters - m4.xlarge, 2 workers - m4.xlarge, 2 infra - m4.large

# Install
* https://access.redhat.com/documentation/en-us/openshift_container_platform/4.2/html/installing_on_aws/index
* Installation: https://cloud.redhat.com/openshift/install/aws/installer-provisioned
* Client: https://mirror.openshift.com/pub/openshift-v4/clients/ocp/latest/openshift-client-linux-4.2.14.tar.gz
* Installer: https://mirror.openshift.com/pub/openshift-v4/clients/ocp/latest/openshift-install-linux-4.2.14.tar.gz

`openshift-install create install-config --dir=~/lab-cluster`

* Platform: aws
* AWS Access Key ID: ****
* AWS Secret Access Key: ****
* Region: eu-central-1
* Base domain: sandbox483.opentlc.com
* Cluster name: cluster-9f52

`lab-cluster/install-config.yaml`:

```
apiVersion: v1
baseDomain: sandbox483.opentlc.com
compute:
- hyperthreading: Enabled
  name: worker
  platform: {}
  replicas: 2
controlPlane:
  hyperthreading: Enabled
  name: master
  platform: {}
  replicas: 3
metadata:
  creationTimestamp: null
  name: cluster-9f52
networking:
  clusterNetwork:
  - cidr: 10.128.0.0/14
    hostPrefix: 23
  machineCIDR: 10.0.0.0/16
  networkType: OpenShiftSDN
  serviceNetwork:
  - 172.30.0.0/16
platform:
  aws:
    region: eu-central-1
    type: m4.xlarge
pullSecret: ****
```

`openshift-install create cluster --dir=$HOME/lab-cluster --log-level=info`

API: https://api.cluster-9f52.sandbox483.opentlc.com:6443
To access the cluster as the system:admin user when using 'oc', run `export KUBECONFIG=/home/dliderma-redhat.com/lab-cluster/auth/kubeconfig`
Console: https://console-openshift-console.apps.cluster-9f52.sandbox483.opentlc.com user: kubeadmin, password: ****
