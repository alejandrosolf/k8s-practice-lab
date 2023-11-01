# Statefulsets
Before starting the task:

*   Run the following command:
    
        $ ./deploy_sts
    

**To check tasks and get secret phrases run:**

    $ ./checker -course 'kubernetes' -course-version 'statefulsets' -test-suite 'statefulset'

**NOTE:** before running check after each task make sure that statefulset is up and all replicas are also running.

**Task 1:**

Create a new StatefulSet:

    Requirements:
     Name: random-generator
     Image: sbeliakou/random-generator:1
     Namespace: default
     Replicas: 3
     Service: random-generator
     Labels: app=random-generator

**Do not forget to copy secret phrase, test will fail after task 3.**

**Task 2:**

Add volumeClaimTemplates to `random-generator` sts. Recreate statefulset if it’s needed.

    Name: logs
    mountPath: /logs
    Capacity: 10Mi
    accessMode: ReadWriteOnce

**Task 3:**

Update container’s image to version 2.

_Please pay attention to the way how StatefulSet recreates pods. It starts from 2 and goes to 0._

**Task 4:**

Run any test pod. Using nslookup check the record of random-generator service. Save the output of the above commands to `$HOME/k8s_sts.txt`

    nslookup random-generator-0.random-generator.default.svc.cluster.local
    nslookup random-generator-1.random-generator.default.svc.cluster.local
    nslookup random-generator-3.random-generator.default.svc.cluster.local

  
  

This is it with statefulsets. To remove auomatically privisioned resources run:

    $ ./delete_sts

And don't forget to clean up everything else