# Store
The store acts as a repository for [plugins](./plugin.md), where [users](./users.md) can find and download plugins and developers can upload their plugins.

## Dashboard
In the [dashboard](./dashboard.md) there is a page from where users can access the verified plugins from the store. 

## Website
It might be nice to have a website that displays the plugins that are in development, tracking their progress via git. This can also be used to track the verification status of plugins.

## Verification
Plugins that appear on the dashboard store page should be verified before be allowed to be seen there. This is because while uploading plugins should be available for everyone, non-experienced users will put trust in the quality of the store page. It may also be a good idea to in a later stage automatically verify updates of plugins that are available trough the store page. A possible workflows for verifying:
### Asking for verification
```text
Developer                                 Store site                                  Verifier
  |                                           |                                            |
(is owner of unverified plugin)               |                                            |
  |                                           |                                            |
  | ---------Asks for verification----------> |                                            |
  |                                           |                                            |
  |                              Adds plugin to list of plugins                            |
  |                               that yet have to be verified.                            |
  |                                           |                                            |
 ---                                         ---                                          ---
```
### Verifying (success)
```text
Developer                                 Store site                                  Verifier
 ---                                         ---                                          ---
  |                                           |                                            |
  |                                           | <------------Assigns to plugin------------ |
  |                                           |                                            |
  |                                           |                        Checks plugin and finds 
  |                                           |                             no issues with it.
  |                                           |                                            |
  |                                           | <-------------Verifies plugin------------- |
  |                                           |                                            |
  |                                Marks plugin as verified                                |
  |                                 and removes from list.                                 |
  |                                           |                                            |
  | <---------Notifies developer?------------ |                                            |
```
### Verifying (denying)
```text
Developer                                 Store site                                  Verifier
 ---                                         ---                                          ---
  |                                           |                                            |
  |                                           | <-------------Assigns to plugin----------- |
  |                                           |                                            |
  |                                           |                        Checks plugin and finds 
  |                                           |                     a/multiple issues with it.
  |                                           |                                            |
  |                                           | <--------------Denies plugin-------------- |
  |                                           |                                            |
  |                                   Removes from list.                                   |
  |                                           |                                            |
  | <------------Denies request-------------- |                                            |
  |                                           |                                            |
```
It may also be a good idea to limit the amount of verification attempts a developer can do per certain amount of time.