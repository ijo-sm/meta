# Machine
A machine is a controlling instance of IJO running on a virtual or physical operating system. It controls the services on the operating system as directed by its configuration. This configuration is controlled by the IJO [dashboard](./dashboard.md). Communication between the dashboard and machines is encrypted by default (maybe not for internal connections), but this can be turned off if that is preferred. Since this connection is only to be used by the dashboard asymmetric cryptography is used. The following is an example of a machine tree.
```text
                          Dashboard
							  |
  +-------------+-------------+-------------+-------------+
  |             |             |             |             |
Physical     Physical      Physical      Physical    Physical
machine      machine       machine       machine      machine
  |                           |                           |
Container                  Virtual         +--------------+
                           machine         |              |
                                       Container    Container
```