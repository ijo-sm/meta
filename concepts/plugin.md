# Plugin
A plugin is a piece of code that uses the IJO [dashboard](./dashboard.md) or [machine](./machine.md) interfaces to add functionality to IJO. This can be very high-level functionalities like containerization or small additions like adding support for some custom database service. Plugins can be installed by [users](./user.md) using the [store](./store.md) on the dashboard. Plugins can be programmed in JS (maybe support for other programming languages will be added at a later moment).

# Environments
Because some plugins might not work on all operating systems a plugin can specify different source files for different environments.