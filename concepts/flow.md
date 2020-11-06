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

## Connecting blocks
Different blocks provide different services, each can have multiple parents and multiple children. Each line has an outgoing and incoming part and not all blocks can connect to eachother. This is solved by creating handlers for each variation of a block to block lines that are allowed. A block may also provide a universal incoming line handler. This way and outgoing line only has to be made compatible with the universal handler. Not all handlers are included with IJO by default of course, they will check the store if there is a plugin that has defined that handler.

## Propagator
These are a special kind of boxes that are the start of data transfer. This will, in the most cases, be the gateway. It could also be cron job, sending a start signal to another service.

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
How containers will be implemented is as of yet to be seen. Running a machine instance in every container will take to much computation. It might be better to just observe the container from the outside. What control that gives for blocks inside of the container is, in that case, doubtful.