# Ideas
This file contains the ideas we have for IJO Server Manager.


## Language
The programming that will be used for IJO is Javascript, with NodeJS running it. This is because: NodeJS is lightweight; Javascript is the most well-known language; NodeJS is platform-independed, meaning it can be used on (almost) all platforms.


## Store
The store is basically a JSON API to access all the official plugins from. It makes it easier to check the plugins, keep them updated on your machine and manage them. There will also be a HTML version of the store that interacts with the store's API. You can use this HTML version to search for plugins, but it won't directly install them. Just like NPM.


## Plugins
The plugin system will allow for the usage of multiple programming language to create your plugin. This is done to let all users create their own plugins, without them having to learn a whole new language. To make this work, programming languages are installed in two parts. There first part is the engine and the second part is the interface. The engine is the part that executes the programming language. This means you don't necessarily need an SDK to execute a  plugin. The interface is a program written in the programming language that acts as an interface for the plugin. It lets the plugin create instance of classes, which actions will be passed through to the panel or machine via an IPC connection that was created when the instance was spawned. Of course, when using JavaScript, the engine won't have to be installed, since NodeJS can already be used.

### Downloading a plugin
```text
Store                                       Panel                                       Machine
  |                                           |                                            |
  | <- The panel requests to download a ----1-|                                            |
  |    plugin from the store.                 |                                            |
  |                                           |                                            |
  |-2- The store returns the plugin, but ---> |                                            |
  |    compressed.                            |                                            |
  |                                           |                                            |
  |                              3 - The panel decompresses                                |
  |                                      the plugin.                                       |
  |                                           |                                            |
  |                                           |-4- The panel sends the part for the -----> |
  |                                           |    machine to the machine.                 |
  |                                           |                                            |
  |                             5 - The panel calls the panel                              |
  |                           initialization part of the plugin.                           |
  |                                           |                                            |
  |                                           |            6 - The machine calls the machine
  |                                           |            initialization part of the plugin
  |                                           |                                            |
  |                                           | <- The machine sends back a message -----7-|
  |                                           |    the plugin initialized succesfully      |
  |                                           |    or had an error.                        |
  |                                           |                                            |
```
The same process is used when updating a plugin.

### Starting a plugin
```text
Panel                                       Interface                                   Plugin
  |                                             |                                          |
  |-1- The panel starts by using the engine --> |                                          |
  |    to start the interface.                  |                                          |
  |                                             |                                          |
  |                                             |-2- The interface calls the startup ----> |
  |                                             |         function in the plugin.          |
  |                                             |                                          |
  |                                             | <- The plugin calls the interface to --3-|
  |                                             |    create instances or cause other       |
  |                                             |    events that will be passed through    |
  |                                             |    to the panel.                         |
  |                                             |                                          |
  | <- The interface will call the panel -----4-|                                          |
  |    there was an event caused by the plugin. |                                          |
  |                                             |                                          |
```
The same 2 first steps are used when stopping the plugin.


## Flows
A flow is a server pipeline. These pipelines are used to manage servers. 

### Load balancer
```text
                                             Gateway
                                       everything on port 80
                                      with domain: example.com
                                      to 8080 or 8081 or 8082
                                                |
                      |-------------------------|-------------------------|
                      |                         |                         |
                    Server                    Server                    Server
                 on port 8080              on port 8081              on port 8082
```

### Container
A container creates a submachine. This is basically a little machine that will be in the parent machine. Using this you can create multiple flows.
```
Gateway
everything on port 80
with domain: example.com
   |
   |- Container: 80 > 8080 
```

### Cron jobs & Hooks
```text
Job
every 10 minutes
 |
 |
 Hook
 backup-plugin
 /everything
```


## Dashboard
The dashboard page contains information about everything, displayed in two modes. The first mode is automatic selection, which uses algorithms to select to most relevant information. The second mode is pinned, which displays the information pinned by the user. There are dashboard pages for the whole panel, machines and even for individual pipelines.


## Permissions
There are permissions for everything. This is done so a small hosting company can decide what features a user can and cannot touch or even view.
```yaml
user:
  server.view
 
admin:
  server.*
```
