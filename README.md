# Quality Infrastructure - Frontend Demo Code

## End-User Demos

This branch (`dist`) includes pre-built single-file versions of the Javascript code needed to embed metrics informations (charts and summaries) from the Quality Infrastructure on another site, along with demo code showing implementation examples.

All demos will need to be served from a webserver due to the use of AJAX.

The most basic examples of using the demo code are:
- `demos/index-singleFile-basic.html` (single Javascript file including jQuery + single CSS file)
- `demos/index-noJquery-basic.html` (separate jQuery include)

These examples require no particular knowledge of the underlying code implemented using the [Infusion](https://github.com/fluid-project/infusion) Javascript library, and use basic inline Javascript to render the panels.

More elaborate examples are:
- `demos/index.html?repo=gpii/universal`
- `demos/index-singleFile.html?repo=gpii/universal`
- `demos/index-noJquery.html?repo=gpii/universal`

These demos include navigation controls and functions that make use of Infusion component features to change the views presented by the graphs.

---

## Developing

- `npm install`
- `npm install -g grunt-cli`
- `grunt copy:frontEndDependencies`

This copies necessary front-end dependencies from `node_modules` to `src/lib`

## Building a Redistributable Single File Version

- `npm install`
- `npm install -g grunt-cli`
- `grunt copy:frontEndDependencies`
- `grunt dist`

This produces four single-file versions of the dependencies in the `/dist` directory:
- non-minified with all dependencies
- minified with all dependencies
- non-minified without jQuery
- minified with jQuery

## Libraries Used
- jQuery / jQuery UI
- Infusion
- D3
- Floe Chart Authoring Tool

## The Demos

The demos `index-singleFile.html` and `index-noJquery.html` in `/demos` assumes a single-file distribution has been built and use it in their markup; these demos are intended to guide those implementing the QI panels into their own site.

## Using a Container

A container running a web server can be used to host the redistributable source code mentioned above.

To build a container the following command should be used:

```
sudo docker build \
--no-cache \
-t gpii/qi-dashboard-frontend-demo .
```

Then to start a container this command can be used:

```
sudo docker run \
--name qi-dashboard-frontend-demo \
-d \
-p 80:80 \
gpii/qi-dashboard-frontend-demo
```

The server will be reachable at ``http://<your container's IP address>:8888/`` and will serve the contents of the generated ``dist`` directory.
