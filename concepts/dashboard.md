# Dashboard
The dashboard serves as the controller for [machines](./machine.md) as well as an interface for [users](./user.md). Thus it can be seen as the brains of IJO. The dashboard acts as maximal node of a hierarchical tree structure, where all lower nodes are machine instances. This makes it possible for machines to, using containerization, run in other machines.

## API
The dashboard is accessible via an API. 

## Backend databasing/caching
By default the databasing exists of JSON files and the cache is saved in RAM. It is possible though to change this using plugins, so the defaults should be modular. This is done to make the dashboard more flexible and thus scalable.

## Frontend
The frontend is supplied to users by a standalone service. This allows the frontend to be scalable. The frontend then interacts with the dashboard backend via an API. This frontend can also be bundled with electron as a client. The client visuals can then be easily changed. This can also be done as an app. Users select the domain their dashboard is hosted from and this lets them login there and applies the customized styling.

## Styling
The way a user's dashboard looks is customizable. This is done with by loading a css file after the default css files.

## Development
The dashboard (and machine) are developed from the [main repository](https://github.com/ijo-sm/ijo).