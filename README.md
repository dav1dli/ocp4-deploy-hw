# Homework Assignment Lab
## Goals
Assess hands-on proficiency with Red Hat® OpenShift® Container Platform advanced deployment topics

Complete this course leading to Red Hat Delivery Specialist - Advanced Platform-as-a-Service (PaaS) Administration accreditation.

## Criteria
Assignments take the average student about eight hours to complete

Assignments are an individual effort—complete the assignment without collaboration

Assignments simulate a challenge typically encountered in a Red Hat Consulting engagement

## Grading
You should create a fully functional OpenShift 4 cluster which satisfies all criteria listed below. The cluster should pass all FTL tests.

## Submission
FTL output
Result of running the `grade_lab ocp4_advanced_deployment hw` command. You can locate the file here: `/tmp/grading_result.txt`

Indicate the following in a note with the submission in the FTL output file:
* Instructor
* Class location
* Class date

Instructions for using the LMS: Red Hat employees: Red Hat LMS



## Environment
Log in to OpenTLC. Go to Services → Catalogs → OPENTLC OpenShift 4 Labs → OpenShift 4 Installation Lab. Click Order → Submit

You will recieve three emails indicating the status of the environment and instructions for accessing the environment. In the third email you receive all information you need to install and configure an OpenShift 4 cluster.

# 1. Business Use Case
You are a consultant on an assignment to a telecommunications company called MitziCom.

MitziCom is very impressed by the demonstration of OpenShift 4 capabilities and the results of the PoC that you provided. Now they want to deploy a fully functional cluster for their development team. They asked you to install a cluster that is as close as possible to a production cluster in terms of resource control and security.

# 2. Requirements
You have to install an OpenShift 4 cluster to satisfy the following requirements. At the end of the installation you have to run a script which tests all required cluster parameters.

The script checks your cluster settings literally: if the requirements specify "20G" it checks for "20G" and not for "20Gi". Please pay attention to such details.
Your setup should satisfy all the requirements. Don’t destroy your cluster until you have received PASSED to all tests.

## 2.1. Cluster Information Requirements
* The cluster name should be named *cluster-$GUID*
* Use the base domain sandboxNNN.opentlc.com

Replace the NNN with the sandbox ID that appears in your list

## 2.2. User Authentication Requirements
Ability to authenticate both at the webconsole and command line

Five users have access to the cluster: *john*, *paul*, *ringo*, *george*, and *pete*. The password for each user should be set to `openshift4`.

Note: to pass the tests you should have logged in with oc login as each of the users at least once so that the user object is created in the cluster.

User *john* is a cluster admin

## 2.3. Cluster Architecture Requirements
There are three master nodes working

There are two worker nodes

There are two infra nodes

Image registry is running on one of the infra nodes

Routers (two replicas) are running on two infra nodes

Logging and monitoring are running on the infra nodes

Elasticsearch should run on two nodes and have SingleRedundancy

## 2.4. Sizing Requirements
Masters: instance size .xlarge (m4.xlarge or m5.xlarge)

Infra nodes: instance size .xlarge (m4.xlarge or m5.xlarge)

Workers: instance size .large (m4.large or m5.large)

Elasticsearch: make storage volume 20G, memory request 4Gi, CPU request 500m

Hint: you will have to edit the clusterlogging object to change the requests

## 2.5. Resource Controls Configuration
LimitRange for all new project should be set to:

LimitRange name: project-limits

Default request: 500m CPU

Default request: 500Mi memory

Default limits: 1 CPU

Default limits: 1Gi memory

Resource Quota for all new projects should be set at:

ResourceQuota name: project-quota

10 pods

4CPU/8Gi requests over all pods/containers

6CPU/16Gi limits over all pods/containers

20G PVC storage

HINT: you have to change the default Project Request Template (look up in the documentation)

## 2.6. Network Policy Configuration
In each new project the following network traffic should be allowed:

Between Pods in the same namespace (the policy name should be allow-same-namespace)

From Ingress namespace to the Pods in the project (the policy name should be allow-from-openshift-ingress)

HINT: you have to change the default Project Request Template

# 3. Setup Test
To test your setup you have to run the following command on your bastion/VM host:

$ grade_lab ocp4_advanced_deployment hw <your-opentlc-id>
It will create a test project and check if all its parameters (quotas, limit ranges, network policies) are set according to the requirements above. The command will display the test results. Make sure it passed all the tests.

After the command above passed all the tests, find the results file in /tmp/grading_report.txt. Submit this file with your class details as described in the Submission section.
