## Example webservice project with Flask and React


# Deploying the web service project to production

## STEP1: install the nginx to load your project directly from the build folder.

## 1. Installing the nginx locally

> brew install nginx

For Mac, nginx will be installed in the following path:
>/opt/homebrew/opt/nginx/bin/

Default nginx docroot (folder that nginx load website) is
>/opt/homebrew/var/www

For configuration of nginx, you need to look at this location.
> /opt/homebrew/etc/nginx/nginx.conf 
By default, nginx listen to 8080.

To start the nginx in daemon mode, run this
>brew services start nginx
nginx will load files in `/opt/homebrew/etc/nginx/servers/`.

If you want to run nginx in forground mode, run this
>/opt/homebrew/opt/nginx/bin/nginx -g daemon\ off\;

### change the nginx.conf (/opt/homebrew/etc/nginx/nginx.conf) for local development.
Since we are not deplying to the actual server with dedicated nginx install(we will explort that option later.), we just want to check if nginx can load our production ready built project directly. 

To do so, we need to instruct nginx to load the index.html from the `\build` folder. Make the following changes in the original `nginx.conf`.

```
... some other configuration you don't need to touch ....
http {
... some other configuration you don't need to touch ....
    server {
        listen       8080; --> we are listening to 8080 for development.
        root /Users/peterhan/workspace/example_webservice/build;
        index index.html;

... some other configuration you don't need to touch ....

        location / {
            try_files $uri $uri/ =404;
            #root   html; --> comment that out for now
            #index  index.html index.htm; --> comment that out for now.
        }
... some other configuration you don't need to touch ....

```

To restart the nginx after changing the nginx.config, run this command (only for mac)
```
$ brew services restart nginx
--> the following will be printed out.
Stopping `nginx`... (might take a while)
==> Successfully stopped `nginx` (label: homebrew.mxcl.nginx)
==> Successfully started `nginx` (label: homebrew.mxcl.nginx)

$ nginx -s reload
```

If anything in `nginx.conf` is wrong, it will fail.

Now, open the browser and type `localhost:8080`.

# Getting Started with Create React App

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in your browser.

The page will reload when you make changes.\
You may also see any lint errors in the console.

### `npm test`

Launches the test runner in the interactive watch mode.\
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `npm run build`

Builds the app for production to the `build` folder.\
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.\
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `npm run eject`

**Note: this is a one-way operation. Once you `eject`, you can't go back!**

If you aren't satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you're on your own.

You don't have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn't feel obligated to use this feature. However we understand that this tool wouldn't be useful if you couldn't customize it when you are ready for it.

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).

### Code Splitting

This section has moved here: [https://facebook.github.io/create-react-app/docs/code-splitting](https://facebook.github.io/create-react-app/docs/code-splitting)

### Analyzing the Bundle Size

This section has moved here: [https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size](https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size)

### Making a Progressive Web App

This section has moved here: [https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app](https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app)

### Advanced Configuration

This section has moved here: [https://facebook.github.io/create-react-app/docs/advanced-configuration](https://facebook.github.io/create-react-app/docs/advanced-configuration)

### Deployment

This section has moved here: [https://facebook.github.io/create-react-app/docs/deployment](https://facebook.github.io/create-react-app/docs/deployment)

### `npm run build` fails to minify

This section has moved here: [https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify](https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify)
