# User
A user is as the name implies a user using IJO. Most probable is that the user is using the [dashboard](./dashboard.md), but using the [machines](./machine.md) directly is also not excluded. 

## Permissions
A user can be the administrative user, able to access all parts of the dashboard, or a user with more limited permissions. This way IJO can be used by small hosters that can give the customers access to their own (restricted) machines for example. As per the tree structure of machines the permissions a user has for a parent are inhereted by its children.

## Roles
A role is a set of permissions created by the administrative user. Roles can then be assigned to users to easily assign groups of permissions to users. Roles can created for machines (and thus their children) or for the maximal node, the dashboard, which means the role is globally assignable. Roles created for a parent node can also be assigned to its child node and the permissions that apply for that child will automatically be determined.