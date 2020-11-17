# Plugin
A plugin is a piece of code that uses the IJO [dashboard](./dashboard.md) or [machine](./machine.md) interfaces to add functionality to IJO. This can be very high-level functionalities like containerization or small additions like adding support for some custom database service. Plugins can be installed by [users](./user.md) using the [store](./store.md) on the dashboard or by installing them manually. Plugins can be programmed in JS (maybe support for other programming languages will be added at a later moment).

## File structure
A possible file structure for a plugin is:
```text
machine/
  windows.*/
    index.js
  linux.*/
    index.js
dashboard/
  index.js
README.md
plugin.json
```

## Environments
Because some plugins might not work on all operating systems a plugin can specify different source files for different environments. It can also specify which parts of the plugin only have to be included for that environment.

## Smart metadata
It is also preferred to include metadata in the plugin config file about what [blocks](./flow.md) and line handler are included in the plugin.

## Versions
All plugins should update plugins with version numbers. This helps the store to keep track of metadata that changes per function. If a user is using a block in one of his/her flows and an update removes that block the user should know it is impossible to update without changing the old flow.

## Downloading a plugin
This show how a plugin is downloaded (or updated):
```text
Store                                     Dashboard                                    Machine
  |                                           |                                            |
  | <--The panel requests to download a------ |                                            |
  |    plugin from the store.                 |                                            |
  |                                           |                                            |
  | ---The store returns the plugin, but----> |                                            |
  |    compressed.                            |                                            |
  |                                           |                                            |
  |                                The panel decompresses                                  |
  |                                      the plugin.                                       |
  |                                           |                                            |
  |                                           | ---The panel sends the whole plugin------> |
  |                                           |    to the machine, unless othewise         |
  |                                           |    specified.                              |
  |                                           |                                            |
  |                               The panel calls the panel                                |
  |                           initialization part of the plugin.                           |
  |                                           |                                            |
  |                                           |                  The machine calls the machine
  |                                           |              initialization part of the plugin
  |                                           |                                            |
  |                                           | <--The machine sends back a message------- |
  |                                           |    the plugin initialized succesfully      |
  |                                           |    or had an error.                        |
```