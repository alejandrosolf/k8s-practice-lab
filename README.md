# Ingresses

Before starting the task:

*   Run the following command:
    
        $ ./deploy_ing
    

**To check tasks and get secret phrases run:**

    $ ./checker -course 'kubernetes' -course-version 'ingresses' -test-suite 'ingress'

**NOTE:** Think about how to resolve your application DNS name to IP.

**Task 1:**

There’re `aqua`,`maroon` and `olive` deployments created in default namespace. Please do the following:

1.  Create services `aqua-svc`, `maroon-svc` and `olive-svc` for respective deployments.
2.  Create (3) Ingress Resources which forward incoming traffic to respective pods:
    *   aqua-ingress:
        *   domain name: aqua.k8slab.net
        *   service name: aqua-svc
        *   service port: 80
    *   maroon-ingress:
        *   domain name: maroon.k8slab.net
        *   service name: maroon-svc
        *   service port: 80
    *   olive-ingress:
        *   domain name: olive.k8slab.net
        *   service name: olive-svc
        *   service port: 80
3.  Check your services in browser:
    *   aqua.k8slab.net
    *   maroon.k8slab.net
    *   olive.k8slab.net

**Task 2:**

Using the services you have created recently (in task #1), create Ingress Resource assuming that:

*   Ingress Resource Name: colors-ingress
*   FQDN: colors.k8slab.net
*   Context Paths:
    *   /aqua: implements aqua-svc response
    *   /maroon: implements maroon-svc response
    *   /\* (default, any other): implements olive-svc response

**Verification Details:**

*   colors.k8slab.net/aqua responds with aqua page
*   colors.k8slab.net/maroon responds with maroon page
*   colors.k8slab.net/ responds with olive page
*   colors.k8slab.net/blah-blah-blah responds with olive page

**Task 3:**

Let’s create a service from the requirements as below:

1.  Application red-color
    *   Deployment:
        *   Name: red-color
        *   Replicas: 3
        *   Image: sbeliakou/color:v1
        *   Environment Variables: COLOR=red
    *   Service:
        *   Name: red-svc
        *   Type: ClusterIP
        *   Port: 8080
2.  Application green-color
    *   Deployment:
        *   Name: green-color
        *   Replicas: 1
        *   Image: sbeliakou/color:v1
        *   Environment Variables: COLOR=green
    *   Service:
        *   Name: green-svc
        *   Type: ClusterIP
        *   Port: 8080
3.  Application yellow-color
    *   Deployment:
        *   Name: yellow-color
        *   Replicas: 2
        *   Image: sbeliakou/color:v1
        *   Environment Variables: COLOR=yellow
    *   Service:
        *   Name: yellow-svc
        *   Type: ClusterIP
        *   Port: 8080
4.  Service switch
    *   Name: switch
    *   Type: ClusterIP
    *   Port: 80
    *   Selected Backends: red-svc, yellow-svc and green-svc
5.  Ingress Resource lights-ingress
    *   Ingress Name: lights-ingress
    *   FQDN: lights.k8slab.net
    *   Routing Rules:
        *   lights.k8slab.net -> switch
        *   lights.k8slab.net/red -> red-svc
        *   lights.k8slab.net/green -> green-svc
        *   lights.k8slab.net/yellow -> yellow-svc

**Task 4:**

In namespace trouble-1 we’ve created two applicattions, which show html-pages with some colors.

We have two URLs:

[http://trouble-1.k8slab.net/lime](http://trouble-1.k8slab.net/lime) - should show “lime” page

[http://trouble-1.k8slab.net/purple](http://trouble-1.k8slab.net/purple) - should show “purple” page

Something failed during the deployment and now url addresses doesn’t work as expected.

Please, find the problem and fix it.

**Task 5:**

In namespace trouble-2 we’ve created two applicattions, which show html-pages with some colors.

We have two URLs:

[http://trouble-2.k8slab.net/teal](http://trouble-2.k8slab.net/teal) - should show “teal” page

[http://trouble-2.k8slab.net/navy](http://trouble-2.k8slab.net/navy) - should show “navy” page

Something failed during the deployment and now url addresses doesn’t work as expected.

Please, find the problem and fix it.

**Task 6:**

In namespace trouble-3 we’ve created two applicattions, which show html-pages with some colors.

We have two URLs:

[http://trouble-2.k8slab.net/maroon](http://trouble-3.k8slab.net/maroon) - should show “maroon” page

[http://trouble-2.k8slab.net/navy](http://trouble-3.k8slab.net/fuchsia) - should show “fuchsia” page

Something failed during the deployment and now url addresses doesn’t work as expected.

Please, find the problem and fix it.

**Task 7:**

Let's customize the default (error) page!

1.  Create the custom default-backend:
    *   Namespaxe: ingress-default-backend
    *   Deployment Name: sorry-page
    *   Image: sbeliakou/http-sorry-page
2.  Create a service with the name `sorry-page-service` (downstreams to `sorry-page` backend):
    *   Namespaxe: ingress-default-backend
    *   Service Name: sorry-page-service
    *   Type: ClusterIP
    *   Port: 80
3.  Configure ingress-nginx-controller to use our custom error backend( `--default-backend-service` )

**Validation:** try to open any not existing page.

  
  

This is it with Ingresses. To remove auomatically privisioned resources run:

    $ ./delete_ing

And don't forget to clean up everything else