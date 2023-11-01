# Services

Before starting the task:

*   Run the following command:
    
        $ ./deploy_svc
    

**To check tasks and get secret phrases run:**

    $ ./checker -course 'kubernetes' -course-version 'services' -test-suite 'service'

**Task 1:**

Create `pod-info-svc` service for `pod-info-app` deployment:

    Requirements:
     Name: pod-info-svc
     Type: ClusterIP
     Service Port: 80
     Service TargetPort: 80

Investigate `pod-info-app` deployment and choose selector and do not change the deployment

**Task 2:**

Run a pod (based on image busybox:1.28) and execute following commands (as given below) inside this pod and save outputs into files:

    wget -q -O- pod-info-svc save to $HOME/testing-clusterip-web.log
    nslookup pod-info-svc save to $HOME/testing-clusterip-nslookup.log

**Task 3:**

*   Create deployment `myapp`, image: sbeliakou/web-pod-info:v1, replicas: 1
*   Create headless service `myapp-headless` pointing to myapp pods
*   Create non-headless service `myapp-clusterip` pointing to myapp pods

Checking name resolution:

Non-headless service has own IP address (and port), and proxies traffic to backends:

    $ kubectl run --rm -it test --image=busybox:1.27 --restart=Never nslookup myapp-clusterip

Headless service doesn’t proxy traffic to backends, it simply responds (on early dns lookup phase) with the IP address(es) where to go:

    $ kubectl run --rm -it test --image=busybox:1.27 --restart=Never nslookup myapp-headless

**Task 4:**

We have already created hello-hello web application for you. Create a new service to access this web application, check the requirements.Figure out all necessary settings from the deployment.

    Requirements:
     Name: hello-hello-service
     Type: NodePort
     Downstream Pod Port (Service targetPort): 80
     Node Port: 30300

For verification you can execute `` `curl $NODE_IP:30300` `` command or open the browser page http://$NODE\_IP:30300. Substitute $NODE\_IP with the IP address of your node.

  
  

This is it with services. To remove auomatically privisioned resources run:

    $ ./delete_svc

And don't forget to clean up everything else