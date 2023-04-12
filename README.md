# chaos-qa

## What is Chaos Engineering?

Chaos engineering is a method of testing distributed software that deliberately introduces failure to verify its resilience in the face of random disruptions.

## Why is Chaos Engineering necessary ? 

By designing and executing Chaos Engineering experiments, you will learn about weaknesses in your system that could potentially lead to outages that cause customer harm. You can then address those weaknesses proactively, going beyond the reactive processes that currently dominate most incident response models.

## Which platforms or targets does Harness Chaos module support? 

Harness Chaos Engineering (HCE) can inject faults on a wide range of infrastructure platforms, including Kubernetes/OpenShift, AWS, GCP, Azure, VMWare and Baremetal systems.  

## What are the prerequisites for Chaos Engineering? 

Here are a few important prerequisites to carry out chaos engineering: 

- Cultural infrastructure with alignment to respond and buy-in from stakeholders
- Ability to detect changes in the system under test, i.e., observability
- Expectations about hypotheses around system behavior
- Tooling to carry out chaos experimentation with right controls (blast radius & security. 

## What is the simplest Chaos Experiment I can perform? 

Deleting a pod belonging to one of your microservices (pod is the smallest deployable unit in Kubernetes that consists of one or more containers) is a simple, yet effective chaos experiment. Harness Chaos Module provides a pod-delete experiment template that you can readily leverage. 

It can be used to verify:

- Disk (or volume) re-attachment times in stateful applications
- Application start-up times, and readiness probe configuration 
- Adherence to topology constraints (node selectors, tolerations, zone distribution, and affinity/anti-affinity policies)
- Leader election process in case of stateful application clusters, like databases
- Proxy registration times in service-mesh environments
- Lifecycle hooks and graceful termination for the microservices under active load
- Resource budgeting on cluster nodes

## How does the Pod-Delete Chaos Experiment work? 

By default, the experiment causes a graceful or forced deletion of random pods that satisfy a specific app selection criteria, i.e, they bear a specific label, belong to a certain workload type (such as deployment or statefulsets) and reside in a given namespace. The experiment simulates a rescheduling operation or an eviction scenario. The experiment is also capable of causing the deletion of a group of pods identified by their name(s) and also take percentage values (of pods that meet the app selection criteria) as chaos inputs. 

## What are the possible outcomes of the Pod-Delete Chaos Experiment? 


The possible outcomes of a pod deletion experiment include: 

- Uninterrupted service by the workload due to availability of additional replicas  with no impact to performance 
- Uninterrupted service by the workload due to availability of additional replicas, but with significant degradation in performance 
- Transient loss of service followed by successful recovery of the system within acceptable recovery window   
- Complete failure of the system for a brief period, followed by self-heal/recovery 
- Complete failure of the system needing manual intervention

## How can I measure the impact of the Pod-Delete Chaos Experiment? 

APM platforms are the best sources to indicate the impact of the pod-deletion fault. The impact can be observed using the Golden Signals, i.e., the following few metrics, during the chaos window (and beyond, in some cases): 

- Application Traffic/QPS: Rate of requests served 
- Error Count/Rate: Failed requests count/Rate  
- Latency: Avg time taken to serve the requests 
- Saturation: The resource utilization levels for the given service

In addition to these, it might be of interest to verify the following information from a Kubernetes cluster health & configuration standpoint: 

- Time to reschedule pod 
- Time to (re) attach volumes 
- Time for application startup
- Time for autoscale (in cases where the pod-autoscaling is configured & saturation is high) 

## Where should I run the Pod-Delete Chaos Experiment? 

You can begin by running the chaos experiments on pre-production environments (Dev-Test, QA, Staging). Once you are confident about your applications’ resilience to pod failures and about the readiness of your observability infrastructure, you can execute the pod-delete chaos experiment in production, albeit with low blast radius. 

## When should I run the Pod-Delete Chaos Experiment?

Chaos experiments can be executed at various points of time in the application delivery cycle. The effectiveness of the experiment depends upon the environment it is executed in, the hypotheses associated with it & extent to which the target microservice/application is loaded. Here are some recommendations: 

- As part of the build & test pipelines, where the generated service artifact is deployed in a transient test-bed/cluster. This helps rule out obvious stability issues, if any and prevent deploy in higher environments

- As part of exploratory testing in QA & Performance/Benchmarking test cycles, to verify how the service stands up to failure for a variety of load conditions and the subsequent impact on downstream services

- As part of post upgrade automated (CD pipeline driven) or manual sanity runs in long-living staging environment (that mimics production) 
 
- As part of Gameday events in production, with multiple participating stakeholders and during maintenance or lean windows. 




