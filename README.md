# "Element Size" Balancer

A small example of a HAProxy based Load Balancing config that routes traffic to different backends based on a dynamic size of some "element" inside the request. The idea is that you might have backends that can only handle a specific size of a request, where the size is not based on the bytes of the request payload, but a more arbitrary element determined by the developer.

## Example

Let's say the load balancer is proxying requests that contain 1-N log items.  For "some" reason, various backend servers can only handle smaller amounts of log items per request, in this example divided into three groups of 1-10, 10-50 and 50+. 

The developer will send information about the amount of log items (N) in the request. There are multiple methods to get this information in the Load Balancer:
- using Proxy Protocol in any mode
- through a header or JSON payload in HTTP mode
- etc.

The load balancer will fetch this information and route the traffic to the right backend.
