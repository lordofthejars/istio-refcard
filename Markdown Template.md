# Service Mesh with Istio 

## What is Service Mesh and Istio

A *service mesh* is a dedicated infrastructure layer for making service-to-service communication safe, fast, and reliable.

Istio is a service mesh which allows you to connect, manage and secure your microservices in an easy and none intrusive way.

Some of the features that offers Istio are:

* Intelligent routing and load balancing
* Resilience against network failures
* Policy enforcement between services
* Observability of your architecture. Tracing and Metrics
* Securing service to service communication

### Istio Architecture

Istio is composed by two major components:

* **Data plane** which is composed of *Envoy* proxies deployed as sidecar container along with your service for managing network along with policy and telemetry features.
* **Control plane** which is in charge of managing and configuring all *Envoy* proxies.

![Istio Overview](arch.png "Istio Architecture")

All communication within your *service mesh* happens through *Envoy* proxy, so any network logic to apply is moved from your service into your infrastructure.

## Key Concepts of Istio

### DestinationRule

A *DestinationRule* configures the set of rules to be applied when forwarding traffic to a service.
Some of the purposes of a *DestinationRule* are describing circuit breakers, load balancer and TLS settings or define *subsets* (named versions) of the destination host so they can be reused in other Istio elements.

For example to define two services based on version label of a service with hostname *recommendation* you could do:

~~~
apiVersion: networking.istio.io/v1alpha3
kind: DestinationRule
metadata:
  name: recommendation
  namespace: tutorial
spec:
  host: recommendation
  subsets:
  - labels:
      version: v1
    name: version-v1
  - labels:
      version: v2
    name: version-v2
~~~

### VirtualService

A *VirtualService* describes the mapping between one or more user-addressable destinations to the actual destination inside the mesh.

As its name suggests a *VirtualService* are virtual destinations, so they are not registered into any service registry.

For example, to define two virtual services where the traffic is splitted between 50% to each one.

~~~
apiVersion: networking.istio.io/v1alpha3
kind: VirtualService
metadata:
  name: recommendation
  namespace: tutorial
spec:
  hosts:
  - recommendation
  http:
  - route:
    - destination:
        host: recommendation
        subset: version-v1
      weight: 90
    - destination:
        host: recommendation
        subset: version-v2
      weight: 10
~~~

### ServiceEntry

### Gateway

## Getting started with Istio

### Installing Istio

###This Is a Second-Level Header
This is the body text of the Refcard. Use two asterisks for **bold words** and one asterisk for *italic words*. **Use one underscore to create _italics_ within bold text.** _Or you can have **bold text** within italics._

To add inline code, surround the code with backticks: `public static void main (String[] args)`.

Start new paragraphs with one blank line between the two paragraphs.

Code blocks should be formatted normally and surrounded above and below by three tildes:

~~~
System.out.println("Try to keep code lines <60 chars.");
for(int i = 0; i < 2; i++){    
    if(2 + 2 != 5){
        System.out.println("Keep code neat!");
    }
}
~~~

Build tables with vertical bars/pipes:

|	Table Headings		| Go Above at Least Three Dashes	|
| -------------------	| ------------------------------	|
|	**For inline code**	|	`You can use backticks as normal`	|
|	**For spacing**		|	Keep at least one space or tab between your content and the pipes.	|
|	**Try to keep it neat**		|	But if necessary, the pipes do not have to align.	|

For links, enclose the content to be linked in square brackets, followed directly by the URL in parentheses: [This is DZone's Refcardz page.](https://dzone.com/refcardz)

Keep all images collected in a folder. To reference an image, use an exclamation point, followed by the alt text in square brackets (for the web version of the content), followed then by parentheses enclosing the following: the image directory and filename, one space, and then the image title in quotes.

![Alt text for this image](images_dir/Figure1.png "This is the title/caption for this image")

All images should be on their own line.

Ordered list items should have the number, a period, a space, and then the content of that item. You can then continue your list with numbers on new lines.

1. This is the first item of an ordered list.
2. This is the second item of an ordered list.

Use the plus sign then a space for unordered lists.

+ This is an unordered list item.
+ Here is another.

    Blank lines above and below, and leading spaces before the content, will let you create new paragraphs within the list.

+ You can then return to your list items as normal.










