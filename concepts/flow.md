# Flow
Flows are the core concept of IJO and what makes it unique with respect to other server managers. Flows describe in a flowchart kind of way the flow of data between services (and users). Here services or parts of services are "boxes" and "lines" connecting the boxes describe the flow of data. An example of this would be a line coming from an opened port 80 to a static webserver:
```text
Gateway
everything on port 80
  |
  |
 \./
Static webserver
```
Using such a flowchart we make it very easy for not just developer but also less programming-savvy users to understand what is happening, as such flowchart perfectly describes the experience for those using the webserver. As lines in most cases describe sockets they almost always have an orientation, as seen in the example.

## Load balancer
This is an example of what a flowchart for gateways should look like:
```text
						     ---
							  | (port 80)
							  | 
						     \./
	|-------------------Load balancer-------------------|
	|                         |                         |
   \./                       \./                       \./
  Server                    Server                    Server
on port 8080             on port 8081              on port 8082
```

## Container
And this an example of a flow that goes into a container. The part of the flow inside the container might also be seen from the machine running in the container, if that is enabled.
```text
					  ---
					   | 
	+------------------|-(port 8080)------+
	|                  | (port 80)        |
	|                  |                  |
	|                 \./                 |
	|               Server                |
	|             on port 80              |
	|                                     |
	+-------------------------------------+
```